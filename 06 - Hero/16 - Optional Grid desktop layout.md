# Optional: Grid desktop layout

Alright, so for our desktop grid layout, the first thing we need to figure out is what our grid template should look like for desktop. In our design, we have our 2 columns, and like we mentioned earlier, the left column has the text and takes up 6 columns, then the unicorn is on the right and it takes up 5 columns.

So even though we need to change the order of the image and text, we can handle that later. Right now we should create our desktop grid template based on what we see in the design. In our styles, in the `hero__wrapper` large breakpoint, I'm going to add `grid-template-columns: 6fr 5fr`.

This is similar to what we did with the `flex: 6` and `flex: 5` style rules. But where in flexbox we were setting the flex growth rate, with CSS grid we're creating the number and size of columns. The `fr` or fractional unit will divide up the available space between the columns, with the first column getting 6 parts and the second column 5 parts.

Let's save and see how that looks. And in our website, we have our 2 columns. The most obvious thing we want to fix is switching the unicorn image and the text placement. Fortunately, in grid (and also in flexbox) we can use the `order` property to assign an order to the child items. By default, `order` is set to 0 for all elements, and then it will follow the order based on what comes first in the markup.

Let's make the unicorn second-- just in the browser, in the `hero__image` styles, I'll add `order` and set it to 2. And now we can see that the unicorn is in the second column. And the column sizes didn't change-- they're always going to be set at the 6fr 5fr sizes that we created in the grid template. We're only assigning which column the grid child items get put into.

Since we didn't assign an order to the `hero__text`, it is at `order: 0`, so technically we could set the unicorn to `order: 1` and it will still come after the hero text, as you can see. But I think it's a bit more intuitive to set it to `2` to have it come second. This is just my personal preference-- `order: 1` works just as well.

Let's add that to our styles, for the `hero__image` selector, large breakpoint. I'm going to add `order: 2` before the `width` property, because I prefer putting my flex and grid styles before the other styles. And save, and on our website, we can see the unicorn is on the right for desktop. And if we reduce the viewport, on mobile the layout goes to 1 column, and the unicorn is first. Looks good!

Going back to desktop, there's one other thing I can see that we need to change. If you want, pause the video, and compare what you have on the website with the desktop design in Figma, and see if you can identify what we need to change.

Ok, so the thing that I noticed is that we need to vertically center the content on desktop, right now, the hero text is up at the top, but we'd like it to be centered to where the unicorn is, since the unicorn is taller than the hero text. And we also want the unicorn to be vertically centered on smaller desktop viewports, where the text is taller than the unicorn image.

Again, if you want to try this yourself first, see if you know what style rule to add and where, in order to vertically center the grid content. You can always use the CSS Tricks Grid Guide for reference to help you find the property you need.

If we go to our styles, the most efficient way to vertically center the grid child items is to go to the grid parent selector, `hero__wrapper`, and add `align-items: center`. I'm adding this under `justify-items`. This is our default styles which will affect mobile, but I don't think it will cause any issues to do it here.

And if we save, and look at the website, we can see that on desktop the hero text is now vertically centered. If we go down to a smaller viewport, we can see at one point that the text is taller than the unicorn, and here the unicorn is centered vertically to the text.

One thing I'm noticing is that the unicorn seems smaller than it should be. If we check the desktop design, the unicorn is 483px wide. But on our website, it's only [XXX] pixels wide. So we need to look through the styles to see what might be causing this issue.

If we inspect the unicorn image, in the `Rules` tab, the unicorn has the `max-width` and `width` style rules. And that `width: 62%` is probably causing the unicorn to be smaller than we want. If we uncheck that rule, then the unicorn gets bigger. We originally needed the 62% for mobile styles, so we'll need to cancel it out for desktop styles. One thing we could do is in the desktop media query, set `width` to 100% like we had in our boilerplate styles. If we do this, it will override the 62% width.

I think that might be the simplest way to adjust the width when going from mobile to desktop, so let's go into our styles and do that. In the `hero__image` class selector, in the large breakpoint, I'll add `width: 100%`. And when we save, and in our website the unicorn is now the correct size of 483px.

Ok, so let's refresh to get back to our saved styles, and do one more check of the hero section, on desktop. Looks good, we have the 2 columns and the text and image are vertically centered. And as we go to mobile widths we go to 1 column, with the unicorn on top, and centered horizontally.

So the hero styles look pretty good. If this was a real work project, the next thing I would do before showing this to my team is to do one more check, a bit more detailed, to make sure that all the elements are the right size, color, etc., and that the spacing is right.
