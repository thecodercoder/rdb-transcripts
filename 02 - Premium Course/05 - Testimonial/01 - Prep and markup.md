## Markup and positioning

Alright, so in this section we're going to be making some tweaks to the existing Testimonial section. If we look at the website, on desktop, what we have is the quotation mark image, then the quote text, and then the author photo and description. And on mobile, it's pretty much the same, except the author info is now centered.

Going to Figma now, on mobile the design looks the same, so there are no changes for that. Then on desktop, the quote text and author info looks the same, but there are now two quotation marks. The original one at the beginning, and then a new one at the end.

If I select just the quote text and hold down Alt, the opening quotation mark, instead of being right above the quote text, is now positioned to the left by 40px, and slightly above it, by 30px.

And the closing quotation mark is positioned 40px to the right and 30px below the quote text block. And the author info is 40px below the quote text-- which, if we go to the website and inspect the quote text and go to the Layout tab, it has a bottom margin of 40px. So nothing about the quote text or author info is changing. We're going to just be working with the quotation marks and positioning them.

When I look at this design, what's the best way to position the quotation marks? We could try using CSS grid like we did in the Hero section to position that hero wave image at the bottom of the section.

However if we did, we'd have to create the grid on the parent element, figure out the grid column sizes, and place each individual child-- the quotation marks, quote text, and author info-- in the correct cell. Which is possible, but I think it may be more complicated than it needs to be.

I think that using position absolute on the quotation marks would be a simpler way of achieving the layout, because we can just write styles to affect the quotation marks, and we won't have to do too much different to the quote text and author info.

The first thing we need to do is create the second quotation mark in our markup. So in VS Code, let's go to the index.html file, and in the Testimonial section take a look at the markup we have so far.

Right now, we have a figure tag, and it is containing the first quotation mark image, then the blockquote with the quote text, and then the author info. I'm going to select the quotation mark image tag, copy it, and since the first image is right before the blockquote tag, I'll paste the second one right after the blockquote tag.

So now on our website, we have the two quotation mark images. If I inspect one of them, let's check out the styles that they have. They both have a class of "testimonial\_\_icon", and then in the styles we're setting the width, with a max-width, and then a margin-block-end adding space between the image and the quote text.

I think we will keep all these styles for now, and we can tweak later on if need be. Let's start positioning the quotation mark images. In VS Code, let's open the testimonial styles. In the Quick Open menu, I'll type in "testimonial" and select the Sass file.

Again, the styles for the images are in the "testimonial\_\_icon" selector. Let's add a desktop media query so we don't affect any mobile styles. I'm going to add "@include u.breakpoint(large)" and in it, write "position: absolute".

Now when I save, you can see the quote text and the rest of the content on the page moved up. This is because making the quotation mark images position absolute took them out of the normal flow of the document, meaning that they are no longer taking up space on the page, and the rest of the normal content moves up to fill the space.

However, if I inspect one of them, and in the browser I toggle the "position: absolute" rule, you can kinda see that the first quotation mark isn't actually moving-- it stays in the same position that it would have been in originally, but it's just not taking up any space.

The same thing is happening with the second quotation mark-- it is moving up only because of the first quotation mark getting taken out of the flow, but it's not moving up into the quote text, and the author info is now overlapping it as if it wasn't there.

This is what happens just by adding "position: absolute" to both images. This is our starting point, and we're going to further position each quotation mark, using some of the CSS positioning properties of "top", "right", "bottom", and "left", starting with the first quotation mark.
