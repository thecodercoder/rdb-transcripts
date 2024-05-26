## Second quotation mark

Now let's work on the second quotation mark. First, let's figure out what selector we need to use for this one. You might think that since we did "first-child" for the first quotation mark, we should be able to use "last-child" for the second one, since it's the last "testimonial\_\_icon" element in the section.

In our styles, under the "first-child" pseudo-class I'll add a new selector, "ampersand colon last-child" and in it I'll add a test style of "outline: 2px solid red".

Unfortunately, when we save, nothing happens. And if we inspect the second quotation mark, our selector and style rule aren't there. And this is because like I mentioned in the previous section, the first-, last- or nth-child selectors work by first finding the child element of the group of sibling selectors that matches the order number, and then seeing if it matches the class or other selectors you have in the styles.

So in this group of sibling selectors that are children of the figure tag, the last child is the "testimonial\_\_author-wrapper" div. And since that doesn't have the "testimonial\_\_icon" class, the style isn't getting applied.

But, we can use the "nth-child" selector to target the second "testimonial\_\_icon". This might a bit tricky, especially if you haven't worked with these child pseudo-class selectors, but based on what you know so far, why don't you pause the video and try to figure out how to target that second "testimonial\_\_icon" in the styles.

[ pause ]

Alright! To use the "nth-child" selector, we need to figure out what order the element we want to target is in. In the figure tag, if I count, it is the 1, 2, 3 -- the third child in the figure tag. So to target that, let's go to our styles, and instead of "last-child" I'm going to change that to "nth-child()" and in the parentheses type in "3".

And now it has the red outline from our styles. One thing to keep in mind, in a lot of programming we start counting from 0. But in this case, we start counting from 1. So it can be slightly confusing, but I try to think about it like "first-child" means 1, second child means "2", third means "3" and so on.

Let's go back to the design to figure out where we need to position this quotation mark. If I select the quote text, and hold down Alt, the second quotation mark is 40px to the right and 30px below the text. So very similar spacing wise from the first quotation mark, just in a different direction.

Back in our styles, just to make things easier to see, I'm going to add an outline to the quote text too. So in the "&\_\_quote" selector I'll add "outline: 2px solid blue".

Now, for the quotation mark, the first thing we'll want to do is turn it upside-down. We can do this with the "rotate" property, and turn it 180 degrees with "180deg".

Now, let's align it horizontally. We want to first get it all the way to the right side. We could set "right: 0", and now the right edge of the quotation mark is lined up with the right edge of the quote text. However, another thing you could do is instead of the "right" property, use "left" and set it to 100%.

This moves the quotation mark farther over, because with the "left" property, we're positioning the left edge of the quotation mark, and the 100% means we're moving it 100% of the width of the parent, the figure tag, away from the left side. Meaning it's moving to the right.

And this is kinda nice because since it's lined up, horizontally we only need to move it 40px more to the right. So in the "left" property, we can use calc() again, and then set it to "calc(100% + 40px)".

Now we need to position it vertically. Since we haven't set any "top" or "bottom", right now the quotation mark is positioned vertically in the same place it would have been if it wasn't position absolute, but it was in the normal flow of the document.

What I mean by this is that if I inspect the quote text and hover over the markup, you can see it has a bottom margin pushing down the quotation mark. And in the "Layout" we can see that the margin is 40px. And for the quote text, if I set "margin: 0" to remove it, you can see that the quotation mark, as well as the author info moves up.

I would like to move the quotation mark up so that its bottom edge lines up with the bottom edge of the quote text. Then we can move it down 30px.

But how should we do this? We actually can't use the "bottom" property because that will align it relative to the parent, which is the figure tag, which includes everything, including the author info.

I think the best option is to use "translate" to move the quotation mark up. In the browser, let's try setting "translate" to "0" because we don't want to move it horizontally, and then "-40px". So now it's aligned with the bottom edge.

And I want to move it up the height of the quotation mark image, so we can do that by adding to the "translate" value. We can subtract 100% from our -40px to do that. So I'll add "calc()" and in it it'll be "calc(-40px - 100%)".

And now the bottom edges are lined up, so we can move it down 30px to match the design. So in the calc() function, I'll make it less negative by 30px, to move it down 30px.

Alright, that looks pretty good! So let's remove the outlines from the styles. And we are pretty set with the desktop styles.
