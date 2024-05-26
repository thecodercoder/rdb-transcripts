# Button styles

Now let's start building the buttons. To start, let's go to Figma and see what we have in the design. We have a teal primary button and then a clear white border secondary button. And if we compare mobile and desktop, it looks like the buttons are the same size on both versions, so we can just have one set of styles for all viewports.

Now, let's figure out how we want to write the styles for the buttons. We could use the BEM format using modifiers like `hero__button--teal` and `hero__button--clear`. But if we go down the page, there's another button, a solid white button in the full width CTA section.

And we can assume that buttons might be used elsewhere in the website, in other sections of this homepage, and if there were multiple pages to this website. So for the buttons I think I'm going to use some helper classes that will let them be reused throughout the website more easily.

Let's go into VS Code and start writing the styles for the buttons. I think I'm going to put the button styles in the scss/globals folder. I could also put it in the components folder, but I think for our purposes, `components` should be styles that are limited to one section, like we have with the top nav and the hero section styles.

Since buttons will exist in multiple sections of the website, I'd like to keep them in the global styles. So in the globals folder let's create a new Sass partial, `_button.scss` and then in the globals index.scss file we'll forward the button partial.

In the button.scss file, let's first load the util styles and add `@use '../util' as u` at-rule to the top. And then I'm going to add a `button` class selector, where we'll add shared styles that all the buttons share. So let's go to the design and take a closer look at the button styles.

If we select the text in one of the buttons, it tells us that the font-family is `Source Sans Pro,` which is the font we're already using, so the button will inherit that style from the the body, and we don't need to create a new rule for that. Then the font-weight is `Bold` which is 700, font-size is 18px, and the line-height is also 18px so the line-height will be 1.

Let's add those to our styles. First I'll add `font-size` and set it to `u.rem(18)`. Then we'll add `line-height: 1`. And then to make it bold we'll add `font-weight: 700`.

Now let's go back to Figma and get some more styles. Next to the line-height, there's a 5% Letter spacing, which is the same letter spacing as the Top Nav text links had.

Again, we can't use percentage for letter-spacing in CSS, but we can use the relative unit `em` which when we use it for letter-spacing will be relative to the font-size. Since 1em will be 100% of the font-size, 5% of the font-size is 0.05em, which we can also see in the `Inspect` tab, in the CSS rules section. So going to our styles, we can add `letter-spacing: 0.05em`.

Going back to Figma, another thing we need to style is making the button text all caps. We can achieve that with `text-transform: uppercase`.

Next up, since we have the button text styles, let's figure out how to size the buttons. Usually, what I like to do is to not give the button a set height or width, but instead use padding to add the space around the button text.

This will allow each button's width to be determined by how long the button text is. And the buttons will all be the same height since they will have the same font-size and padding.

I'm going to select some button text. Then if we hold down Alt and hover just outside the button text but still in the button, we can see there's 12px of padding on the top and bottom, and 16px of padding on left and right.

Let's add those padding styles to our `button` class too. In our code I'll add `padding: u.rem(12) u.rem(16)`, which will add 12px of padding to the top and bottom, and 16px of padding to the left and right. And I am using our rem() function for this so the buttons will maintain their padding if the base font size changes and not look too weird.

Next, let's see how rounded the corners of the buttons are. If we select one of the buttons, under the height, it tells us that the corner radius is 24px. I think `corner radius` is the design term-- in CSS the property is `border-radius`. So back in our styles we can add `border-radius: u.rem(24)`. And like the button padding, I'm going to use rems for the border-radius so that the rounded corners also maintain the same roundness if the base font size goes up.

Ok, so we now have the text and size styles that all the buttons will be sharing. Now, let's add styles for the different button colors. These will also be helper classes, and I'm going to put them all inside the `button` class selector, so that they'll only take effect when the element also has a class of `button`.

The first one will be the primary button, which is that teal color. I'll create a new class selector called `&.primary` -- the reason that it needs the ampersand is so that the final selector in the CSS will be `.button.primary` which means it will look for an element that has both classes set.

Otherwise, if I didn't add the ampersand, the selector would be `.button .primary` with a space between, which would look for an element of class `button` that has a child element of class `primary` which isn't what we want to use.

In this `primary` class, we'll need to set the background-color and the text color. Looking back in the design, the background-color is teal, and the text color is a dark gray. And I believe we already added CSS custom properties for the button colors. So let's grab those colors from the colors Sass file.

The teal background color will be `--button-primary-bg`, so I'll copy that, and then in the button.scss file I'll add `background-color` and set it to `var()` and paste in the color name. And then going back to the colors, the text color should be `--button-primary-text` so I'll copy that and set the `color` property to that.

Now, let's start testing our button styles by adding the classes we need to the first button link. Back in the index.html file, in the first anchor link for the `Free Trial` button, let's add the class names `button primary`. And save, and let's see how this looks on the website. It looks pretty good!
