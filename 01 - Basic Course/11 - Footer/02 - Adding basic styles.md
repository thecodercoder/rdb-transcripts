# Adding basic styles

We need to create our Sass partial for the footer styles. In VS Code, I'm going to go to the scss/components folder and create a new file there, and let's call it `_footer.scss`. And as usual, since we have a new partial, we need to forward it in the index.scss file. So we'll open that and at the bottom I'll write `@forward 'footer'`.

Then, in the footer.scss file, at the top we want to use the util styles, so I'll write `@use '../util' as u`. Then we can start adding the selectors for all the HTML elements in the footer. I'm going to go to the footer.scss tab, right-click, and select `Split down`. Then in the bottom half I'll go to the index.html file. This way we can reference it as we're adding all the class name selectors.

Ok, starting with the `footer` BEM block name, in footer.scss I'll add that class of `footer` and curly brackets. Then we'll just continue down the elements. Next up is `footer__wrapper` so in our Sass file I'll add `&__wrapper`, then `footer__logo`, `footer__homelink`, `footer__logo-image`, `footer__copyright`, `footer__column`, `footer__links`, `footer__item`, and then the last one is `footer__link`.

That's good for now, so let's close the split footer.scss file. And now we can start adding some of the basic styles. In Figma, in the footer, the first elements are the logo and copyright text. We did copy the markup for the logo image from the Top Nav, but we should also check to see what styles we set on the image tag for the Top Nav, because the Footer logo image will probably need the same styling.

Let's go to the website and up in the Top Navigation, inspect the logo. The image tag has a class of `topnav__logo` and in the styles we did set some styles for the width for mobile and desktop. Right now the footer logo looks like the same size as the Top Nav logo, and that's because it's using the original size from the SVG file itself. And we also added width and height attributes that match the original SVG size.

However, both of those are in pixels, which will not scale if we increase the browser base font size. So what we need to do is use those same width styles for the footer logo.

Let's check the design just to compare the Top Nav and Footer logos before we do anything in the styles. In Figma, in the desktop design, I'm going to first check the Top Nav logo image. And it is 128px wide by 36px tall. Then on mobile, the Top Nav logo shrinks to 70px by 20px.

Let's also check the Footer logo image. On desktop it is 128x36, which matches the Top Nav. And on mobile it looks like it stays the same size, at 128x36. So this is different from the Top Nav logo which shrinks on mobile.

Next up, let's go back to Figma and check the space underneath the logo image. On desktop, it has 10 pixels of space between it and the copyright text. And on mobile it is the same, also 10 pixels of space under the logo.

Going back to the website, if we inspect the logo image, there's no space under it. So let's add that. In VS Code, I think I'll add the space to the image tag itself, targeting the `footer__logo-image` class. In our styles, I'm going to add the space with `margin-block-end` and using the rem() function, set it to `u.rem(10)`. Now let's save, and on the website we can see that the logo now has space under it.

Let's also check the font-size for the copyright text. In Figma in the desktop design if we select it, it tells us that it's 18px and has a line-height of also 18px, so that would be a line-height of 1. And on mobile, it looks like the text is the same size. Let's check what our website has.

If we inspect the copyright text, it looks like it's using the global paragraph styles. Let's see what the calculated pixel size is in the `Computed` tab, and it looks like it's 18px which is what we have in the design. The line height is greater than 18px, so we'll want to adjust that in our styles.

This paragraph has the class `footer__copyright`, so in VS Code, in the footer.scss file we want to target the `footer__copyright` class selector, and add the rule `line-height: 1`. And if we save and go back to the website, we can see that it has the `line-height: 1` rule, so we're all set with that.

Next up, let's check out the styles for the footer links. In Figma, on the desktop design, the h3 tag is bold, which it already is, and it's 22px font-size and 24px line-height. If I pull out the calculator and divide 24 by 22, we get around 1.1 for the line-height. And then under the h3 text is 14 px of space. Then in mobile, it looks like it is the same, 22px font-size and 24px line-height. And 14px of space under it too.

Back on the website, let's inspect that h3 tag, and it's inheriting the global h3 styles of 1.5rem and line-height of 1. If we go to the `Computed` tab the font-size is 24px. So we need to change the font-size to 22px.

