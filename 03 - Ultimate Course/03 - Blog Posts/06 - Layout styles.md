## Layout styles

Now that we have the card styles pretty much set, let's start looking at our layout.

In the design for mobile the cards are all in 1 column, and then on desktop, we have the cards in 3 columns. To build a grid of block items like these cards, I think using grid and auto-fit would be a really good solution.

I wouldn't really build this with flexbox, because while it is possible to get it to work, we're really trying to get these cards to conform to the 1 column or 3 column layout. When you have a specific layout requirement and you're trying to get the content to conform to it, grid is usually going to be the way you want to go.

Flexbox is good when you just want to fit the content into the available space, and you don't care as much about the specific sizing or layout arrangement.

Let's look at the website to see where we're at with the layout so far. Right now, each "blog\_\_item" card is a child of the "blog\_\_grid" div which we've made the grid parent. Things look good on mobile, but if we increase the viewport width, the cards will still be in the 1-column default layout and take up 100% of the width.

So for wider viewports, we want to go into multiple columns. Let's start this by writing "grid-template-columns" so we can change our grid template.

What do we want to set this to? Since the columns are all going to be the same width, we can use the "repeat()" function. This is going to be similar to what we did in the footer, where we used the repeat() function to have 2 columns on mobile and 4 columns on desktop.

Let's start by creating 2 columns, and set it to "repeat(2, 1fr)", so we'll have 2 columns and divide the available width between them.

Now when we save, on the website for mobile, we have 2 columns. Things do look squished for now. But as the viewport keeps increasing, we stay on 2 columns and the cards get wider.

So how do we go from 1 to 3 columns? On the footer, we used media queries to switch between repeat 2 and repeat 4 columns.

However, here I'm going to show you a more advanced method of going to multi columns without needing media queries. I'm going to change the number of columns from "2" to a new value called "auto-fit".

Auto-fit is a really powerful feature in CSS grid that lets the browser decide the number of columns that can fit in the available space. But you can't just use it by itself-- if we just leave the styles like this and save, on the website the layout will only be 1-column, no matter what width we're at.

This is because we set the column size to be 1fr, meaning it'll take up all available width. So the browser will only be able to fit 1 column on the available space.

What we need to do is to instead of just having 1fr as our column width, to use another function in CSS grid called "minmax()". Minmax() takes two parameters, a minimum number and a maximum number.

In order for it to work, you want to have one of the numbers be an absolute number, like 300px, and have the other one be a relative number like 1fr, auto, or a percentage.

This can be hard to wrap your head around if you aren't super familiar with minmax(), but I'll show you how it works. Let's replace the 1fr value with minmax(). Then in the function, let's make the min number "u.rem(300)" for 300px, then add a comma and set the max number to be 1fr.

What this will do is tell the browser that the cards have to be at least 300px, and then it will fit as many columns of 300px width onto the row. Then if there is any available space, it will allow the columns to grow to take up all available space in the parent.

So when we save, let's go to the website and start with mobile. And I'm going to inspect one of the blog\_\_item elements and go to the Layout tab so we can monitor the width of the columns as they change.

So on mobile the columns are 327px wide. And now let's drag out the right edge right until we hit that 700px breakpoint. And that is about... here.

In the Rules tab we can see our grid template columns and auto-fit getting applied now, and we have two columns. And each column is [xxx] pixels wide. So the browser is starting with that 300px width and is able to fit 2 columns in the row, and since there's a little space left, each column grows to fit so all available space is taken up.

Now let's keep increasing the viewport width. So the columns are progressively growing wider, and then once the browser can fit 3 columns of 300px wide at [xxx] wide, it changed the layout to be 3 columns.

And if we can get at the exact breakpoint where the layout changes, if we inspect one of the blog\_\_item elements, we can see that they are exactly 300px wide, which is again coming from our minimum width that we set in the minmax() function.

Then as we keep increasing the viewport width, the columns increase. And then when we max out the wrapper class at 1200, the entire content doesn't grow anymore, and we are left at 3 columns wide.

This is just really cool that we can get a bit more flexible with CSS grid layouts, all with that one style rule for all devices.

The cards are looking pretty good! However, I'm realizing that the title is supposed to be centered. If I go back to Figma and check, it is centered on both mobile and desktop.

[ Center text with "fullwidth" class, create "fullwidth dark" class to use for FW Feature and FW CTA to have "color: var(--text-light)" ]

However, one thing that I'm noticing is that because the gradients are all the same, it's making the cards look a little bit too same-y or monotonous, just from a design perspective. It looks a bit weird seeing the gradient cross cards going down.

So next up we're going to try to add a little variation in the gradients across the different cards.
