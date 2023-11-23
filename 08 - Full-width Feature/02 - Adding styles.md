# Add styles

Now let's start adding the styles. Going back to VS Code, we need to create a new Sass partial file for this section. I think we will create it in the `scss/components` folder since it's a new component, meaning a section of the website that could standalone as a distinct part of the website, like the Hero section and the 3-column Features section.

In the `components` folder I'll create a new file and call it `_fw-feature.scss`, so the name of the file matches the name of the block class name that we created in our index.html file. And since we created a new Sass partial, we need to go into the `components/index.scss` file and write `@forward 'fw-feature'`.

Now let's go to `fw-feature.scss` and first thing we want to do is import our util module with the `use` at-rule. If you don't remember how to do that, there's no problem-- we can just see what we've done previously and copy that over. So we can go to the features.scss file, and up at the top, we can copy that `use` at-rule and then go back to the fw-feature.scss file and paste it in.

After we have that, we want to add the block selector, which is the class name we added for this section and are using in the file name too. So we'll add `.fw-feature` and use curly brackets to make the selector.

Next, I'm going to add selectors for all the classnames for the BEM elements that we used in our HTML markup. Let's check that out in index.html. We got `fw-feature__wrapper`, then `title`, `description`, and `image` as the elements. Then back in our Sass file inside our block selector I'll nest the element selectors. The first one, `fw-feature__wrapper`, I'll write `&__wrapper`. Then under that I'll do the same thing for `&__title`, then `&__description`, and last, `&__image`.

Let's start adding our styles. Let's look at our website, and then look at the design and see what we want to add first. When I compare what we have with the design, the first things that stick out to me are the magenta background color for the section, and making the text white. Let's check our color CSS custom properties to see if we added the magenta color yet or not.

Our colors are stored in the `globals/colors.scss` file. Looking at our custom props, I'm looking for a magenta color swatch. And we have a custom property name, `fullwidth-bg` which sounds like the section we're working on, and the color does look magenta. Let's just double-check that the HSL value is correct to what the design has. It's 320, 85%, 41%, and then 1 for the alpha or opacity set to 100% which is the default. So we just need to look for 320, 85, 41.

In our design I'm going to click on the background image, and double-click until I see in the right sidebar the color pop up somewhere. Ok now we are in the `background` layer and in the right sidebar there's a `Fill` panel with the magenta color swatch. Figma displays colors in hex format by default, but we can se the HSL value if we click the color swatch, and then in the pop-up make sure the color format has `HSL` selected. And now we can see the HSL numbers. It's 320, 85, 41, 100% which looks like what we have in our CSS custom props!

Going back into our code, I'm going to copy that `--fullwidth-bg` custom prop name, and then going back to our fw-feature.scss file, I want to add it to our styles. Now, where do we need to add the background-color rule? If you're not sure, let's check the index.html file and we want to add it on probably the `fw-feature` section tag. In our styles, under the `fw-feature` class block selector, I'll add `background-color` and then load the custom prop with the var() function and paste in `--fullwidth-bg`. Let's save and see what that looks like.

And the background color is now loading. And, again, we want to add the background color to the main section tag, and not the `wrapper` div, because the `wrapper` div has that max-width of 1200px so the text and image content doesn't get too wide. If you're curious what that looks like, if we copy that background-color rule from the section tag, uncheck it, and then go to the `fw-feature__wrapper` div and paste it in the element styles, you can see that there's extra white space on the left and right sides.

Ok, let's reload to refresh the styles. Looking at the website, we also need to make the text color white. Let's check and see where the current gray text color is being set. If I inspect the text, and look through the styles, we can see that the body selector has the `color` property set to `var(--text-dark)`. In order to override that, we can set the white color on the class of the `fw-feature` block.

A class selector has a higher specificity than the tag or element selector, and thus will override it. And, even if they were the same specificity, the Sass files in the components folder will get loaded after the global styles, so due to the cascade in CSS, later styles of the same specificity will override earlier styles.

Going into our styles, and the colors.scss file, we probably want to use the `--text-light` custom prop, since that's what we're using it for. I'll copy the `--text-light` and then back in our fw-feature styles in the block `fw-feature` class I'll add the `color` property and set it to `--text-light`. And now when we save, the headline and paragraph text are white!

Next up, let's center the text and the image in the section. In the same `fw-feature` selector I'll add a new rule saying `text-align: center`. And looking at the website, the text is centered but the image is not. `Text-align: center` will only work on inline or inline-block elements, and since we set all images to be `display: block`, we will have to center it the same way we did with the Features icons on mobile, by setting `margin-inline` to `auto`. In our Sass file in the `fw-feature__image` selector, I'll add `margin-inline: auto`.

Now, looking at the website, the next thing we should do is make sure the headline and paragraph text are the right size, and have the right amount of space underneath them. Let's start from the top with the h2 text. In the design, the headline is 48px, and on mobile it's 36px.

On the website, if we inspect the headline, the font-size is being set with the clamp function, so let's go to the `Computed` tab and filter by `font-size` to see the final pixel size. And it says 48px when we're at a desktop viewport width, and if we go down to a mobile size it decreases until it hits a minimum of 36px. So we should be good! And the font-weight is bold or 700, since we already set that in our typography styles.

Let's also check the line-height. In the desktop design, the headline line-height is 52.8, so I'm going to get the calculator and put in 52.8 and divide it by the font-size, 48. And the result is 1.1. Let's also check the mobile design. The line-height for the headline there is 40, and that divided by the font-size 36 is about 1.1.

In our website, if I inspect the h2 tag, there's no line-height style, so it's currently going to be taking the default browser line-height. So let's add the 1.1 to our styles for the h2 tag. The h-tag styles are in the globals/typography.scss file. And if we look there, the h2 tag does not have a line-height set yet. So I'm going to add `line-height: 1.1` there.

Let's now check the space under the h2 tag. If I inspect it in the browser, it looks like there's a bottom margin, but there's no `margin-bottom` or `margin-block-end` rule in the styles. This means that the margin is coming from the browser defaults. Let's go to the design to see what that space is supposed to be.

In the desktop design, if I select the headline and hold down Alt, there's 20px of space under it. And on mobile if I do the same thing it's also 20px of space. Going back to the typography.scss file, in the h2 tag selector, I'll add a new rule of `margin-block-end: u.rem(20)` and save. And then on the website let's check that the rule is getting applied.

If I inspect the h2 tag, I see the margin-block-end of 1.25rem, and it's interesting because it looks like Sass combined the h1 and h2 tags since they have the same amount of margin-block-end. If I click the `typography.scss` link we can see the original SCSS file, and yeah, it looks like both h1 and h2 have `margin-block-end` of `u.rem(20)`. So that's cool that it combines them for you. And then on the `Layout` tab it tells us that the calculated bottom margin is indeed 20px.
