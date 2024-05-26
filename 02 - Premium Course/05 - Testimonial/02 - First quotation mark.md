## First quotation mark

When working with absolutely positioned elements, you need to make sure that the parent element that you want to position the child element relative to, is set to something other than the default of "position: static".

Let me show you why. Just in the browser, if I go to the first quotation mark image, and add "top: 0", it totally disappears! Where is it? If I right-click the element and select "Scroll into view", we can see that it's at the very top of the website.

This is happening because absolutely positioned elements are, like we mentioned, not in the normal flow of the document like the rest of the website content.

If you don't add the other positioning properties like top, right, bottom, or left, then the image will just kind of float in the same position it would have been without position absolute. However, if we start adding those properties, the browser needs to know what parent element to use as kind of the position anchor.

It's going to look at the parent element, which in our case is the "figure" tag, and see if it's position is explicitly set to something other than "static". If I select the "figure" tag, it doesn't have its position set. So the browser will go up to the grandparent element, in our case the "wrapper" div. This one also doesn't have a set position.

And if doesn't find one, it's going to keep going up the tree all the way until it hits the initial containing block, which is what contains the viewport. If we change "top: 0" to "bottom: 0", the quotation mark actually moves to the bottom of the viewport.

Obviously we don't want the quotation mark to move up this much, so we need to set "position" on one of the parent elements in the Testimonial section. So let's reload and go back down to that section.

In our markup view, the parent element of both quotation marks is the "figure" tag. So let's go into our styles, and I'm not going to add a class to the figure tag, but I'm just going to add a tag selector before the "&\_\_icon" and in there let's set "position: relative".

And now on the first quotation mark, I'l try setting "top: 0", and nothing happens, because it is already positioned at the top of the element. And if we change it to "bottom: 0", it moves down to the bottom of the bounds of the figure tag. And if I hover over the quotation mark image, notice that the margin-block-end that we have on it is offsetting that bottom position, so it's pushed up a bit.

If I remove the "bottom" property, we're back to where we want to start positioning the first quotation mark image. Let's position it horizontally first, it needs to be 40px to the left of the quote text. I'll add "left" because we want to position it relative to the left edge of the parent. Right now it's at "left: 0", meaning 0 pixels from the left edge. If I increase it to 10px, it's 10px from the left edge, so it is moving to the right.

To position it to the left of the left edge, we need to go into the negative numbers. Let's try setting it to "-40px". Now it is left of the left edge, but it's not nearly far enough. This is because you need to also take into consideration the size of the absolutely positioned element.

We're positioning the quotation mark horizontally right now, so we need to also consider its width, which is 78 pixels. What we could do is add 78 to 40 to get 118px. And set the "left" property to "-118px". And that looks to be the right distance.

The only problem with this approach is that if the image changes size, either because of responsive styles or if the image itself gets redesigned and changes in the future, it could throw off this number.

One trick I use when I have to position things like this is to take advantage of the "translate" property. Let's reload the website to refresh and go back to the saved styles.

And the first quotation mark is back to having just "position: absolute". Just in the browser, let's add "translate". The translate property lets you set up to 3 numbers to move an element horizontally on x-axis, vertically on the y-axis, or even through 3d space on the z-axis. Usually you'll just be using the x and y axis for most websites.

Similar to top / right / bottom /left, you can use a length unit like pixels. However, if you use a percentage for the "translate" value, it will be a percentage relative to the element itself. In the past when we've used percentages like for example the "testimonial\_\_icon" has a width set to 15%, which in that case means 15% of the parent's width.

But for translate, the percentages are in relation to element. So if I set "translate" to negative 100%, it's going to move to the left because of the negative number, and 100% of the quotation mark's width. This is super handy because it puts the quotation mark right outside the left edge of the figure tag, without needing to put in the explicit width in pixels.

And now, we can set "left" to be "-40px" so that it's 40px away from the quote text. And if you wanted to control the horizontal positioning only in translate, let's uncheck the "left" property. And set "translate" to be "calc(-100% - 40px)". We need the CSS calc() function because we're doing math and subtracting 2 values together, so you need to put them in the calc() function in order to do that.

In this case, I like using the combined calc() with just the "translate" property, so we don't need the "left" property. And it's still reasonably clear what you're doing-- you're moving it 100% and 40px to the left. So let's copy this style rule, and add it in our Testimonial styles.

Now, we need to figure out how to target only the first "testimonial\_\_icon". One way that would work is to target the ":first-child" pseudo-class, because, if we look at the index.html file, the first "testimonial\_\_icon" is the first child in the figure tag.

In our styles, we can nest it inside the "testimonial\_\_icon" class selector, and because this is only going to be for desktop we can actually put it also in our existing large breakpoint.

So in there I'll add "ampersand colon first-child"-- and it does need to be a single colon. And then paste in our "translate" style rule. And when we save, it is 40px to the left of the quote text.

Now, we need to position it vertically. According to the design, it's supposed to be 30px above the top edge of the figure tag quote text. There's two ways that I think you can achieve this, either using the "top" property or adding to the "translate" property. If you want to try this for yourself, pause the video now, and then unpause when you want to see how I do it.

Okay! So, if we wanted to move it 30px up, we can set "top" of negative 30 pixels. Because if we don't set "top" the element will automatically position itself at the top edge of the figure tag, which is the same position as "top: 0" gives you. It's zero pixels down from the top of the parent's top edge. So to keep moving it above the top edge we need to make the number negative and move it 30px, so -30px.

And that looks good. But, if you wanted to just use the "translate" property and not "top", you can add a second number to the translate value. So after the "calc(-100% - 40px)", we can add a space and then write "-30px". This does the same thing as "top: -30px" because with pixels it's that absolute pixel value, it's not a percentage.

I'm going to keep using just the translate property, so let's go back to our styles, and in "translate" I'll do the same thing, add a space and "-30px". So when we save, the first quotation mark looks good!
