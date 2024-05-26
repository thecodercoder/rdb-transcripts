# Quote text styles

Next up is the quote text styles. Going into Figma, let's start with the mobile styles, and select the quote text. It's the same font-family that we've been using, Source Sans Pro, and it's bold and font-size is 24px. The line-height is 30px, and in our calculator if we divide 30 by 24 we get a line-height of 1.25.

Then in the desktop version, we have a font-size of 36, and line-height of 45. If we divide 45 by 36 it's also 1.25. And the other font-styles are the same. The color is the dark gray that we have as our default text color.

Let's go to our styles, and I'm going to go to the index.html file and check what selector we need to use. The blockquote tag has a class of `testimonial__quote`, so going into our testimonial styles, we'll be using the `quote` selector.

I think I'm going to use the Fluid Typography Calculator to generate the font-size, so let's add the other styles. I'll add the `line-height: 1.25`, and then the text is bold, so I'll add `font-weight: 700`. And now let's get our font-sizes.

Let's plug in those numbers. I need to refer back to the design-- the mobile font-size is 24 and the desktop font-size is 36. So I'll set the `Min Font Size` to 24px, and the `Max Font Size` to 36px.

And now we'll copy the Result, and go back to VS Code and paste it in at the top of the `quote` styles. I'm going to round the decimals to 2 places to 1.16rem and 1.45rem. And now let's save, and check out the website. And the text looks good-- in the rules we can see our clamp() function for the font-size, and in the `Computed` tab I'm going to filter for `font-size` and we can see it's 36px for desktop. And when we slide over the dev tools panel it decreases until we hit 24px for mobile widths.

Next, we need to add space under the quote text before the author photo. Going to the design, it looks like we have 40px of space on desktop, and on mobile we also have 40px. That makes things easier since it's always going to be the same. Going back to our styles, I'm going to add `margin-block-end` and set it to `u.rem(40)`. And now on our website we have that space under the quote text.

Now, let's look at the author info. The author photo is 120px wide and tall, and it is a circle.

I think we're good with just having the width set, and the height set to `auto` so that the full image will be displayed and it won't have to be constrained to a square. Let's refresh to get back to our saved styles.

The next thing we wanted to do is to make the author photo a circle. We can actually accomplish this with the `border-radius` property. With border-radius, you can set it to a static length like 1rem. But to make a circle you want to set it to half the width or height, since we have a square image. And the easiest way I've found is to set it to 50%. And an added benefit is that if we change the image styles to be a different size than 120px, it will still be a circle-- assuming the image is a square. With a rectangular image, it would be an oval instead.

So, let's add the `border-radius: 50%` rule to our styles. I'll go to VS Code, add `border-radius: 50%` to the `author-image`, and then when we go back to the website, the photo is a circle. Looks good!

The last element in the Testimonial section is the author info. In the design, let's see what font styles we'll need to add. In the desktop design, the font-size is 24px, and the line-height is 31px, which, if we get the calculator, is 31 divided by 24, which is around 1.3 line-height. Then on mobile, we have a font-size of 20px, and a line-height of 26px. And if we divide 26 by 20 we get also 1.3.

Ok, so the font-size is 20px on mobile and 24px on desktop. I know we made some global paragraph styles earlier, so let's see if the author info will match any of those. In VS Code, the paragraph styles are in the globals/typography.scss file. And if we check out the paragraph tag selector, we have the `medium` class. If we look at the clamp() function, the minimum font-size which is what will be used for mobile, is 20px, and the maximum font-size, which is what desktop will use, is 24px. And all paragraphs have a line-height of 1.3. So we should be able to use these styles by adding the `medium` class to the paragraph tag.

Going to the index.html file, the author info is in the `figcaption` tag we created. And we didn't add a paragraph tag in the figcaption, but I think it's ok to add one nested in the `figcaption`. And then I'll take the text and move it into the paragraph tag. And so that the styles get added to the paragraph too, I'll cut that whole class from the figcaption and paste it in the paragraph tag. I think all the styles we need will be in the `medium` class, so let's add that to the paragraph tag. But I'll leave the `testimonial__author-description` class there for now, just in case we do need to add some Testimonial-specific styles to the description.

And let's save, and on the website we now have our author info styles. Let's inspect the paragraph, and it looks like it has a bottom margin, which we don't want because it will offset when we try to vertically center it with the author photo. So I'm going to go back to our styles, and in the testimonial.scss file, in that `author-description` class selector, I'll add `margin-block-end: 0`. So it's good that we kept that paragraph selector.

Now let's save, and back on the website, the paragraph doesn't have a bottom margin anymore.

Ok, now that we have the styles set up for the Testimonial class elements, let's work on the responsive layout for the author photo and info. Looking at the design, on desktop we have the author photo on the left and the author info on the right, and they are vertically centered. And on mobile, we have them stacked to 1 column, with the author photo on top and the author text under it. And both are horizontally centered.
