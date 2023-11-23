# Optional: Grid mobile layout

To start off with our grid layout, let's go into our hero.scss file, and I'm going to go through our styles and comment out the flexbox style rules, so that can start from scratch with our grid styles, but we still have them for future reference.

In the `hero__wrapper` I'll comment out `display: flex`, `flex-direction`, I'll leave `gap` since it does the same thing in both flexbox and grid; and then comment out `align-items` and keep the `padding-block`. Then in the large breakpoint I'll comment out `flex-direction` and keep `gap` and `padding-block`. Just for organization's sake, I'm going to group the commented styles up at the top together.

In the `hero__image` selector, I'll comment out the `flex: 5` rule in the breakpoint. And the same in `hero__text`, I'll comment out `flex: 6`.

Looking at our website, and sliding from desktop to mobile viewport widths, we can see that all the basic styles are there, and the unicorn image is still scaling. We just don't have the 1 to 2 column layout and centering the unicorn image.

Let's start adding our grid styles for mobile. The grid parent will be the `hero__wrapper` div just like it was the flexbox parent, and then also the grid children will be the `hero__image` and `hero__text` elements, again like they were for flexbox.

In the `hero__wrapper` selector, we first want to turn on grid by adding `display: grid`. Then we'll have to create our grid template, since unlike flexbox nothing will happen by just adding `display: grid`. For mobile, we want a 1 column layout, so I'm going to add `grid-template-columns: 1fr` to create 1 column that will take the full width of the grid container.

And now let's save and see how that looks. And now we have our mobile layout, with the gap of 40px between the two rows, since we kept that from our flexbox styles. The hero text looks pretty good, but we still need to center the unicorn in the top row.

With flexbox, we could center along a row by setting `justify-content: center`. However, grid is a little different. Let's check out the CSS Tricks grid guide-- you can search for `css tricks grid` and it should be the first result. Once you're on the page, do a Ctrl-F to search the page for `justify-content`.

And you can see in the little diagram that `justify-content` controls the alignment along the inline, or row axis of the entire grid, if there is space available within its container. If you want to control the alignment of grid child items within their individual cells, you'll want to use `justify-items`. Let's do another Ctrl-F and search for `justify-items`, to see a visual depiction of what that looks like.

`Justify-items: center` is what we're looking for, so let's go back to our styles, and in the grid parent `hero__wrapper` I'll set `justify-items: center`. And when we save and check out the website, the unicorn is now centered!

And let's do a quick check to compare the website with our mobile design. I'm going to use Responsive Design Mode to emulate the iPhone. And if we flip back and forth between the design and the website, it looks good to me-- the size of the image and text look good, and the spacing between elements seems the same between both.

Let's now set up the desktop layout.
