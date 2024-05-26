## Layout styles

Now that we have the basic styles for the text and images set, let's start working on the layout styles. Looking at the design, on mobile things are all stacked to 1 column, and the image is centered. Then on desktop, we have 2 columns with alternating order. First the image is on the right, then in the next row it's on the left, and then right again in the last row.

Let's start by figuring out if we want to use flexbox or grid for the desktop layout. I'm going to turn on the Layout Grid in Figma and zoom in a bit. It looks like the images are different widths-- the first one is 401px, then the next one is smaller, at 352px. And the last image is even smaller at 242px.

And the text elements are also different widths. We have 695px, then 746px, and 860px. And they are taking up different numbers of columns in that 12-column layout grid that we have.

Lastly, if we check the space between the image and text, it looks like there's 100px of space between them on all 3 rows.

The different sizes of image and text elements on each row tells me that this layout would be better to build with flexbox. The content isn't adhering to a strict size of columns for the image and then the text. The sizes are changing between rows, and the only thing that stays consistent is that 100px of space.

We just want to fit the image and text on one row, with 100px of space between them. Flexbox is better when you just want to fit the content in a row like this. I'm going to turn off the Layout Grid. And we'll start by building the mobile layout in 1 column with flexbox.

Looking at the website and the markup, each row is in the "alt-feature\_\_row" div, and the direct children are the image tag and the "alt-feature\_\_text" div. So we can make the flexbox parent the "alt-feature\_\_row" div.

I'm also going to turn on Responsive Design Mode and load the iPhone view since we're doing mobile styles first. In VS Code I'll go to the alt-feature.scss file, and in the "row" selector I'll add "display: flex" and then "flex-direction: column" to put the text under the image.

Let's save and see how that looks. Looks pretty good, we will need to add space under the image, probably with gap. And that last image looks really big. So let's check out the design to get the space, and see what other image styles we need to add.

In the mobile design, if I select one of the images and hold down Alt, there's about 40px of space under it. So let's go back to our styles and add that with "gap". So in the "alt-feature\_\_row" selector, and I'll use pixels since it doesn't need to scale up with the browser base font size.

And going back to Figma, let's look at the image sizes. The first one is 200px, the second one is also 200px, and the last image is also 200px. Going back to our styles, for the "alt-feature\_\_image" maybe for mobile we can add a "max-width: u.rem(200)" and we do want rems so they scale up.

And then we'll add a media query breakpoint, and move the "max-width: 100%" inside it. So now, on our website, we have the space between image and text, and the images are all 200px.

And let's also center the content on mobile. Since the main axis is vertical with our "flex-direction: column", to center left to right, we'll need to use "align-items: center" instead of "justify-content: center" like we normally do.

And now when we save everything is centered!

One other thing is that I think we need more space between the text of the previous row, and the image of the row after it.

[ right-click inspect the space between image and text of a row ]

So if I inspect one of the rows, and then hover over the elements inside it in the markup view, it looks like the space is only coming from the paragraph. And since we don't have an explicit style, it's coming from the browser default.

Having a margin-bottom on the paragraph will throw off the vertical centering when we go to the 2-column layout on desktop. On Figma, if the paragraph has space under it, that's part of the paragraph, so it will kind of push the text up when it's centering, so it will look a bit off.

We don't want that to happen, so I think the easiest way to get rid of this is to cancel it out for the Alternating Features section. In the alt-feature.scss file, in the "alt-feature\_\_text" selector I'm just going to add a nested paragraph selector, and in it set "margin-block-end: 0". So now the space is gone.

We do need to add space between the rows, and that's something we want for both mobile and desktop. Let's look at the design, and on mobile if we select one row, we have 60px between the rows. Then on desktop, there's 80px of space between the rows.

We need to figure out how to add that space. If I inspect one of the "alt-feature\_\_row" elements, we could, just in the browser, try adding space under each row with "margin-block-end: 60px" for mobile. And it does work, however the problem with this is that the last row also has that 60px of bottom margin, which will create too much space between sections. You can use a ":last-child" pseudo-class, like if I click the "plus" icon to add a new "alt-feature\_\_row" selector, and add ":last-child" and in it set "margin-block-end: 0", then it will remove that margin just for the last row.

It's kind of annoying to have to cancel out styles, so I might not use that and refresh to reset the styles. And instead, I can make the whole wrapper div for the Alternating Features section be a grid parent, so each row would be a grid child. Just in the browser, on the wrapper div, I can add "display: grid" which will put each grid child on its own row, which is what we want. And then set gap to 60px.

So now if I turn on the grid highlighting, we can see the 60px of gap between the rows, but not after the last row. I like this a little better, but to make it work I'll need to add a section-specific class to the wrapper div.

In the index.html file, in the wrapper div I'll add a new class, "alt-feature\_\_wrapper". And then in our styles I'll add a new selector at the top for "&\_\_wrapper" and in it we'll write "display: grid" and "gap: 60px".

And the website looks good. And since we know we want the gap to be 80px on desktop, let's do that now while we're here. I'll create a new breakpoint mixin for large, and set "gap: 80px". And on the website if we select Laptop, and inspect, we have that gap of 80px. And obviously it looks weird right now, we'll get to the desktop layout in a little bit.

Going back to iPhone view, things look pretty good! So I think we can move on to the desktop layout now. I'm going to turn off Responsive Design Mode.

To put the image and text on the same row, in our styles for the "alt-feature\_\_row" class selector, I'm going to add a breakpoint for large, and in it we'll change "flex-direction" to "row". Looking pretty good!

Let's now add that space between the image and text with the "gap" property. In the design it was 100px of space. Let's start with that, so in our breakpoint I'll also add "gap: 100px". And I do want to check how things look as the viewport decreases especially for tablet widths, and see if the space looks ok, or if it ends up being too big.

In the browser, I'll use Responsive Design Mode and let's select iPad. And right now we're still loading mobile styles for iPad. I'm going to drag that right edge out to increase the viewport width. And right when we break to that 2-column layout, it looks okay, not terrible. But I might want to change the gap property to a percentage just so it will decrease as the viewport width decreases.

Let's switch to a Laptop device, and I'm going to try to see what percentage we should use. We know the wrapper is 1200px max-width on desktop, so 100px is less than 10%, maybe 8%. In the browser under the gap of 100px, I'll add a test style of "gap: 8%". And it's a tiny bit smaller than 100px but I think it's close enough.

Now, let's set the viewport width to 1250px to be right at that mark. And reduce the viewport width. And you can see the gap is slightly decreasing. Right at 900px is where the 2-column layout is the narrowest. And that looks okay. Just to compare, I'll uncheck that "gap: 8%" rule so we can see that there's a decent amount of difference between 8% and 100px at this width.

I think that looks good. In our styles I'm going to change the 100px to 8%. Okay, so we're all set for the spacing. Now let's go back to a desktop view, and get the alternating part working.
