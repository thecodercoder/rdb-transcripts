# Button hover state

Next, we need to figure out what the hover states for the buttons are. Since hover states aren't a feature that you need on mobile, Firefox won't show any hover states when you're emulating a mobile device. So let's close out of `Responsive Design Mode` to go back to a desktop display.

Just like the top navigation links, we want the buttons to change in appearance when you hover over them to let you know that they are clickable elements.

I didn't include button hover state styles in the design, but we can follow some common design choices for hover states.

For the teal `Free Trial` button, let's take the initial teal background color and make it darker. Since we saved the original background color as a CSS custom property, we'll also save the hover color as another custom prop.

Going to VS Code, in the colors.scss file, I'm going to find that custom prop, `button-primary-bg` and I'll press Ctrl-D to duplicate that line. Then I'll name the new property `button-primary-bg-hover`. The HSL format allows us to darken and lighten colors without having to use a tool to calculate the HEX colors, which is pretty nice.

Again, HSL is `hue saturation lightness` and then the last number is alpha which means opacity. That means that the 42% number is the lightness, so to darken it we'll decrease that number, let's try by 10, to 32%. And now we have our hover color.

If you want to try this yourself, in the button.scss file, add a `hover` pseudo-class to the `primary` button and in it, change the background-color to this new custom property, so that when you hover over the button on the website, it will change colors.

Ok! First, let's copy that custom prop name `--button-primary-bg-hover`. Then, in the button.scss file, inside the `primary` class selector, I'll add a new selector for the hover state pseudo-class. So `&:hover` -- and we need that ampersand with no space since the hover state is on the primary button itself.

Then in the selector, I'll add a new rule, `background-color: var()` and then paste in the `--button-primary-bg-hover` custom prop. Now let's save and check it out on the website!

Ok, the button color changes, which is great. However it's a bit too dark, and there's not enough contrast between the background-color and the text color, which is affecting the readability of the button.

So let's go back to the colors.scss and reduce the lightness change for that `--button-primary-bg-hover` custom prop. Instead of 32% let's lighten it to like 37% so it's a change of 5% instead of 10%. Now when we save and go back to the website the color change looks better-- it's still changing, but the contrast is enough that the button text is still readable when you hover.

The last thing I'd like to do is to add an animation for the color change so that it smoothly changes from the lighter to the darker color over a short period of time, instead of instantaneously changing.

Since we might want this type of animation for all buttons, let's add the styles for this under the `button` class. To animate the change, we are going to use the CSS `transition` property. This allows us to control how the transition, or change, happens.

The `transition` property is a shorthand property for 4 different transition related properties. The first one is `transition-property`, which is what CSS property you are changing. In our case, we're changing the background-color. So I'll write `background-color` as the first value.

Second is `transition-duration`, which is how long you want the animation to last. I generally start with 250 milliseconds, which you can write as `250ms`, or 0.25 seconds which you can write as `0.25s`. Either is fine-- I'm going to use 250ms.

The third is `transition-timing-function`, which is the acceleration curve of the animation, how fast or slow it begins and ends. This can get pretty complicated, but I generally use `ease-in-out` to have the animation slow slightly at the very beginning and the end. The default value for this is `ease` which is a bit faster at the beginning, and slower at the end. I think either `ease-in-out` or `ease` are perfectly fine options. I'm going to use `ease-in-out`.

If you're curious to learn more about this, search for `Josh Comeau CSS transitions` -- he has an excellent interactive blog post with visual examples of the different options that make it a bit easier to understand.

The last transition property is `transition-delay`, which is an amount of time you want to wait to begin the animation. In our case we don't want a delay because we want the animation to start right when we hover over the button, but it can definitely come in handy in other situations. I'm not going to set anything for this, and it will default to 0 seconds of delay.

Now, let's save this and see what it looks like in our website. And when we hover over the button, it smoothly animates to the darker background-color, which is nice. I might want to make it a bit faster. Let's inspect the button, and in the browser styles tweak the transition time to be 0.2 seconds or 200 milliseconds. Ok, that seems a bit better, so I'm going to change our styles to be `200ms` for the transition duration.

Now let's add the hover state style for the clear white `Pricing` button. I think what I might do is have the background-color change to solid white, and the `Pricing` text change to the purple color of the hero background. So they're kind of flipping colors.

Again, since we're saving all the button colors as custom props, let's go to colors.scss and add new custom properties for the secondary button background color and text colors. I'm going to duplicate the `button-secondary-bg` rule and add a `-hover` to the end. And I'll set the value to white like the secondary border color.

Since the border color is remaining the same, it won't get animated so we don't need to create a new custom property for the border hover color. But the text color will change, so let's duplicate the `button-secondary-text` property and add `-hover` to the end. The color is going to be that purple that we're using in the hero background.

One cool thing you can do with CSS custom properties is use them as values for other custom props. So for the button-secondary-text-hover property, I'm going to set it to `var()` and then copy the `--hero-bg` custom property name and paste it in the var function. This is so that if the hero background color ever changes, we will only have to change the `hero-bg` property, and not the text hover color, since it will be pulling from the hero background custom prop.

If you'd like to try this on your own first, you can pause the video here, and add the hover styles for the `secondary` button, to make it solid white and the text to be purple when you hover over it.

Alright. So let's go to button.scss and in the `secondary` class selector, add a new selector for the hover state, with `&:hover`. Then I'm going to copy the background-color rule from the default secondary class and paste it in, and add `-hover` to the end of the custom prop name, since we added the `hover` to the end of the existing colors. And then for the `color` property, I'll do the same thing so it says `button-secondary-text-hover`.

Now let's save and check it out! Ok, hovering over the `Pricing` button the background color is fading in to white which is good. It looks like the text is kind of blinking almost, like it's faster than the background color animation. And I think this is because we didn't add the `color` property in the transition style rules-- currently we're only transitioning the `background-color` property.

So let's go back to the button.scss file. The shorthand `transition` property does allow you to add values for multiple properties, separated by a comma. I'd like to use the same `transition-duration` and `transition-timing-function` for the color transition, so what I'm going to do is add a comma at the end of the `ease-in-out` value, then add the `color` property and then copy the `200ms ease-in-out` and paste it after `color`.

And now in the website, the `Pricing` button has a smoother transition. And let's see how the `transition` properties look. If we inspect the `Pricing` button and scroll down to see the `transition` properties, there's no error warning, which tells us that we have all our syntax correct. And you can expand the shorthand property to break it out into the different transition properties.

Another thing you can do if you're animating multiple properties but want to use the same duration and timing function for all of them is to use the individual `transition` properties in your styles instead of the shorthand one. This will let you only have to type the shared values once.

Let me show you what I mean in our button styles. So right now we have the shorthand `transition` property. But let's split this out-- first I'll add `transition-property` and set it to `background-color, color` separated by a comma.

Then I'll set the `transition-duration` to 200ms. And the `transition-timing-function` to `ease-in-out`. So for all button animations on the background-color and color, they will use the same duration and timing function, without you having to write them twice like you would when using the shorthand. I feel like this is a bit more efficient, so I'll comment out the shorthand property, but leave it for future reference.

Ok, I think we are pretty set with the button properties. And we've now gotten the styles for the different hero elements set-- the unicorn image sizing, the text, and the buttons. Next up, we're going to get the layouts set up so we have the correct alignment and layout for both mobile and desktop viewports.
