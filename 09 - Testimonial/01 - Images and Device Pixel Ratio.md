# Images and Device Pixel Ratio

Alright, now we're going to build the Testimonial section. So as always, let's check out the design and figure out what our approach is going to be.

I'm going to have both desktop and mobile versions visible-- and they look pretty similar. In terms of layout, the teal quotation mark and quote text look the same on both, they're just bigger on desktop. Then the author photo and description are next to each other on desktop, and then stacked and centered on mobile. And the description text looks like it's just slightly smaller on mobile.

In terms of layout, we'd want to use either flexbox or grid for at least the author section, to change between the side-by-side and stacked versions. And I would probably just use margins to add space above and below the quote text.

First off, let's export the images, starting with the quotation mark image. I'm going to select the "quotation-mark-teal" layer, and then in the right sidebar click on the "Export" panel and select "SVG" and then the "Export" button. And then in our file explorer I'll copy the file and paste it in our image folder.

For the author photo, we don't want to export the images in the actual website mockup because they're only 120px wide, and not large enough for actual website use. But if you go to the right of the mobile design, there are 1x, 2x, and 3x versions of the author image.

In the real world, you would normally get the images externally from the client or your team member-- they wouldn't be part of the design file. But for this course, this was the easiest way to give you the images you need.

You might be wondering why there are 3 different images for the author in Figma. To explain that, I'm going to go on a slight detour to talk about Device Pixel Ratio, or DPR. When you're working with raster images like JPGs or PNGs, you need to keep in mind the DPR, or Device Pixel Ratio, that your users may be using.

In websites, there are 2 types of pixels that we're mainly concerned with. One is the CSS pixel-- this is how big we size things with CSS, for example, setting a JPG image to be 300 pixels wide. However, there's another type of pixel, and that's the actual, physical pixels that make up a screen.

Initially, the standard Device Pixel Ratio was 1 device pixel to 1 CSS pixel, meaning that the 300 pixel wide JPG would be displayed with 300 pixels on computer screens. However, Apple began making Retina screens with a higher pixel density, so that the width of 1 CSS pixel would be displayed on devices with 2 device pixels. This would give the device a DPR of 2.

As an example, I found a really old article from 2012 on The Verge, when Retina screens first came out. In the article they have this side-by-side comparison of a zoomed in look of a non-Retina display versus a Retina display. You can see how the pixels literally are bigger on the non-Retina screen, and how the smaller pixels on the Retina display make the image seem smoother and less pixelated.

The idea behind this was to create screens where the physical device pixels were smaller than the human eye could detect, making the images on the display look more crisp and high quality.

However, in order for images to look good on these high pixel density screens, we need to load images that are double the size. If we want a JPG image that is 300 pixels wide on the website, we'd need a JPG image file that is 600 pixels wide. If we don't have that, then on Retina screens, the resulting image would look slightly blurry and low resolution.

Nowadays, most mobile devices have a DPR of at least 2, and some newer ones have a DPR of 3 or even 4. You can actually see this in the Firefox dev tools. If I go to our website and load the Responsive Design Mode, and select the iPhone 11, it tells us that the DPR of this is 3. The iPad has a DPR of 2, and the Samsung Galaxy S10 has a DPR of 4.

If you want to support the highest pixel densities, you'll need bigger images, and the downside is that you'll have larger file sizes, creating more load on the website (and the mobile data plans of your users). But do you really need to have 4x images?

To be honest, at the moment, there don't seem to be any concrete guidelines. From what I can tell and have read, while you can easily see the difference between a 1x and 2x image on a high pixel density screen, it's harder to notice the difference between 2x and 3x images, and so on.

In addition, from what I've seen on Apple's website and other websites, most places seem to just use 2x sized images if anything. So you could go with having 2x sized images everywhere on your website and that would be fine for most cases.

However, in this section, I'm going to teach you how to load the author image with the option of 2x and 3x image versions for devices that have a DPR of 2 or 3. And then there will be a fallback image at 1x.

But first, let's go ahead and export the author images from Figma. Since the frames are all just images, we should be able to select the frames and export them together. I'm going to click the frame "author-1x", hold down Shift, and select the "author-2x" and "author-3x" frames. And if we check the left sidebar, we can see that we've selected all the frames.

Then in the right sidebar in the "Export" panel, we want to export these as JPGs and at 1x. The images are already sized, so we want to export them at those sizes. If we selected 2x in the dropdown, Figma would scale up the images to double the size we have in the design, and since they're JPGs, they would end up looking pixelated, which we don't want. So we'll export them at 1x, and hit the "Export 3 layers" button.

Now Figma has downloaded the three images in a zip file, so in our File Explorer I'm going to open the zip file, copy the files, and paste them out in the Downloads folder.

Also, I just like to minify JPG image files, so in Firefox I'm going to open a new tab and go to TinyPNG.com. And then drag the author images there, just to see how much we can save.

And it looks like we can save a pretty significant amount of file size, so I'll click the "Download all" button and download the minified images in a zip file. Then I'll go into the zip file and again, copy the images, and go to our project image folder and paste them in.
