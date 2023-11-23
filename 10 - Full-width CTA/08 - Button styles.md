# Button styles

The last thing we need to do for the Full-width CTA section is style the button.

On the website, let's inspect it in Firefox. We initially copied the `Free Trial` button markup from the hero section, so it's currently getting all its styles from the `button` class and the `button primary` class.

But if we go to the design, The `Free Trial` button in the Full-width CTA section is solid white, with the default dark gray text color. Since this is a new button style, we'll have to figure out how we want to set that up.

Let's go to VS Code and take a look at our button styles. They are stored in the scss/globals/button.scss file. As a quick refresher, the `button` class contains the styles that we want all buttons to have-- mainly size and font-size.

Then the additional button classes, `primary` and `secondary`, set the background and text color of the buttons, as well as their hover state colors. The primary button on the hero is the solid teal, and the secondary hero button has a transparent background and a white border.

The Full-width CTA button is similar to the primary button styles-- both have a solid background color and no border, and have the dark gray button text. So what I might do is create another helper class inside the `primary` class and set the white background color on there.

In the `primary` class under the hover state selector, I'll add a new class, `ampersand dot white`. The ampersand is so the final selector for this button will target an element with both the `primary` and `white` class names, as well as the `button` class.

Without the ampersand, the selector will be `primary space white` which would target an element with the class `white` that is a child of another element with class `primary`. That wouldn't work since we're putting both class names in the button.

In the `white` class, we need to set the background-color. For the other button styles, we set the colors as custom properties in the globals/colors.scss file, so we should do the same thing for this one. Let's open that colors.scss file, and create some new custom properties under the `--button-primary` custom props.

We don't need to worry about the text color, since it can use the `button-primary-text` color, but we will need to set the background and the background hover colors. So I'm going to select the `button-primary-bg` and `button-primary-bg-hover` custom properties and press Ctrl-D to duplicate them.

Then in the duplicated properties, I'll add `white` to their names so we have `button-primary-white-bg` and `button-primary-white-bg-hover`.

Then we'll need to set the HSL colors. We can copy the `main-bg` HSL color, which is white, then I'm going to paste it for both the white button color properties.

The default background color is white, but we also want the hover background color to be different. Let's go back to the colors.scss file and see what we did for the teal primary button. So the default teal background color is in `button-primary-bg` and the hover background color is `button-primary-bg-hover` and it is slightly darker. We can tell because the last number, which is the L in HSL, controls lightness. The default teal has 42% lightness, and the hover color has 37% lightness, so it's 5% darker.

Let's do this for the `button-primary-white-bg-hover`. I'm going to reduce it by 5% and see how that looks. (see if it looks good, otherwise make darker with 90%)

Now let's go back to the button.scss file, and in the `white` class, I'm going to copy the background-color rule from the `primary` styles, and paste it in there. And I'll also copy the entire hover state selector, and paste it in as well. Then I'll add `white` to the custom property names to use the new custom props we just created.

Now, we've set up the white button styles, so we need to add the `white` helper class name to the button in our HTML. So for the `fw-cta__button` I'll add it to the end of the class names. And let's save, and check out the website.

And now we have a white button! And when we hover over it, the background darkens slightly due to the reduced opacity so that it's semi-transparent. So that looks pretty good.