It looks like the h3 tag doesn't have a class yet, so we should add one. Let's go to VS Code and the index.html file, and add a class to the h3 tag, and let's give it a class name of `footer__column-title`. I think that will be a good, descriptive name.

Then in the footer.scss file, under the `column` class selector let's add `&__column-title`. You could also nest this in the `footer__column` selector with `ampersand dash title` but I prefer to keep all the selectors on the same level in the Sass file.

In the `footer__column-title` selector we can add our styles. So let's add `font-size: u.rem(22)` and `line-height: 1.1`. And to add the space under it of 14px, I'll write `margin-block-end: u.rem(14)`.

Now let's make sure the index.html file and the footer.scss file are both saved, and check out the website. And we can see the h3 tag has the class, and also the styles that we added. I'll just check the `Computed` tab for the calculated font-size and it is 22px, and it has the margin-block-end of 14px. So we are good.

Next up is the links themselves. In Figma, the links are the default dark gray text color. And they are 18px font-size and 18px line-height which would be 1 since it matches the font-size. And then below each link is 10px of space. The links have the class `footer__link`.

In our styles, we'll add it in the `footer__link` class selector. We'll add `color` and let's just check the colors that we have in globals/colors.scss, and the one we want is `--text-dark`. So let's copy that and then in footer.scss we'll set the color to `var(--text-dark)`. Then we can add `font-size: u.rem(18)` and `line-height: 1`. And then a `margin-block-end` of `u.rem(10)`.

Now let's save, and check out the website. The text styles look good, but it doesn't look like the space between links is loading. Let's see what's going on here. If I inspect one link, we can see the styles, and our `margin-block-end` rule is there, but if I hover over the anchor link in the source code, it looks like the margin is just kinda floating over the next line-- it's not actually pushing the other elements away.

This is probably due to the `display` property. I didn't set it explicitly, so the display is taking the browser default, which for anchor links is `display: inline`. Let's just confirm that I'm right about that-- also, if you don't know off the top of your head what the browser default is, you can always check what's going on in the `Computed` tab.

Let's check the `Browser Styles` to show all the default browser styles, and I want to filter for `display`, and the anchor link is by default `display: inline`. You can tell that this is a browser default because let's try a property that we know we set-- let's filter for `margin-block-end` and there's a small caret or arrow. If we expand it, it tells us where in the styles the rule came from and we can see that it's something that we set. If we filter again for `display`, the rule doesn't have that arrow, so that means it is a default browser style.

Let's try setting the anchor links to `display: block`. And now the space is showing up. But because these are links, it's making them take up 100% of the width, so it's actually making the empty space to the right of the text links clickable, which could potentially cause confusion. So I think instead of `display: block` which makes it go all the way across, let's add another rule in the browser for `display: inline-block`.

So now the links are only taking up as much space as the text itself, and we don't have the extra clickable space, which is great. You might have noticed that if I toggle the `display: inline-block` on and off, the text is slightly moving up and down.

This is because for inline and inline-block elements, the browser will add that tiny bit of space at the bottom of the element to leave space in case there are letters with descenders.

I'm ok setting these footer links to `display: inline-block` and having that tiny bit of extra space, so let's add that to our styles. And save, and now on the website the links have the space between them, and don't have any extra clickable area.

And actually now that we're fixing this issue, we have the same thing going on for the logo link. If you hover to the right of the image, it's clickable. This is kinda weird because if you hover over the image, it's set to 128px wide, and if you hover over the anchor link containing the image in the source code, it's also 128px wide. But it's still clickable all the way across the parent width.

I do want to get rid of the extra clickable area there too. We could set the `footer__homelink` anchor link to inline-block. Which you can see does work. It does add that little space for the descenders, even though it's an image it still gets added to any inline or inline-block element.

If you don't want that space, another alternative is to set the anchor link to `display: block` but then to prevent it from going all the way across, set the width to `fit-content`.

This will limit the width of the anchor link to its content, which is the image, so it won't be wider than the image, and we won't have the extra clickable area. Either solution works. I kinda like the `display: block` and `fit-content` solution because we don't need space for descenders with the image. I'm going to copy those rules, and then in the styles paste them in the `footer__homelink` selector.

Now let's save and check the website. And the logo no longer has the extra clickable area, and we'll just check that the same is true for the text links, and they look good too.
