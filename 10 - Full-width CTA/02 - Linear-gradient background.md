# Linear-gradient background

We haven't added any styles yet, but let's take a look at the website to see where we're at right now. It's pretty blank-- we have the headline and paragraph global styles working, we have our button sized but just not in the right color, the content isn't centered, and we don't have the gradient background yet.

Since making a gradient is something we haven't done yet in this website, let's work on that first.

So how do gradients work? Let's first look at the desktop gradient in Figma. If we double-click on the background, in the right sidebar under the "Fill" panel, we can see that it says the fill color, looks like a gradient. And it says "Linear."

If we click on that color swatch, a pop-up menu appears and we can see that it also says "Linear," and we can see the 3 colors that make up the gradient. A linear gradient is one that progresses along a straight line, hence the name. And you can make that line horizontal, vertical, or angled.

In our case, Figma displays the line in the actual section on the design, and it is horizontal, going from left to right. We can also see that it's made up of 3 colors, a dark blue gray, then blue purple, and lastly a bright teal or aqua color.

If we click on one of the color squares in the pop-up menu, Figma tells us the color in Hex code, or you can choose another color format.

Along with the colors that make up the gradient, we can control where each color starts along the gradient, which is called the "color-stop." In CSS, you can set those color-stop points by using a percentage. For example, the starting point of the gradient would be by default at 0% and the ending point would be by default at 100%.

Right now, our gradient begins on the far left side with the dark gray at the starting point, of 0%. Then it changes to the blue color, which has a "color-stop" point at a little over 50%, and then it changes to teal at the ending point, somewhere greater than 100%, since the teal is positioned past the right side of the section.

Unfortunately, Figma in Design Mode won't tell you the position of each color stop-- that's something that you can get from Dev Mode-- but we can eyeball them and get pretty close.

Now let's look at the mobile gradient to see how it compares to desktop. If we double-click the Mobile background layer, and click on the "Fill" color swatch, it looks like the mobile gradient is made up of the same 3 colors and the angle of the gradient progression is also horizontal, but the positions are a bit different.

It still starts with the dark gray on the left at 0%, but the blue is more past the 50% mark, probably 75% or so. And then the teal color is way past the right edge of the section, probably 130% or so.

Let's start coding the gradient. First I want to get those 3 colors and save them to CSS custom properties, and then we'll add the style rules for both desktop and mobile gradients.

Let's copy that first gray color. It's #383A4A which I think is the same as the gray text color, but just to be sure let's copy that hex code. Then, let's go to VS Code, and load the scss/globals/colors.scss file.

I'm going to create a new property for this gradient color, so at the bottom, let's make a new line and I'm going to call it `--gradient1` and then paste in the hex code, and put a hashtag or pound symbol in front of it.

Now, let's convert the color to HSL, I'm going to hover over the color swatch, and then when the pop-up appears, click on the title bar and it should change to HSL as the next option. Let's save that, and go back to Figma for the next color.

In the color picker I'm going to click on the blue color, and copy that hex code. Then in VS Code I have the cursor on the `gradient1` color and I'll duplicate the line by pressing Ctrl-D. And rename the color to `gradient2` and then I'll paste the color in, add the hashtag, and then convert it to HSL too.

Ok, let's get the last color from Figma, copy it, and in VS Code we'll duplicate `gradient2,` rename it to `gradient3`, and paste in the hex code. And convert this to HSL.

And now we have our 3 gradient colors! Next, we can start creating the gradient style. If you're not familiar with CSS gradients, let's go to Firefox and search for `css linear gradient.` And the first result should be MDN, so let's go there.

Linear gradients are images that you can create with CSS. So here in the examples, they are all set on the `background` shorthand property, using a function called `linear-gradient.` Since they're images, they are technically getting set on the `background-image` property. I just mention this because if you try setting it on a different background property like `background-color,` the gradient won't load. So it has to be set either on `background-image` or the shorthand `background` property.

Looking at the first example, in the linear-gradient() function, the only parameters it has is two colors, separated by a comma. There's no direction and no positioning of the colors. By default, the linear gradient will be vertical, going from the top down. So the first color is the pink color, and the second color is the purple color.

And if you don't explicitly set the color-stop points, with two colors the browser will default to the first color at 0%, at the top, and the second color will be at 100%, at the bottom. You can have more than 2 colors, and if you do, they will by default be evenly spaced across the background unless you explicitly set the color-stops.

