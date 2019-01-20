# Shopify Web Engineer Challenge - Summer 2019

Build a web app to search for waste items using the Toronto Waste Wizard database, and save frequently used ones.

**Challenge:** https://cdn.shopify.com/static/web-eng-challenge-summer-2019/index.md

**Live App:** https://jayyeung.github.io/shopify-web-eng-challenge-summer-2019/

**Codebase:** https://github.com/jayyeung/shopify-web-eng-challenge-summer-2019

## Mockup
![Design](http://cdn.shopify.com/static/web-eng-challenge-summer-2019/design.png)

## Project setup
```
npm install
```

**Running for development**
```
npm run serve
```

**Running for production**
```
npm run build
```

# My Thought Process
Below are some of my thoughts when doing this challenge:

## Functionality
Simply, the app will initially prefetch the data and will filter out the results when the user searches.
When a user favourites an entry, the `waste-entry` component will emit a callback to the parent component, which will handle the favouriting and update the list.

**Fetching the data:**
I found two ways to fetch the data: either fetch all data on app start, or just when the user searches a query. Although there is some overhead at the beginning, I felt the benefit of prefetching the data would be that you can easily filter through each entry, faster than sending a GET request every time. However, if there were a lot entries, it might be better to fetch on search instead.

**Displaying the description:**
I intially had trouble displaying the description. Using `v-html` to render the body, it would not render the text into actual HTML elements. After some research, I found that it wasn't working because I needed to unescape the HTML first before rendering. Instead of writing my own function (which I initially did), I felt it was more reliable to use a small NPM package (`unescape`) to decode it. 

## Design
It was very important for me to recreate the app as close to the design mockup as possible. Imagine a designer who've taken their time painstakenly crafting the UI only to end up with something completely different!

**Style organization:**
For component-based styles, I simply styled them using scoped scss.
For more global styles, I grouped them into "modules" (in the `styles` folder) that would all be imported into one `main.scss` file. Inspired from [my favourite CSS framework](https://www.iotacss.com/), I found that this technique makes it easy to maintain the styling as you can edit, add, or remove modules as you wish.

**Spacing:** 
Measuring the mockup up in Photoshop, I noticed that spacing between elements and line-height were roughly multiples of 4; I simplifed the spacing into spacers of **4, 20, 28, 40, and 80px**, and created a file `styles/settings/_spacing.scss` that will generate re-usable classes based on these spacers.

**Responsiveness**
A problem that I used to have when coding websites was responsive text. Normally you would use manual breakpoints to change the font-size, but that results in awkard type sizes on devices that hover but don't pass these breakpoints. Ever since, I've been using a technique with `calc()` and viewport units to linearly interpolate the sizes between breakpoints that I used in `styles/settings/_type.scss`.
