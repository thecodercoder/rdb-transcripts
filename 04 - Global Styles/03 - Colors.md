# Colors

Now that we've taken a look at the design, let's start adding our global styles, starting with colors. I'm going to go through and save the colors as CSS custom properties.

We'll start by getting the default background color, which is white. So if I click on the "Desktop - 1440" frame, in the right sidebar, if you scroll down to the "Fill" panel, it tells us that the fill for the entire frame, which is basically the background color, is white, which in hex code is FFFFFF.

In the right sidebar, Figma will display the colors in hex format, but if you click the color swatch to pop up the color picker, you can change the color format with the dropdown here.

We want to use HSL or "Hue Saturation Lightness" colors in the course, so if you select HSL in the dropdown, then it will display the Hue, Saturation, and Lightness numbers, as well as the opacity or what's called "Alpha" as that last number which is a percentage.

However, since the individual HSL numbers are split out and you can't copy the whole thing to paste in VS Code, I think it might be faster to go back to Hex, and then you can copy those 6 digits, and convert it in VS Code itself.

Let me show you what I mean. I'm going to copy the hex color, then let's go to VS Code, and go to our colors, which are stored in the colors.scss file. You can find it in the Solution Explorer in `scss/globals/_colors.scss`.

Let's add this white color to the the `:root` selector where we already have some CSS custom properties for colors from the demo website. I'm going to delete them since we don't need them anymore for our new website.

Now in the `:root` selector I'm going to create a new custom prop called `--main-bg`, and paste in the hex color from Figma. And we need to add a hashtag or pound symbol in front of the 6 digits for it to be valid hex code.

Now a color swatch has appeared, and we can click it to make a color picker appear in VS Code. And now we can change the color format by clicking the title bar, and the first option is HSL, so let's do that, and save.

Let's go back to the design to grab the text colors as well. We have a dark gray text when it's on a white background, and then white text when the background is a solid darker color.

If we select the white text in the Hero, we can see that it's the same `FFFFFF` white as the background color. So we can reuse that white color in VS Code. Let's first select some of that dark gray color-- I'm going to zoom in on the headline in one of the 3-column features, and in the "Fill" panel we can copy that hex code.

Now, in VS Code, I'll create a `--text-dark` custom property and set it to that dark gray. Paste in the color, and add a pound in front of it, and click the color swatch and then in the pop-up, click the title bar once to change to HSL.

Next, let's create a new custom prop called `--text-light` and I'll copy and paste the `main-bg` white color, and paste it in `text-light`.

It might seem like unnecessary work to create 2 custom properties with the same white color value.

For example, we could create a `color-white` variable and use it for both the background color and the light text. And it might work at first, but if the website gets redesigned and only the text color changes but not the background color, we'd have to go through all our styles where we used the `color-white` prop name, and manually change it to the new text color.

Instead, here we are using separate custom properties from the start for each of the different place where the color is going to be used. That way, if the light text color ever changes, we can change the `text-light` color value here, and it will immediately affect all our styles where we loaded this variable. And it won't affect the background color since they are kept separately.

Alright, let's get some more colors from our design. Next, I'm going to get the purple color for the hero background. So let's double-click in the background area, copy the color, and then in VS Code, let's create a new custom prop for it called `--hero-bg`.

Then we'll do the same thing of pasting the color, adding the pound symbol, clicking the color swatch, and clicking the title to change it to HSL.

Back in Figma, let's also grab those colors for the buttons. For these, a common naming is "primary" and "secondary" buttons. So I'll copy the teal background color in the "Free Trial" button and then in our colors create a custom prop called `--button-primary-bg.`

And we also want to get the button text color, so I'll select that in Figma, copy that, and create a custom prop called `--button-primary-text`.

The secondary button for "Pricing" has a transparent background, so in VS Code I'm going to create another custom prop called `--button-secondary-bg` and set it to `transparent` which is a special keyword that browsers use, that maps to black with 0% opacity. I just use `transparent` because it's a bit quicker.

This secondary button is also different in that it has a white border instead of a solid color background. The border and text are the same color, white, so in VS Code let's create a custom property called `--button-secondary-border` and then `--button-secondary-text` and for both we'll once again copy the white HSL color and paste it in for both of those.

In Figma, the next color we'll need to grab is in the Full width Feature section which has the magenta background. So let's double-click into the "background" layer, and copy the color. Then in our code I'll create a custom property called `--fullwidth-bg` and paste in the color, then convert it to HSL.

Hey all! Future Coder Coder here. As I mentioned in the Intro to this course, Figma changed their UI while I was in the middle of recording this course.They moved the "Inspect" tab out of Design Mode which is what we're using, and into a new Dev Mode, which they plan to eventually make a paid product.

Since I don't want to use the paid version of Figma in the course, I had to cut out the last part of this video where I show you how to get the linear-gradient colors in the Full-Width CTA section from the Inspect tab.

But don't worry, I'm going to show you how to get the linear-gradient colors from Design Mode later on in this course when we build the Full-width CTA section.

In the meantime, please ignore any parts of the course where you see the `cta-desktop` and `cta-mobile` linear-gradient colors in VS Code, as that is leftover from the old Figma.

And again, I'll be showing you how to do this later on, in the Full-Width CTA section of the course. I apologize for any confusion.

So, that's it for the colors, and let's get on with the next section, wrapper styles!