Clicking to the next example, this one has 3 colors, and the first parameter which says `0.25turn` sets the angle of the gradient direction.

You can think of the direction like hands on an analog clock, where a 0 turn will go from bottom to top, like in the 12 o'clock direction. Then `0.25 turn` is one quarter of a full turn. You can also use `degrees` when setting the angle, so this would be 90 degrees to the right. Then `0.5 turn` would be half of a full turn, which you can also say is 180 degrees.

You can do a lot more complex things with gradients, but for our purposes, let's try making our linear gradient in our styles.

In VS Code, looking at the index.html file, we want to set the background on the section tag, similar to how we've set the background color for the Hero and the Full-width Feature sections previously.

So in our styles, that would be on the `fw-cta` class selector. Let's add the `background` shorthand property, and then set it to the `linear-gradient()` function. Then in the function let's start by adding the 3 colors that we need.

Going to our colors.scss file, the gradient colors are `gradient1`, `gradient2`, and `gradient3`. I'm going to copy `--gradient1`, and in the fw-cta.scss file, in the linear-gradient() function, I'll write `var()` and in the var() function paste in `--gradient1`.

Now, let's copy the `var(--gradient1)` function, and after it, add a comma, then paste it, add another comma, and paste it again. And we need to change the second gradient1 to say `gradient2`, and make the last one say `gradient3`.

Now let's save, and on our website, we can see a gradient as the background. Let's make the text color white to match the design. In our styles, in the same `fw-cta` selector, I'll add `color` and set it to white, which we've saved as a custom prop, `var(--text-light)`.

Ok, now it's looking a bit closer. However, the gradient is going vertical, from top to bottom. So we need to make it horizontal, by adding a first parameter in the linear-gradient() function.

There are multiple ways you can do this. One way is by using keywords for direction. We can write `to right` and then add a comma after-- and when we save now the gradient starts on the left and progresses to the right side.

We can also write it using the `turn` unit, like we saw in the MDN examples, so going from left to right you could write `0.25turn`. Or you can use degrees, and write `90deg`. Any of those will work. I'm going to keep it on degrees because I find that easiest to think about.

Now, we need to figure out the color-stops, starting with the mobile version. I'm going to use Responsive Design Mode and select the iPhone. And then let's go to Figma, and look at the mobile gradient.

We can see that the website has all 3 colors equally spaced, from the dark gray on the left, to blue in the middle, and teal on the right side. But in the design, the blue is almost to the far right side, and the teal is beyond the 100% mark, so the blue is just starting to get a little lighter on the right side.

Let's try to tweak the gradient to match the design by adding color-stops. For the blue color, I'm going to guess that it starts somewhere around the 75% mark. Let's add that in our code.

In our styles, we want to add that 75% for the second color since that's the blue. We can leave the first color alone since it's going to start at 0% by default which is what we want.

After loading the `gradient2` custom property, before the comma, let's add a space and then `75%`, and see what happens. When we save, the blue is now extending more towards the right side, so we're getting there.

We do need to add the color-stop for the teal color too. Let's go back to Figma. Ok, so the teal color is way past the right edge of the section, maybe half the width of the section itself, around 150% or so. Let's try that for the color-stop. In VS Code, after the `gradient3` color I'll add `150%`.

And when we save and check out the website, it looks closer to the design! If we put them side by side, the gradients are very close.

Now let's try to get the desktop gradient. I'm going to select `Laptop` in Responsive Design Mode, and zoom out until we can see pretty much the whole thing.

And in Figma, let's also zoom out on the desktop view so we can see the whole section. This one, the blue color-stop is just slightly past 50%, and the teal color is a bit past the 100% mark. Basically everything is shifted slightly to the left to be inside the visible section, compared with the mobile version.

In our styles, let's add a media query with a desktop breakpoint to change the linear-gradient() for desktop. So I'll write `@include u.breakpoint()` and set it to `large`. Then in the curly brackets I'm going to copy and paste the mobile `background` style rule.

Now we can change the color-stops for desktop. For the second color, which is the blue, let's change it from 75% to be 55%. And then, looking back at Figma, the teal color is maybe at 110%. Let's try that, save, and see how the website looks.

Cool, so now we can see more of that teal on the right side of the website. Looking at the design, I think that looks pretty close. We can always tweak the color-stops later on if need be, but I think this is a great starting point for the linear-gradient background.
