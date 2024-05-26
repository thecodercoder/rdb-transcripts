# Hover states

Let's talk about hover states.

When you're working with links and things that are clickable, it's generally considered a good user experience to change their styles when you hover over them, in order to signify that they are links.

We can do this by adding a "hover" pseudo-class to our selectors for the top nav links.

Let's start with the logo. We usually want to add the hover pseudo-class on the anchor tag itself, because links are what you are hovering over. So for the logo that would be the `topnav__homelink` class.

Inside the `topnav__homelink` selector, we can add the hover pseudo-class by writing a `&:hover` selector. Pseudo-classes are selectors that indicate some kind of changed state, and they are always written with a single colon and then the name of the pseudo-class. "Hover" is one of the most commonly used ones, but there are many others.

Then in the curly brackets, we want to write our changed styles when you hover over the homelink.

One common hover state style is to reduce the opacity a little bit on hover, so it looks semi-transparent. We can do this by adding the `opacity` property and then setting it to a number less than 1.

The number 1 means it's 100% opaque, so totally solid and not transparent at all. If we wanted 50% transparency we would set it to 0.5. That might be a bit too transparent and not readable, so let's set it to 0.8 so it's 80% opaque or solid.

Now if we save and check out the website, if we hover over the logo, it gets semi-transparent. That might be a bit too much, so let's debug this in the browser and figure out what we want the opacity to be.

One really helpful feature when you're working on hover states is that you can force the browser to display different pseudo-classes like hover. In the inspector, I'm going to make sure the `topnav__homelink` anchor tag is selected in the source code panel-- NOT the `topnav__logo` image tag. It has to be the anchor link.

Then in the "Rules" panel, at the top to the right of the "Filter Styles" there's a little icon that says ":hov". If you click that the browser will display checkboxes for different states that you can force.

Let's click the ":hover" checkbox, and now the opacity has been reduced, and we can see in the "Rules" panel the `topnav__homelink` now has the "hover" pseudo-class added to the selector, and we can see the opacity property set to 0.8.

I'm going to increase this a bit to 0.9, so it will be 90% opaque. And if we toggle the "hover" checkbox, we can see how it changes. I think 0.9 looks ok, so let's go back in the code and change opacity to 0.9. And when we save and reload the website, we can hover over the logo and it will change to the hover state style.

Ok! The last thing in the desktop navigation that we're going to work on is the hover state for the text links. First, let's check what selector we need to use for the text links.

If you want to try this yourself, you can pause the video here to figure out what class we want to target in our styles, and add the hover state pseudo-class to the correct selector in the `topnav.scss` file.

Alright. So if we inspect one of the text links, the anchor tag has the class `topnav__link`. So in VS Code, in the topnav.scss file, we'll be adding the hover state to the `&__link` selector.

So under the styles we already have in `topnav__link`, we'll want to add an "ampersand colon hover" and then curly brackets to contain the hover style rules.

What I want to do is add a bottom border when you hover over the links. In the :hover pseudo-class I'll add `text-decoration: underline`.

Now in the website when we hover over a link, a white underline appears. It's white even though we didn't specify a color, because by default the underline will be the same color as the text color, which is set to white.

Let's force that hover state on the text links by making sure one of the `topnav__link` items is selected in the source coe panel, then clicking the ":hov" icon and then checking the ":hover" checkbox underneath. And now it should have that white border displayed.

By default the text-decoration underline will be 1px of thickness. We can customize the look of the underline a bit with some additional properties. For example, if I want to make the underline thicker I can add `text-decoration-thickness` and then set a size, like 2px.

I can also change the color of the underline with `text-decoration-color` and then add a color value.

Another cool part of using CSS custom properties for our colors is that they will get loaded in the browser and we can use them when debugging. If I start writing `var(--`, once I start writing the two dashes, you'll see the options for the different custom properties that we created pop up.

If I press the down arrow we can navigate through all the options from our CSS styles. I'll choose `--button-primary-bg` and press "Enter", and now the underline is the teal color. We might want a bit more contrast, so let's change it back to white. I'll select the text-decoration-color and retype `var(--` and then select `--text-light`.

One more thing we can customize is the position of the underline itself. I'd like to move it down a bit so there's a little space between the text and the underline.

We can do this with `text-underline-offset` and set it to 4px, so it will be moved down a bit from the link text. Looks pretty good! I'm going to copy the additional styles we added starting with `text-decoration-thickness` and paste them in our code.

And when we save and reload the website, we have our underlines happening on hover.
