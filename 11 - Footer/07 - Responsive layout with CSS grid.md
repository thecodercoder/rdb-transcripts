# Responsive layout with CSS grid

Now, before we start writing our grid styles, let's take a look at the website and the source code to identify where we want to set up our grid.

On the website, everything in the footer is in the footer tag. And in there we have our hidden h2 tag, and then the visible content is in the `footer__wrapper` div. In the `footer__wrapper` we have the `footer__logo` section tag, and then each of the 4 footer columns are in their own section tag.

Ideally what I'd like to be able to do is to have the footer logo and the footer columns be grid children, so the grid parent or container will be the `footer__wrapper`.

In the footer.scss file, I'm going to go to the `footer__wrapper` selector, and I'm going to make this the grid parent by writing `display: grid`. When we've worked with flexbox previously, you might remember that just adding `display: flex` will automatically place the flex children all in one row, whereas when adding `display: grid` nothing seems to change on the website.

However, the browser is still placing the grid child items. If I turn on the grid highlighting, we can see that the grid children have each been placed in their own row.

This is because of some default style rules related to grid. Let's select the `footer__wrapper` grid container, and take a look at the `Computed` tab. If I filter for `grid` then we can see some grid properties.

We've set `display: grid` in our styles, which we can tell because it has the arrow that shows us where the style rule was set. But these other properties don't have an arrow, meaning they are coming from the browser defaults.

One of them, `grid-auto-flow`, is set to `row`. This means that if we don't explicitly add styles to set the grid template, the browser will put each grid child in its own row.

We can change this direction, kind of like how in flexbox we can change the `flex-direction` to be `row` or `column`. In our styles, if we add `grid-auto-flow` and set it to be `column`, then the browser will arrange the grid children in 1 row, each in their own column.

I just wanted to mention this because I think it seems to be a slightly lesser known feature, that you can let the grid auto layout and just set the direction the children will get added to the grid.

However, since we need to make the logo take up the entire first row, and have the footer columns begin on the second row, we can't rely on just the auto flow, and will need to explicitly create a grid template. I'm going to reload to refresh from our saved styles.

Let's refer back to the design. We want the footer to be 2 columns on mobile and 4 columns for desktop.

Let's go to VS Code and start writing our mobile styles. In our grid parent, the `footer__wrapper`, let's add `grid-template-columns` and set it to `repeat(2, 1fr)` to create 2 columns on mobile. And on our website I'm going to load the iPhone view, and turn on the grid highlighting so we can see the lines in our grid template.

Now we have our 2-column layout. Next, let's set the logo to take up the entire first row. With grid we can place each grid child in any cell within the template, using the `grid-column` shorthand property, which lets you set the `grid-column-start` and `grid-column-end` properties.

One way you can set these is with the grid line numbers. On our grid the columns are between the vertical grid lines. So right now, the `footer__logo` child is between column line 1 and column line 2. It starts at line 1 and ends at line 2.

We want it to end at the last line, line 3. So just in our browser, we can write `grid-column` then first write the line number it starts on, `1`. Then a forward slash, and the line number it ends on, `3`. And now the `footer__logo` is taking up the whole first row.

We can also instead of a line number for either the start or end, write `span` and then the number of columns we want it to take up. So if I change the grid-column-end number to be `span  space 2`, it will start at line 1 and span 2 columns. Which ends up doing the same thing as saying it will end on line 3.

And if we write `span 2 / 3`, that will also do the same thing, it's spanning 2 columns, and instead of saying where it starts, we're saying it will end on line 3. I kind of like saying the start line and the span 2.

So let's go to VS Code, and for the `footer__logo` selector, let's write `grid-column` and set it to `1 / span 2`. In the website, the layout looks pretty good, pretty close to the design.

However I am noticing some spacing issues. We didn't add a gap yet, and we need to add some space between the rows, because they look pretty close. And we probably also have space between the columns that we should add.

In the design, let's check out the mobile design. If I select the `Company` footer column, and hold down Alt, there is 40px of space under it between rows, and 20px of space next to it, between columns.

So let's add that in our styles. [ minimize Figma ]

