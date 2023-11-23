# Figma design

Alright, so now, you've gone through the videos on how to set up all the tools you'll need for the course, and the Sass and Responsive Design intro. In the rest of this course, I'll show you how to build out the course website from a custom Figma design.

And we're going to start by getting familiar with Figma. In this video I'm going to show you how to get the design loaded in your Figma account and how to look at the design to get the style information to put into your code.

And just a disclaimer, I am by no means a Figma expert-- I'm only showing you some of the basics of how to look at Figma designs as a web developer. There are a lot more advanced features of Figma that I'm not going to be covering here, just because they're more for people using Figma to create website designs.

First off, if you haven't already, you should download the Figma file, called "BASIC - Responsive Design Beginners.fig" from the course page.

Once you have the file, you'll need to log into Figma at Figma.com. If you don't have an account there yet, you can sign up for free.

Once you're logged into Figma, you should see a dashboard. What we want to do now is import the Figma file that you just downloaded. On the dashboard, there should be a button that says "Import file."

Click that button, and then select the Figma file. A window saying "Import files" should pop up with the progress. When the import is done, click the "Done" button. And you should now see the Figma file on your dashboard. Double-click it to open the design.

In the Figma design, in the left sidebar, there's a list of several artboards or what Figma calls "frames." There's one for desktop which is sized at 1440 pixels, one for mobile at 375 pixels, a Favicon image, and then some author images.

You might be wondering why there's no tablet design, only desktop and mobile. And the reason for that is that I very very rarely have ever gotten a tablet design. Most designers will create just desktop and mobile versions.

So sometimes developers have to make design decisions and figure out how the content should look on tablet. And of course, if you're at a job, you can always ask your designer if you're not sure about how things should look at a specific viewport. Usually I'll have the tablet view be some kind of hybrid between the desktop and mobile styles.

Let's dig into the design and I'll show you how to find the style rules for each element and how to export image files. First, let's take a look in the left sidebar at the Desktop frame. You can tell that it's a frame in Figma because of the hashtag symbol next to it. If we expand it, it will show you all the groups of layers that are in this frame. I've tried to keep the layers as organized as possible so that everything is grouped in a way that makes sense.

To navigate through the design, with your cursor in the main middle panel, you can use the scroll wheel to go up and down. Also, if you hold down spacebar the cursor should change into a hand and you can then move your mouse to navigate around that way as well.

You can also zoom in and out. To zoom in, hold down Ctrl (or Command for Macs) and use the scroll wheel to zoom in or out.

In Figma they actually store some of the styles as CSS rules that we can use to put into our Sass files. For example if I click on the hero Figma will open the "Hero" group, then if I double-click again on the blue background it will select the "hero-background" layer. Then we can get info about the layer in the right sidebar.

In the "Design" tab we can see the size of the layer, which is [XXX] wide and [XXX] tall. And it's telling us the fill color which we can use as the background-color in our code.

Let's click on the color swatch in the Fill panel. This opens up a color picker and we can get the hex color, and you can click the dropdown to change color formats to HSL or other formats.

If we close out of the color picker, another cool feature is that if you click the "Inspect" tab, Figma has some CSS code for that element. I wouldn't just copy and paste all of these rules because some of them will be very different from how we'll build the website, and they may not work for responsive styles. But it can be helpful for some things like background colors.

One thing to note when you're clicking on shapes is that if you double-click one too many times you might see the shape covered with these diagonal lines, and the square dots that are in the border turn into circle nodes. This is a feature that allows you to adjust the shape itself by moving the nodes around.

You can see this if I keep double-clicking on the unicorn image, eventually we get to the shape, and we have the circle nodes and diagonal lines. And if I click and drag one of the circle nodes, it actually changes the shape itself.

We don't want to do this, but if you accidentally move things around, you can undo by pressing Ctrl-Z.

If you get in this mode with the circle nodes, you can get out of it by double-clicking somewhere else on the design, and you'll see the circle nodes turn back into squares. You can also press Escape to do the same thing.

Just wanted to mention that, since it's something that happened to me a lot and it will likely happen to you also.

Next up, let's look at some text elements. Let's select the headline by double-clicking the text until just that headline is selected, then in the right sidebar make sure you're in the Design tab. And if we scroll down a bit we can see info in the "Text" panel. So this is telling us the font family, the font weight, font size, line height, letter spacing, and the text alignment.

Below the "Text" panel there is a "Fill" panel with the fill color, which will be the text color since this is a text layer. Again, if we go to the "Inspect" tab, we can see the CSS style rules there. And that's pretty much it for looking at text elements.

Let's also check out the buttons that we have. I'm going to zoom in on that "Free Trial" button and select it. You notice that the buttons have rounded corners. In the "Design" tab for this button, the roundedness is set in the "Group" panel with a setting called "corner radius" and a pixel number. This corresponds to the CSS property "border-radius". Not sure why the names are different, but maybe "corner radius" is used more in the design world.

This button is also a good opportunity to show you how to find the distance between two elements in the design, which is a feature I use a ton. In the button if I select the "Free Trial" text inside the button, then hold down Alt, it will tell me the distance between the text and whatever other element I hover over. This is really helpful in this case to know what to set the padding as in the button. So here there's a top and bottom padding of [XXX], and a left and right padding of [XXX].

And if I select the full "Free Trial" button and hold down Alt, if I hover over the "Pricing" button, it will tell me the distance between the two buttons.

If I zoom out a bit and select the subheadline text, if I hold down Alt and hover over a neighboring element, like the headline, I can see the distance between the headline and the subheadline, and then if I hover over the buttons, the it will tell me the distance between the subheadline and the buttons. This measuring feature is super helpful and I use it a lot to determine the spacing between elements.

And, in that same vein of spacing, Figma lets you use Layout grids to make sure the design aligns with a grid. If I select the Desktop frame in the left sidebar, then in the right sidebar in the Design tab, there is a panel called "Layout grid." I can toggle to hide or show it by clicking the eye icon.

I'm going to make the 12 columns grid visible, and you can see the 12 columns in light blue in the desktop design now. If you click the icon on the left, the 3 vertical lines, you can adjust the number of columns, the color and opacity, and how wide they are.

Seeing the grid helps a lot when figuring out how big to make things. For example, in the hero the text on the left side takes up the 6 columns on the left, and the unicorn image takes up 5 columns on the right. So the way I set up this design is all 12 columns take up 1200px on desktop, so the container size that will limit the width of the content is 1200px. I also created a "1 column" layout grid which just has that 1200px width set in the lines.

The last thing I want to mention is how to export the images from the design to image files. One example is the unicorn image, which should be an SVG since it's an illustration and has all solid colors-- SVGs are vector images which means they can size up without losing quality. If we select the whole illustration, then in the right sidebar at the bottom there is an Export panel, and you can choose the file type and the resolution you want to export it as. For this I'd change it to SVG and then click the "Export unicorn" button.

Most of the images in the design are going to be SVGs since they're illustrations and it'll save on file size to store them as SVGs. But for other images, like in the Testimonial section, the circle author image, that should be exported as a JPG because JPGs are better for more photographic images that have lots of image detail, instead of flat shapes.

Alright, so that's a quick overview of the main functions that we'll be using in Figma in this course! Don't worry if you don't remember everything I just said, because as we build out this website and go back and forth in Figma, I will show you everything step by step so you can follow along.

Up next, we're going to do a couple of prep things, and then start actually building our website!
