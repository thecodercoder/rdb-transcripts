# Quotation Mark Styles

I'm just going to start from the top with the quotation mark image, and we can work our way down the section. Looking in the design, the quotation mark image is a little bigger on desktop than it is on mobile. On desktop it is 78 pixels wide, and on mobile it is 52 pixels.

There are a couple of ways we can handle the size. One way would be to set the width to 52px for mobile, add a media query, and then change the width to 78px.

We could also use the Fluid Typography Calculator and instead of font-size we'd input the width numbers for mobile and desktop, and then copy the output and set the width to that.

And one other way that I can think of that might be a little simpler is to use a relative unit, percentage, as the width. If we go to the design, we have the 52 pixel width for mobile. And as a refresher, the percentage unit is based on the parent's width. So for mobile, the parent will be wrapper div, which has 24 pixels of space on either side. And for the mobile viewport width of 375px, we can use our calculator and divide 52 by 375 to get around 0.16 or 16%.

So we can set the width to 16%, and let's see how that looks.

And let's save, and on the website we can see our new style rule, and let's monitor the width in the "Layout" tab, and see how it changes between desktop and mobile. On mobile it is [XXX], and if we increase the viewport width it grows and on desktop widths it's definitely bigger than the 78px from the design.

So we can control that if we go back into our styles and set a max-width of `u.rem(78)`. And now if we save and go back to the website, it is 78px on desktop, and as we decrease the viewport width the image shrinks until on mobile widths we're back to [XXX].

And we didn't need any media queries which is kinda nice. I do want to mention that I wouldn't do this for font sizing, because percentage won't be affected by the browser base font size. But since this is an icon image and it's fairly big so I think it should be recognizable and I think we can get away with using percentage for it.

If you do want to make the size get bigger if the browser base font size goes up, you can use the Fluid Typography Calculator to get the width sizes, or use media queries and set the width in rems for mobile and desktop.

Alright! Next, we need to add space under the quotation mark image. Going back to the design, on desktop we have 40px of space under the image, and on mobile it's 20px.

Again, you can use media queries to change the width and margin instead of what we did here with `clamp()`. It's really just a matter of your own preference and if you like the fluid change instead of the sudden change when you hit that breakpoint.

Ok, so that should be it for now for the quotation mark styles.
