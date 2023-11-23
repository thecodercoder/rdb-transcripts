# Adding the styles

Ok, now that we have at least our markup for the first feature, let's start writing our styles. First up we need to create another Sass module. But where do we need to create it? If you want, pause the video, and figure out where you want to create this new Sass partial.

I'm going to create it in the `scss/components` folder, and I'll use a filename that matches the name of the BEM block, `features`. We're calling this `underscore features.scss`, the underscore to indicate that it's a partial file and shouldn't be compiled into its own CSS file, but rather, included with the rest of the styles when our main style.scss file is compiled.

And because it's a new file we need to forward it in the components index.scss file. So I'll add another forward at-rule and just the name of the module, `features` since Sass can locate it without needing the underscore or the `.scss` file extension.

Going back to our features.scss file, the first thing we'll add is the name of the block, `features.` I'll create the class selector for the block. And then let's go back to the index.html file and add selectors for the other elements in the features block. After the `features` block, we have `features__wrapper`, so nested in the `features` class selector I'll add `&__wrapper` and the ampersand standing in for the `features` class.

Then we have the hidden H2, which is visually hidden so we don't need to apply any styles to it. After that is `features__item` so I'll add a `&__item` under the `features__wrapper` selector. Then we have `features__icon` so we can add `&__icon`. And then `features__title` and then last `features__description.`

Now that we have all the selectors we need in our Sass file, let's start writing our styles, starting with the size and spacing for the icon images and the text. Going back to the design, let's take a look at the icon, on both mobile and desktop designs. For the image itself it doesn't seem like we need to add too many styles, since the image tag where we set the width and height will make sure the icon is the right size. So I think we're ok with the icon size for now.

In the mobile design let's check the space under the icon, which I'm going to set with the `margin-block-end` property which is the same as `margin-bottom`. Again, when it comes to spacing between sibling elements, I like to use margin to add space between them. And it looks like we have 10px of space under the icon and before the feature title. And on desktop it's also 10px.

So in our styles in the `features__icon` selector I'll add `margin-block-end: 10px` to add 10px space under the icon. I'm using pixels in this because it's for space under an image, and not having it scale up as the browser base font size scales up won't affect readability of the text elements. But again, you can use rems if you want.

Now let's add styles for the `features__title` element. In Figma, I'm going to check on the font styles, first on mobile. The font-family is `Source Sans Pro,` the font-weight is Bold, the font-size is 24px, the line-height is the same, and the color is #383A4A. On desktop, everything looks the same as mobile: the font-family, font-weight, and font-size and color-- so we'll just have to create one set of styles for this. And, some of those styles should be already set from when we did boilerplate styles, but it can't hurt to double-check that they're all there.

In our browser if I inspect the title text, it looks like the font-family is set to `Source Sans Pro` from our boilerplate styles. The font-weight has been set font-weight to 700 or bold in our typography.scss styles. And we can check the `Computed` tab for the calculated font-size, which is 24px which is correct. It looks like there is no line-height set, so we should add that to our styles.

The h3 styles are in the globals/typography.scss file. So let's go over there, and for the h3 tag we just have the font-size style. Under it I'll add `line-height: 1`. It's `1` because the line-height is the same as the font-size, with both at 24px. So a line-height of 1 means that the line-height is 100% of the font-size. And if we save and go back to the website, we can see that the line-height of 24px is showing up in the `Computed` tab.

Now, the text color looks black, which is not correct-- it's supposed to be a dark gray, so let's see what's happening there. In the `Rules` tab, in the `body` selector, the color is set to the CSS custom property `text-color`, but the name is dark gray, and if I hover over it it says `--text-color is not set`. And if I scroll down to look at the custom props we set in the root element, there is no `text-color` property, but there is `text-dark`. So I think `text-color` is probably from the demo website, and I just forgot to change the name from `text-color` to `text-dark`.

Let's fix that by going to colors.scss which is in our `globals` Sass folder, just confirming one more time that `text-color` doesn't exist. And then I'm going to copy the `text-dark` custom property and going to boilerplate.scss and in the body tag selector replacing `text-color` with `text-dark`.

Also, while we're here, I'm noticing that the body tag also has a `background-color` custom prop called `background-color`. Let's go to the colors.scss file, and looking at the custom properties, it does not exist. We do have one called `main-bg` which is white, and is probably what we want the default background color to be. So I'm going to copy the `main-bg`, go back to the boilerplate.scss file, and paste it in the background-color style rule.

And now when we save and recheck the website, the text looks dark gray instead of black, which is good. However, if I scroll down in the styles to where the custom properties are, I can see that the `text-dark` color has a hex code of `#373949`, which is different from what we had in the design. Let's quickly double-check what we have in Figma-- and it is `#383A4A`. That's a bit strange.

