# Sass mixins

For our placeholder styles, we had put them in the globals folder. However, that meant that we had to add another `@use` at-rule to load the global styles. For our mixin approach, I think I might prefer to move the shared styles into the util folder, along with the other Sass mixins and functions. That way the styles will get loaded along with all our other utils.

In VS Code, I'm going to select the fullwidth.scss file, and drag it from the globals folder into the util folder. Then I'll go into the globals/index.scss file, select the `@forward 'fullwidth'` at-rule, cut it, save the file, and then go to the util folder's index.scss file and paste it there.

We can also now remove the `@forward globals` rule from the fw-cta.scss file, and also from the fw-feature.scss file. So let's delete those. Now, let's go to the fullwidth.scss file, and we're going to change it from a placeholder to a mixin. I'm going to replace the `%fullwidth` with `@mixin fullwidth`. So now we've created a new mixin called `fullwidth` and it will generate the same rules as we had before.

Let's go to the fw-cta.scss file first, and in it, instead of the `@extend %fullwidth` rule, I'm going to change it to say `@include u.fullwidth`. And because the mixin lives in the util folder we do need to use that `u` namespace.

We also need to make these changes in the fw-feature.scss file, so let's go there. And I'll change the `@extend %fullwidth` to `@include u.fullwidth`. Ok, now we're using mixins for these shared fullwidth styles. Let's make sure everything is saved, and the compiler has no errors, which is good, and let's check out the website.

Let's check out the Full-width CTA section-- I'm going to inspect the section tag. And now in the Rules, we can see that the `fw-cta` class has the background-image rule that we set in the fw-cta.scss file. But in the same selector it also has the color and text-align rules from the mixin. And you might notice, there's no more compound selector. These shared style rules have essentially been copied and pasted into the selector where we included the mixin.

If we go back to the fw-cta.scss file, we can see that in the `fw-cta` class selector, we added the `fullwidth` mixin which added those 2 share style rules, and then we added the background-image rule.

Unlike with the globals placeholder approach, the styles from the mixin are getting added right where the selector using the mixin is located. Which is one benefit that mixins have over placeholders, because the shared styles aren't getting added in unexpected places in the final CSS file.

Let's look in our style.css file and see how our final styles look with the mixin rules added.

If I go to the `Style Editor` tool and select `style.css` and then click into the editor and do a search for `fw-cta`, we can see that all the Full-width CTA styles are located all together at the end of the stylesheet. And this is where they should be, because the fw-cta.scss file is the last Sass partial that is getting forwarded in our styles. And if we search for `fw-feature` we can see that it also has the 2 style rules for that class.

Let me show you another cool thing you can do with the mixin approach. In the Full-width Feature section, if we inspect the paragraph tag, we added some styles to limit the width to 70 characters and center it with `margin-inline: auto`. I'd like to share that style with any paragraph tag that is in a fullwidth section.

Let's go back to VS Code, and in the fw-feature.scss I'm going to copy the `&__description` selector and all its rules, and then cut it, and paste it in the fullwidth.scss file in the fullwidth mixin. And now, if we reload the website, in the Full-width Feature section we can inspect the `fw-feature__description` paragraph, and it has the styles from the `fullwidth` mixin-- the `margin-inline: auto` and the `max-width: 70ch`. And, if we go to the Full-width CTA section and inspect that paragraph tag, it also has the same rules since it's using the `fullwidth` mixin too.

Going back to the fullwidth.scss file, what we did was add that nested selector for the parent, a double underscore, and then `description`. So when we include the mixin in the fw-cta.scss file, the parent selector is the `fw-cta` class, and it targets the `fw-cta__description` class which we've used in the paragraph tag.

And in the same way, in the fw-feature.scss file, the parent selector is the `fw-feature` class, so it targets the `fw-feature__description` class. We could do the same thing for the `fw-feature__image` styles, since that also is getting centered with `margin-inline: auto`.

So we can select the entire style rule, cut it, and then paste it in the fullwidth.scss file in the `fullwidth` mixin. So now, in future sections that are full-width and have an image, we can center both the paragraph and image elements in that section, as long as they have the proper BEM element name of `description` or `image`.

Let's check the website to make sure the styles for the paragraph and the image are still getting added. Ok, and in the Full-width Feature section, the `fw-feature__description` class has the two styles, and the `fw-feature__image` has the `margin-inline: auto`. And in the Full-width CTA section, the `fw-cta__description` paragraph has the 2 style rules.

So, that's how we can share styles using mixins. I feel like this is a good approach that doesn't do anything potentially unexpected like with placeholders.

Next up, let's see how to share styles using helper or utility classes.
