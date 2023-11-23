# Adding the favicon

In this video, I'll show you how to set up a favicon for your website. Favicons are those little icons for a website that you see in your browser tab, or if you save a website to your mobile phone home page. In order to get a favicon to load for your website, you need to save the image file in your website root, and also add some code in your index.html head to link to it.

Favicons can be kinda tricky. The problem is that you can't just have one favicon image and call it a day. All the different browsers and devices available have different preferred image formats and sizes. And trying to keep up with all the different versions you need can be very time-consuming.

Fortunately, there is a pretty good solution that will provide you with all the different images and the code for your index.html file that you will need. I did some research on favicons, and it seemed like a lot of people recommend using a website called RealFaviconGenerator.net. So that's what I'll be showing you how to use.

If you go to the site, it will prompt you to upload an image file. This image needs be a square image and be at least 260 pixels wide and tall. I've included the favicon for our website in the Figma design. So if you go into Figma, there is a frame on the far right called "Favicon." And we want to export that favicon image. So select the image, then in the right sidebar go down to the "Exports" panel and click to export it as a PNG and at 1x size.

Then, on the Real Favicon Generator site click that "Select your Favicon image" button and select that PNG. After a few seconds, it will show you what the favicon will look like on different browsers and devices. You can leave the image as is, or you can slightly customize how the image looks, so feel free to play around with some of these options. Once you're done with any customizations, scroll down to the bottom and click the "Generate your Favicons and HTML code" button.

It might take several seconds to finish, but when it's complete you can click to download the "Favicon package" to get all the image files, and there's a code snippet that you can copy and paste in your HTML head.

First let's get the files. The Real Favicon Generator site will have given you a ZIP file. Unzip the file and copy all the image files from the zip and paste it directly into your project folder in the root directory.

Then let's go back to the Favicon Generator site and copy that code snippet. Then in your VS Code, open up the index.html file and paste the code in the <head> of your HTML. I don't think it matters a ton where in the head you put the favicon code, but I'm going to paste it right after the title tag, before the Google Fonts tags.

Now, when you load your local website, you should be able to see that favicon load in your browser tab!

Up next, we'll be starting to write our global styles for the website in our Sass files.
