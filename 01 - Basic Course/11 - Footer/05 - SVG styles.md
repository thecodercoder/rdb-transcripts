# SVG styles

Ok, so we have the markup for the SVG working. However, it looks like the color is set to black, not the dark gray text color. So let's start working on the SVG styles.

With SVGs you can set the color of the path or other SVG elements with a `fill` attribute. We didn't set one in our markup, so it is defaulting to black-- we can see this in the `Computed` tab, if we check `Browser Styles` and then filter for `fill`. The fill is set to `rgb(0, 0, 0,)` or black.

We could add a `fill` attribute right in our inline SVG, but since it's an inline SVG we can actually target the `fill` in the path right in our styles. And since we have multiple SVGs it would be more efficient to do it that way.

I think we need to add some more classes to the SVG elements. If we go back to the index.html file, I'm going to add a class to the SVG and the path in the SVG. For the SVG class, let's call it something like `footer__social`. And then the path inside it, I'll add a class and call it `footer__social-path`.

Now, let's add selectors for both those classes in the `footer.scss` file. After the `footer__link` selector, I'll add `&__social` and we'll leave the selector empty for now-- we will add styles to that later on. But we do want to set the fill color of the path now. So after `footer__social` let's add another selector and we'll say `&__social-path`.

And this is targeting the path, so in this selector let's add the `fill` property and I want to set it to the same color as the text links, so if we look above that is set to `var(--text-dark)` so we can write the same thing for the fill.

Ok, now when we save, on the website, the Twitter icon is dark gray instead of black. And if we want to double-check, we can go to the `Computed` tab, make sure the `path` element is selected in the source code panel, and with `fill` in the filter, we can see that it is no longer black but dark gray.

That looks good! However I'm noticing that when hovering, the SVG doesn't change color like the text does. And ideally, we'd like the icon to also change to magenta on hover.

This is one reason why I wanted to use inline SVGs for these icons instead of using an image tag. We can change target the path in the Twitter SVG and change the fill color right in our styles.

We wouldn't be able to do this if we loaded the SVGs in image tags, like we did for the unicorn or laptop SVGs. So that's one benefit to using inline SVGs like what we're doing here.

Let's look in our styles to see where to add the hover state style for the SVG path. In footer.scss, if we scroll down to the `footer__link` selector, we do have a hover state already-- this is where we change the text link color to magenta.

Ideally, I'd like to put the SVG path's hover state style in the same hover pseudo-class as our text color change, so that anytime you hover over the anchor link, both the text and the SVG icon will change colors.

So I want to target the `footer__social-path` inside the same hover pseudo-class. Under the `color` style rule, I'm going to nest another selector, and we will have to manually type out the whole class, `footer__social-path`. Then we can add the `fill` property, and since we want it to be the same magenta color as the text, we can copy that `var(--text-link-hover)` and paste it in for the fill.

Having to type out the `footer__social-path` selector again inside this hover pseudo-class isn't totally ideal. Unfortunately, we can't use the ampersand like the other BEM selectors, because-- 1) the hover state will mess that up, and 2) even if we didn't have the hover state, using an ampersand inside the `footer__link` class selector would load `footer__link` which isn't what we want.

What we actually would need is a way to only load the BEM block name, `footer` so then we could tack on the `__social-path`.

Aside from writing out the class name, one alternative that I've seen used a lot is to create a Sass variable up at the top right inside the `footer` class. We could call it `$b` for the block name. All Sass variables need to start with the dollar sign. Then we would set it to `ampersand` to load the parent selector, which is the `footer` class.

Then, down in the `footer__social-path`, instead of writing out `dot footer` we could load the `$b` variable. Since we're using the variable in a selector name, we need to indicate that we're using the `$b` variable, we don't want a literal `$b` in the selector.

Loading a variable's value inside of a string is what's called `interpolation,` and it's a feature of programming languages that we can use with Sass To interpolate in Sass, we need to put the variable in a `hashtag curly bracket`, with a closing curly bracket at the end. So now, we have `#{$b}` and then the rest of the class name, `__social-path`.

This does work, and again, I've seen it used a lot when you have some nesting that's a bit tricky like when you're working with the hover state of a parent element. I think either is fine-- either using the variable like we have, or just writing out the whole `footer__social-path` class name, even though it is slightly duplicate work.

Ok, let's save our changes and see if it works. And on our website if we hover over the Twitter link, the icon does change to magenta along with the text! So things look good. Alright, now that we have the inline SVG loaded and it has the hover state, let's make sure it's sized and also aligned the way we want with the text.