In the `footer__wrapper` let's add `gap` and we can set different row-gaps and column-gaps. The first number is row-gap or space between rows. That's 40px, so let's use our rem() function and write `u.rem(40)`. And the second number is the column-gap, so let's set that too, with `u.rem(20)`.

Now we can see on our website, we have the shaded gap space between the tracks. However I can see some parts of the grid where it looks like there's some extra space. Can you identify some areas in the grid where you can see that extra space? You can pause the video if you want.

So one place I'm seeing, is under the copyright text-- that should be right up against the edge of the cell. Let's see what's going on.

If I inspect the paragraph, we have a bottom margin, which looks like is from the browser defaults. Let's get rid of that. The selector is `footer__copyright` so in our styles in that selector, I'll add `margin-block-end: 0`. And now the space is gone.

The other place I'm seeing extra space is under the `Contact` text link and the `YouTube` text link. The extra space at the bottom of the `Support` column and the `Resources` column are fine-- they're there because those columns have fewer links than the `Company` and `Follow` columns, so since they're in the same row, they will have to have extra space.

However let's look at the `Contact` link in the `Company` column. If I inspect that, it does have a bottom margin, or margin-block-end in the `footer__link` selector. So we added that to all the `footer__link`'s. And if we look at the `Layout` tab in the Box Model, we have 10px of space on the bottom.

We do need the space under the previous links, but we just don't want the space after the last link.

I think a better way of adding that space would be to remove it from the `footer__link` and add it by making the unordered list in the `footer__links` to be another grid parent. And add the space using gap, between each of the `footer__item`s.

Let's do that. In our styles, first let's delete that space from the `footer__link`-- get rid of the `margin-block-end` style rule. And if we save, the space is gone.

Now, let's go up to `footer__links` and make it a grid parent with `display: grid`. And if you remember, because of the `grid-auto-flow` putting the grid children in their own row automatically, if we add a gap of `u.rem(10)`, then the 10px of space will now be added between rows. And it's not adding it under the last link because gap is only added between children, not on the edges of the grid.

