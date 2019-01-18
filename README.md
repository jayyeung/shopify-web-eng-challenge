# Shopify Web Engineer Challenge - Summer 2019

Build a web app to search for waste items using the Toronto Waste Wizard database, and save frequently used ones.

**Challenge:** https://cdn.shopify.com/static/web-eng-challenge-summer-2019/index.md

**Live App:** https://jayyeung.github.io/shopify-web-eng-challenge/

**Codebase:** https://github.com/jayyeung/shopify-web-eng-challenge

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
I found two ways to get the data: either prefetch the data or fetch it when the user searches. 

**Displaying the description:**
At first, when displaying the description of each entry, I couldn't get it to render properly. After some more research, I later found out that 

## Design
It was very important for me to recreate the app as close to the design mockup as possible. Imagine a designer who've taken their time painstakenly crafting the UI only to end up with something completely different!

**Style organization:**
For component-based styles, I simply styled them using scoped scss.
For more global styles, I grouped them into "modules" (in the `styles` folder) that would all be imported into one `main.scss` file. Inspired from [my favourite CSS framework](https://www.iotacss.com/), I found that this technique made it easy to maintain the styling as you can edit, add, or remove modules as you wish.

**Spacing:** 
Measuring the mockup up in Photoshop, I noticed that spacing between elements and line-height were roughly multiples of 4; I simplifed the spacing into spacers of **4, 20, 28, 40, and 80px**, and created a file `styles/settings/_spacing.scss` that will generate re-usable classes based on these spacers.

