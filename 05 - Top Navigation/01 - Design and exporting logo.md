# Design and exporting logo

In this section we're going to start building out the top navigation of the website! To start off, let's take a look at the design.

For desktop, the navigation has the Mythos logo on the left, and three navigation links on the right. If I think about how I might need to build that, I could use either flexbox or grid to layout the header. And on mobile, the design is pretty much the same, just with the logo smaller and links closer together.

Since the logo is an image, we'll need to export that from Figma first. So in Figma, let's double-click to select the logo. Then in the right sidebar down at the bottom, click the "Export" panel. And in the dropdown, make sure it has "SVG" selected as the file type.

We want an SVG because the image is made up of shapes with a solid color, which is good to export as a vector image like SVG that can scale up infinitely.

Click the "Export" button and Figma should download the image file into wherever your downloads get stored.

We could also export it as a PNG with a transparent background, since the image is a flat illustration style which PNGs are good for. Just keep in mind that PNGs are raster images so they can't be scaled up without becoming pixelated.

JPGs are another type of raster image, but they can't have transparent backgrounds. So I definitely wouldn't use JPGs in this case.

When working with images, one important thing to think about is file size, and seeing which file type gives you a smaller file size. Let's try also exporting the logo as a PNG, and then compare the file sizes of both SVG and PNG to see which one is smaller.

In the "Export" panel, I'll change the option to export as a PNG. And for PNGs and also JPGs, you generally want to export them at at least 2x, which will create larger images that won't look pixelated on retina or other high pixel density displays. I'll get into this concept in more detail later in the course, but for now just make sure to set this to 2x.

Let's go to our file explorer to compare the image files. And it looks like the PNG is half the size of the SVG. And another thing to keep in mind is that with PNGs and JPGs, you can run them through an image compressor tool. I use TinyPNG.com all the time, and it's pretty surprising how much it can compress your files.

Let's go there and then compress the PNG file just to see how small we can get it. And it looks like the compressed version has been reduced by half, just over 1 kilobyte. Both are really small because the logo image is a small image and is pretty simple, with just the white letters and transparent background.

The difference between 1 kilobyte and 5 kilobytes is very minor, so in this case I'm still going to use the SVG because if the design ever changes or we need a larger logo somewhere else, we can use this same file.

If the image files were a lot larger, then it might be better to consider the PNG, since the difference would be bigger.

I'm going to copy the SVG file, and then go into my project folder. I'm going to make a new folder in the root called "img" to store all our images from Figma. And then I'll paste in the file there.

Let's go back to Figma to see if we need to export any other images. And it looks like there aren't any others, so we're all set for images in the top nav.