So now on our website, we have the space and it looks good! We could also have added the gap by making the `footer__links` a flex parent (change to display: flex`). But with flexbox, it will by default put the flex children in their own column. So to make it work we'd have to add `flex-direction: column`.

And that's one more style rule than our grid approach, so for the sake of writing less code, I like the grid approach better for this. [ Undo to grid, save to reload ]

Okay, so we have our mobile grid pretty much set. Now let's write our desktop styles.

For desktop, we want to go from a 2-column grid to a 4-column grid. In order to do that, I'm going to add a media query at our desktop breakpoint and change the grid template to be 4 columns.

If you want to try this yourself first, you can pause the video now.

Okay, so we want to change the grid template in the grid parent which is the `footer__wrapper` selector. So in there, we need to create our media query.

To do that, let's load our mixin by writing `@include u.breakpoint()` and in the parentheses we want to set it for desktop, so I'll write `large` in it. Then I'm going to copy our mobile grid-template-columns rule, and paste it in our breakpoint, then change the repeat number, which sets the number of columns, to `4`.

Let's save, and check out the website. Mobile still looks the same which is good. And if I drag out that right edge until we get above the 900px large size, then it changes to 4 columns.

Our grid template is good, but we have a problem. The footer logo that we set to span 2 columns with our `grid-column: 1 slash span 2` rule is still spanning 2 columns. And then the footer columns are getting added starting in the third column.

For desktop, we want the logo to go all the way to the end of the row, just like we did on mobile. And then the footer columns should start on the second row.

Now, this is a little bit of a challenge, but there is actually a way that we can change the `footer__logo` grid-column style so that it will always go until the end of the row, no matter how many columns are in the grid. And it doesn't need a media query, the same style rule will work for all devices.

If you need a hint, make sure you have the grid highlighting turned on so you can see the line numbers.

Now if you want to try to figure this out, pause the video now, and then unpause when you want to see my solution.

Alright. So, we had set the `footer__logo` to start at grid-column line 1, and span 2 columns. But instead of `span` you can set the ending grid column line number. So for mobile to span 2 columns we could say `grid-column: 1 / 3` to go from lines 1 to 3.

Our problem is, that 3 line won't work for desktop. On desktop, the last line in the first row is line number 5 all the way at the end. But if we try setting `5` that won't work if we go back to a mobile width, because now it's forcing the template to be 4 columns and there's not enough room on mobile. Let's undo that to go back to `3`. And go back to a desktop width.

Let's take a look at the grid lines. The last line, is numbered `5` up at the top. But if we look at the bottom of the grid, there are another set of column line numbers, but they are negative, starting from -5 and going down to -1.

And if we go down to our 2-column layout on mobile again, the negative numbers start at -3 and again go down to -1.

What's happening here is that with the top numbers, each grid column line gets numbered from 1 then goes up by 1 until the last number going from Left to Right.

The bottom numbers go from Right to Left, and start with -1 and then go down to -2, -3, and so on until the last column number.

What this means is that the last grid column line is always going to be line number -1. So we can change the `footer__logo` to start at 1, and then end at -1.

When we make that change, on mobile -1 is the same line as line 3. On desktop, the -1 line is the same as line 5. So by using the negative line numbers, we're able to get the logo to span the entire first row, no matter how many columns are in the grid template. Pretty cool, right?

I think our responsive grid template is working-- we have 4 columns on desktop and 2 on mobile. Let's turn off the grid highlighting so we can see how things look without all the lines. Not too bad!

I do feel like at tablet widths, there's a lot of extra space since we're still at 2-columns. If I select iPad, it does seem like there's a lot of space.

Let's go to 4 columns sooner. In our styles, I'm going to change our breakpoint to trigger at `medium` instead of `large` sizes. If we save, now for tablets we have 4 columns so there's not as much extra space.

However it kind of looks like the middle two `Support` and `Follow` columns are closer together than the two outside ones. Let's turn on our grid highlighting again and see what's going on.

If we go to the `Layout` tab, let's go to the grid diagram and see how wide the columns are. They are all the same width, [XXX]. This is because we sized the columns to be 1fr, so they'll always be equal.

But if we look at the actual text links, the `Support` text links are just longer words than for example, the `Company` or `Resources` links. And the `Follow` links are wider because they have the social media icons.

So setting the columns to be 1fr is making there be more negative space in the first and last columns. So it looks kind of uneven when you turn off the grid lines.

This wouldn't be as noticeable if these were cards with a different background color. Let me show you how that would look. I'm going to go to one of the `footer__column`s and click the `plus` icon to add a selector for the class. And in it I'll add `background: #cecece`.

So now all the columns have a background color, and now the spacing difference doesn't stick out as much because we want the cards to be the same width. But if we get rid of that style, you can see that it does look uneven.

In our styles, what we can do to fix this is to size the columns not equally, but according to their content width. We can do this by changing the `1fr` to `auto` in our 4-column grid-template. And now the columns seem a lot more equal, because each column width is based on the width of the actual content, then any additional space is divided among the columns.

So if we turn on our highlighting again, and go to the `Layout` tab, we can see that the columns are different widths, and the `Support` columns is definitely the widest column.

Now, you might notice that the middle of the grid, which is where the line 3 label is, isn't centered on the website. If you compare it to the `Free Trial` button above the footer, the line is a bit to the right of the center of that button, which IS centered.

But, if we turn off the highlighting, I think it feels better to have the footer columns be more evenly space out. And it's not as noticeable that it's not perfectly centered. Just keep that in mind, because there might be cases where you do want the center of the grid to be centered in the website.

But yeah, I think that looks good. And for iPhone, we are using the `1fr` equal widths columns, but I think that looks fine. So we'll just use `auto` to size the 4-column grid.

All right, and now we can consider the footer section complete. And that's the last section of the website that we're going to be building in this basic course.

So let's commit our changes in GitHub Desktop. So here's our changes in GitHub Desktop in the changes tab. Again, we're just going to kind of eyeball all the files to make sure that everything looks like what we want to push up to GitHub.

So it looks good. And let's write our commit message. I'm just going to say footer. And then I'm going to click the commit to
main button. And then push to origin. All right, well, congrats on finishing up the basic version of the website.

Next up, I'm going to show you how you can deploy the website so that you can load it via the internet instead of, you know, just running it locally.
