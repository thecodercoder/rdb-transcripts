# Header styles

To start out, let's refer back to the design, to see how the text looks. In Figma, in the mobile design, everything is stacked to one column. And the image is centered, but the text content and buttons are all left aligned.

Now let's go to our website and I'm going to turn use the iPhone emulation. And let's see what we need to change when we compare our website with the design.

One big thing we need to do is make the text color in the hero block white instead of the default dark gray color that it currently is now. But where should we add that style rule? Let's look in our source code to decide what element we want to target with the text color.

Ok, so it looks like all the text content is in the `hero__text` div, and that div has h1, paragraph, and anchor link tags. We could add the rule to each individual tag. However, I think that it would be more efficient to add the style rule in one place whenever possible.

We could also add it to the `hero__text` div-- let me add `color: white` to it. And this changes the text color in all the other text elements inside that div, because child elements will inherit the color property from its parent. That's why we often set the default color on the body tag, because it will add that color to any element inside it, unless it is changed.

Personally, I would add the style rule to the hero section tag. All the child elements will inherit the color style from it, and we already added `background-color` to the hero class, and I like the idea of grouping background-color and color styles together. So let's go into VS Code and do that.

Since we stored our colors as CSS custom properties in our colors.scss file, let's look there to see which ones we need to use. For the white text, back in the colors Sass file, I'm going to use the `--text-light` custom prop. So let's copy that, and then in the hero.scss file, if you want to pause the video here, try writing the style rule to set the color to that custom property.

We're going to write the rule in the `hero` class selector. And the property to set the text color is `color`, and to load the CSS custom property we want to use the var() function, and in it, paste the custom prop name. So it should look like `color: var(--text-light)`. Let's save, and now, when we look at the website, the text in the hero is now white!

Next up, let's get our font sizes working, and look at our design. And we'll start with the main header text. It is 42px on mobile, and on desktop it is 72px. Let's see what we have currently on the website for that header text.

On the website I'll go to a mobile viewport width, and inspect that h1 text. And it has the font size using the clamp() function that we set, and if we go to the `Computed` tab we can see the calculated font-size. And it looks like it is set at a minimum of 42px. And if we increase the viewport width, it increases until it maxes out at 72px. So it seems like we already set the header font size, which is great.

One thing I'm noticing is that there seems to be just a little more space between the first and second lines of the header text on the website, when we compare to the mobile design. In the `Rules` tab I had set the line-height to 1.1 for h1, h2, and h3 tags. A line-height of 1, without any unit, will be 100% of the font-size, so a line height of 1.1 will be 110% of whatever the font size is. And it will change as the font-size changes.

Let's see what the design says. Ok, in Figma the mobile frame has 42px font size and 42px line-height, so it should be 100% or a line-height of 1. And desktop the font-size is 72 and the line-height is also 72. So we want the h1 tag to have a line-height of 1.

Going back to VS Code, we have our global text styles in the globals/typography.scss file. Up at the top, we have that compound selector for the h1, h2, and h3 tags where we set the line-height to 1.1. And below that we have individual styles for the h1, h2, and h3 tags.

What I think I might do is remove that line-height style rule from the compound selector, and then set line-height for the individual h-tags as we come across them in our design. So I'll delete that, and then in the h1 tag selector under our font-size, I'll set `line-height` to 1.

And let's check that it's been changed on our website. And yes, if we inspect the h1 tag we can see the line-height is set to 1. And in the `Computed` tab, the line-height is the same, pretty much, as the font-size. So we're good for the line-height.

Now on our website, one thing I'm noticing is that there's a lot of space under the h1 tag. If we inspect the h1 tag, there's that yellow highlight over the space, which tells us that there's a margin-bottom creating that space. However, in the `Rules` tab, there are no styles set for margin-bottom, which tells me that it's coming from a default browser style.

We can actually see the default browser styles in the `Computed` tab, if we check `Browser Styles`. Then because there are just so many, we can add a filter for `margin`, and we can see that `margin-block-end` and `margin-bottom` are both set to 45px.

And if I click the arrow for `margin-block-end` to expand, it tells us that the 45px is coming from that first style rule setting it to 1em. The em unit means that it will be 1 times the font-size of the element itself. And if we filter for `font-size` it tells us that it is indeed 45px.

And, filtering back to `margin`, this is another example of the `margin-block-end` being the same thing as `margin-bottom`. It seems like the actually style rule is for `margin-block-end`, and `margin-bottom` is just taking the same value from it.

Anyway, let's go back to the design and see how much space is under the h1 tag. On mobile, we have 20px under the h1 tag. And on desktop, it's also 20px. So in our styles, I think we can set the margin-block-end to 20px, using our rem function, so we'll write it as `u.rem(20)`. Again, I'm trying to use the more modern `margin-block-end` instead of `margin-bottom`, but both work, so you can use either one.

I think we are good for the h1 styles. If you're wondering why I'm setting the styles here in the global typography Sass file instead of hero-specific styles, I do think you could set them in either place. Because there's really only one h1 tag on the page, in the hero, I think it's ok to set the h1 styles in the typography.scss file.

Going back to the website, the headline looks good! Next up, let's check on the paragraph styles, starting with the paragraph under the h1 tag.
