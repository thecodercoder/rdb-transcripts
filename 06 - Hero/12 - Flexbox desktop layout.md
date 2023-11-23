# Flexbox desktop layout

Let's work on the desktop layout now. I'm going to turn off Responsive Design Mode and go back to a desktop viewport width. So now what we have is all the content in one column. We can make one change to an existing style in order to change the layout to 2-columns, with the text first on the left and then the unicorn on the right.

Feel free to pause and try this out yourself!

Alright, so to change the flexbox layout from 1 column to 2 columns, we can change the `flex-direction` property on the `hero__wrapper` div, to be `row-reverse` instead of `column`. We can test it out in the browser first, and then once we know that's what we want, we can make the code change.

We only want to change the flex-direction for desktop viewports, so in our styles we want to add it in our large breakpoint. So in the media query I'll add `flex-direction: row-reverse` before the padding, similar to what I had in the default styles.

And when we save and check out the website, we can see that the layout is in 2 columns for desktop. And if we use Responsive Design Mode and move to a mobile viewport, it will change to a 1 column layout.

I do want to note that changing flex-direction isn't the only way to make this 2-column layout on desktop using flexbox. I'll show you some other flexbox approaches to go from 1 to multiple columns in the next section, some which don't require media queries. But this seemed like a good opportunity to take advantage of flex-direction.

Going back to the desktop view, one nice thing is that the `align-items: center` style rule which centered the unicorn horizontally for mobile, is now centering the hero text vertically for desktop, since the main and cross axes have flipped for desktop. So we don't need to add another style rule to center the content vertically.

Let's turn on the flexbox inspector and see what other changes we might need to make. One that I can see is that it looks like there is some extra space under the unicorn image, which is throwing off the vertical centering and making the hero text a bit lower than it should be.

On the desktop design, the top of the text should be about level with just below the middle of the unicorn's horn. But on our website it's lower, just level with the top of the head. So we need to get rid of that space under the unicorn, at least for desktop.

If we inspect the unicorn image, hovering over it shows us that there's a bottom margin under it. And in the styles, that's coming from the `margin-block-end` that we set on it. This is something that we added for mobile to put space between the unicorn and the hero text, but we don't want it for desktop.

And actually, since we're using flexbox on the mobile layout, it might be better to use the gap property to add the space, instead of margin. Because the gap will only add space between flexbox child items, so it won't add space below the unicorn on desktop since there's nothing actually underneath it.

Let's try that in the browser first. In the `hero__image` styles I'm going to uncheck the `margin-block-end: 40px` style rule to get rid of the space. Then in the flex parent `hero__wrapper` I'll add `gap: 40px`. Now we have that space back under the unicorn for mobile. And on desktop the gap is between the text and the unicorn, and there's no space under the unicorn anymore, so the text is vertically centered correctly.

We might need to adjust the size of the gap for desktop, but I think this is the way we want to go to add that space. So I'm going go to our styles, and in the `hero__image` selector I'll select the `margin-block-end` of 40px and cut it, then paste it in the `hero__wrapper` styles under `flex-direction`. And we want to change the `margin-block-end` property to the `gap` property instead.

Now save and check out the website, and we can see that gap on desktop, and also on mobile. Let's go back to the design and see what else we need to do for the desktop layout.

In Figma, on the desktop design, just make sure that you have the Layout grid turned on. This is when you click on the `Desktop - 1440` frame, either in the left sidebar, or the little title in the top left outside the frame itself. When the frame is selected in the right sidebar you should see a `Layout grid` panel-- make sure the `12 columns` grid has its eye icon to the `open` state to unhide it.

The 12 columns are spanning the 1200px max-width of our `wrapper` class. And we can use the 12 columns to determine how much width to give each part of the hero section. The hero text on the left, if we start counting, takes up 6 out of the 12 columns. And the unicorn image takes up about 5 columns. And then there's about 1 column of space between them which is going to be our flexbox gap.

With flexbox, you can allocate the space to each flex child by using the shorthand `flex` property. And it's actually recommended in the official documentation to use the shorthand property as opposed to setting the individual flex-grow, flex-shrink, and flex-basis properties yourself, because it uses some default values that will help fit the flex children a bit more intuitively.

Let's go to our styles and start adding flex to the unicorn image and the `hero__text` div. First, for the `hero__image`, let's add a large breakpoint since we are just affecting the desktop styles. I'm going to write `@include u.breakpoint(large)`and curly brackets, and then I'm going to add the`flex`property and set it to`5`. I'm using 5 because in the design, the unicorn takes up 5 out of the 12 columns.

Then for the `hero__text` div I'll again add a large breakpoint with `@include u.breakpoint(large)` and in the curly brackets I'm going to set `flex` to 6. Similarly, we're using 6 because in the design the hero text takes up 6 out of the 12 columns.

Last, we should adjust the gap property, since it needs to be more than the 40px we had for mobile. So in the `hero__wrapper` selector, in the large breakpoint that we already have, I'll add `gap` and in the design the space between the hero text and the image was about 1 column.

So I'm going to do some approximate math and pull out the calculator, and divide 1 by 12, and it's a bit more than 8%. Let's round up to 9, and set the gap on desktop to 9%. Again, this is all sort of approximate, not exact.

Let's save that, and see how it looks on the website! Ok, so now you can see that the gap is bigger than it was before, which is great. Let's see how this looks with Responsive Design Mode, and if you drag out the right edge, you can see how it changes as the viewport changes.
