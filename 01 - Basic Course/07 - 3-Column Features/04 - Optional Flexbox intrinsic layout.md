# Flexbox intrinsic layout

Let's start building the flexbox intrinsic approach, where we still have the 1-column to 3-column layout, but without using media queries.

Let's go back into the features.scss file, and we're going to redo all of our flexbox rules. Now, I don't want to totally throw away the styles we just wrote, so I'm going to select the `features__wrapper` and `features__item` selectors, duplicate them with Ctrl-D, and then comment out one copy.

And I'll add another comment to label it `Flexbox -- media queries`. And this is just for the sake of the course-- that way if you ever want to go back to this for reference or to use this approach it'll be here. If this was for an actual work project I wouldn't keep other versions of the code in comments like this.

Now let's go to the uncommented code, and I'm going to delete all the flexbox style rules so we can start from scratch. So in the `features__wrapper` that's basically all the rules-- so I'll delete everything until we just have the empty selector. And in the `features__item` that's the `flex: 1` rule.

And I know we said that we're trying to not use media queries, but unfortunately, to change text alignment we have to use media queries, so I will be leaving them. But we'll be doing all the layout styles without needing them. Ok, now, in the website the Features section is back to our default mobile styles where everything is in 1 column.

To add flexbox, similar to what we did last time, we're going to go to the parent element, the `features__wrapper` div, and in our styles add `display: flex`. And for our intrinsic approach, we want to allow wrapping, so let's also add `flex-wrap: wrap`.

And now on the website the features items are wrapping, but they seem wider than what we have in the design, since all 3 can't fit on one row.

So we need to add add flex properties to the flex children to control their width. Let's go into the design and see what width we have set for the Features items. In the desktop design, the items are 346px wide, and on mobile they are 327px.

What we can do is to set all the flex children to the same width, and not be greater than the 346px on desktop, but allow them to shrink if necessary on mobile viewports.

Just in the browser for now, in the `features__it em` selector, I'm going to start adding flex properties. I do usually use the `flex` shorthand property, but since we're still figuring things out let's write each one separately. First, let's set `flex-basis` for the initial width of the flex child items. I'm going to set it to 346px-- and we're using pixels for now since we're just testing in the browser.

And we also need to set `flex-grow` and `flex-shrink`. If 346px is going to be the initial width of the items, we don't want them to grow larger than that, since that's what we have in the desktop design. So I'm going to add `flex-grow` of 0, and `flex-shrink` of 1. And it still looks good, so let's combine them into the `flex` shorthand property and set it to `flex: 0 1 346px`.

And now, the three Features are all on the same row! Let's copy that `flex` rule and paste it in the `features__item` selector. I like putting my flex and grid styles at the top, so I have it before the text-align rule. And going back to the website, the width of the items looks good on desktop.

I'm going to click on the `flex` label in the flex parent to turn on flexbox highlighting so we can see what's going on in a bit more detail. On large viewport widths, you can see that there's extra space on the right. And each Features item is exactly 346px. Then, if we narrow the viewport, the items start to wrap to a new row if there's not enough room for them to fit, and they are still at 346px. Then on mobile widths we do have the Features all in 1 column, and they are allowed to shrink below 346px in order to fit.

So that's pretty good. However, going back to a desktop width, they're all aligned to the left, and it would look better if they were centered so it doesn't look as uneven.

To control the alignment of the flex items along the main axis, which is horizontal in our case, we would use the `justify-content` property. By default it's set to `flex-start`, so all the items are packed to the start or left side, with any extra space on the end.

To center the flex child items, we can use `justify-content: center` which packs the children in the center, with equal space on either side. This can be useful for when the viewport decreases so that all 3 can't fit on one row, the last child by itself is centered. Which I think looks a bit nicer than having it on the left.

Let's also add a gap value to add space between the flex child items. In our previous version, we set the `gap` to 6.67%. However, if we do this here, we can see space added between the first two items on the top row. But there's no space added between rows. This is because for the row-gap, the browser needs to calculate 6.67% of the parent, the `features__wrapper`.

But-- and this is a quirk of CSS-- unless the parent height is explicitly set, it will be considered zero. And 6.67% of zero is zero, so the row-gap will be nothing. Just for illustration purposes, if I set the height of the `features__wrapper` to 600px, then we can see the row-gap becomes something other than zero. If I delete the height, it goes back to zero.

Fortunately, the `gap` property is actually a shorthand property for `row-gap`, the space between rows, and `column-gap`, the space between columns. In the browser, if we expand the `gap` property we can see that both row and column-gap are set to 6.67%. For the row gap, let's go back to the static value of 40px which is what we were using previously for the mobile layout.

We can do this by adding `40px` to the `gap` property so it says `40px 6.67%`. And now we can see the row gap has been added. That looks pretty good! Let's copy the new styles-- for `gap` and `justify-content` and then in our code paste it in the parent `features__wrapper` selector.

Let's save, and let's check out the website again. And now we can see that the space between both columns and rows is working. The flex child items are centered, and they go from 1 item per row at small viewports to 2, and then 3 items per row as the viewport gets bigger.

Let's go back to the width where we have 2 features on the first row and the last one on the second row and centered. I just want to note that this arrangement isn't something you can do with CSS grid, because the centered third feature is breaking the 2 column layout in the way that it's centered like that. Grid can wrap items if need be, but the last feature would have to be in the same column and directly below the first feature.

I'm not at all saying that flexbox is better than grid, but they have very different ways of approaching layout. Flexbox is useful if you have content and want it to fit it, and don't mind breaking the arrangement of rows and columns to do it. With grid, you have a set grid template of rows and columns and while it's not as flexible as flexbox is, it gives you a level of control where you can place grid child items in any cell in that template.

Overall, the more intrinsic layout we have here with flexbox and not needing media queries is pretty good. But there is one small issue. Remember how we wanted everything to be centered when everything is stacked to 1 column on mobile widths, but left aligned on larger viewports?

If we start with a mobile width, that part is working fine. But as we gradually increase the viewport, there's a point where we still have 2 columns in the first row, but the text is centered. And then as we continue increasing we hit that large breakpoint to make the text and image left aligned.

Unfortunately there's no easy way to make the intrinsic layout go to 1-column at the exact breakpoint where the text-align changes to center. So in order to have the most control you would have to go back to the responsive approach with media queries, which is why I like the responsive approach a bit better.,

But if the design has everything left aligned on all viewport widths including mobile, then the intrinsic approach will work fine for this.

Ok, I hope this optional video with the alternative intrinsic approach has been helpful. This is the end of the 3-column Features section, so don't forget to commit your changes in GitHub Desktop to the main branch, and pushing to origin, before moving on to the next section, the Full-width Feature.