In the inspector, if I hover over the swatch and press Shift-click Firefox will change the color format. And in HSL it says `hsl(233.3, 14.1%, 25.1%)`. But if we go back to Figma, click the color swatch, and in the pop-up make sure that it says `HSL`, it tells us that it is `hsl(233, 14%, 25%)`. And in VS Code, in the colors.scss file, the color in HSLA format matches what we have in Figma. But let's check the compiled CSS file, in the dist folder.

So I'm going to open the style.css file, save to run Prettier to reformat the code, and then search for `text-dark`. And here we can see that the colors are all in hex code. What I think is happening is that in VS Code, even though we set the colors in HSLA, when it compiles to CSS it converts to hex, which is just slightly off from the HSL color. And the compiler is probably rounding slightly differently than how Figma is, causing the discrepancy. But, the difference is really small, and I highly doubt that it would look different when you look at it.

Aright, now that we got the text styles and color all set, let's check the space under the h3 tag. In the design, the title has 10px under it in both desktop and mobile. This again makes our job a bit easier as mobile and desktop use the same styles. So in the `features__title` class selector, I'll add `margin-block-end: u.rem(10)`, and I'm using rems for this because it is adding space between two text elements and I'd like it to be able to scale up as the base font size increases for better readability.

However, when we save, in our terminal it looks like we have an error in our Sass compiler. And it says `There is no module with the namespace 'u'.` Looking back at the features.scss file, that's because I forgot to use our util module for our rem() function. So at the top we need to add the `@use '../util' as u` rule to get our util rem() function. And if we save and scroll down in the terminal, there's no more error which is good. If we go to our browser and inspect the h3 tag, we can see it has the `margin-block-end` rule and in the `Layout` tab we can see that it's 10px of bottom margin.

Next up, let's do the same thing for the `features__description` styles. If we go to the mobile design, the description text has a font-family of `Source Sans Pro,` font-weight of regular which is 400 in CSS, a font-size of 18px, line-height of 23.4px-- which if we take our calculator and divide 23.4 by 18 we get 1.3 for the line-height value in CSS-- and it's the same gray color `#383A4A `as the title. The gray color should get inherited from the body tag styles-- we mainly will want to check the font-size and line-height.

Let's check the website to see what needs to be added. The `features__description` text, if we inspect that and go to the `Computed` tab, has a font-size of 18px and a line-height of 23.4px, which is correct. And the font-weight looks like it's regular, not bold which is also correct.

There's also a margin-bottom rule from the default browser paragraph styles, and it's set to 18px. I'm not sure if we actually need that margin-bottom since in the design, it's unlikely that we'd ever have more than one paragraph in the feature descriptions. So I'm going to set the bottom margin to zero, just for the `features__description` paragraphs. In features.scss, in the `&__description` selector I'll add a new rule for `margin-block-end: 0`. This way it won't affect paragraph tags in other sections.

Ok! Now that we have our basic styles for the Features item set, I think we can go back into VS Code and create the markup for the other two items in the index.html file. What I'm going to do is select the `features__item` div and duplicate it twice by pressing Ctrl-D twice. And on the website we now have three Features items. Looks pretty good, we do need to update the icon image and the copy for the other two items.

Looking at the design, the second item has the bell icon, and the third item has the speech bubble with the money symbol, so let's update those first. In VS Code I'm going to go to the second `features__item` and in the `src` attribute delete the file name except for the word `icon`, and it should pop up the autocomplete, and I'll select `icon-bell.svg`.

We also need to change the width and height attributes. Back in the design, in the mobile frame I'll select the bell icon, and it says 41px wide by 48px tall. Let's also do the same for the bell in the desktop design and that is also 41 by 48 pixels. So in the index.html file in the img tag for the bell icon, I'll update the width attribute to be 41.

Let's update the icon in the last item-- I'll go to the `src` attribute and again delete the filename except for the `icon` word, then select `icon-payments.svg`. And let's also get the width and height of that payments icon from the design. In the mobile design the icon is 60.57 pixels wide by 48 pixels tall. And in the desktop design it is the same, 60.57 by 48. So back in index.html I will update the width attribute of the payments icon to be 60.57.

Next up we need to copy and paste the copy for the two Features items. In Figma I'm going to copy the title from the second Features item, `Immediate notifications` and paste it in the h3 tag of the second feature. Then copy the paragraph and paste it in the paragraph tag. And if I save, VS Code will automatically wrap that long paragraph text for me. Then I'll copy the title of the last feature, `Protected payments` and paste it in the last feature's h3 tag. Then copy the paragraph of the last feature, and paste it in the paragraph tag, and then save.

Now, in the website we can see that we have the different icons, titles, and descriptions for the 3 features! Next, we're going to work on the layout so that we have 3 columns on desktop and 1 on mobile. I'm going to show you how to make the layout responsive, using flexbox and grid, both with and without media queries.