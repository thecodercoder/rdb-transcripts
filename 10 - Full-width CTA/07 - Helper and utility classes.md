# Helper/utility classes

To set up the helper classes with the shared styles, I think it would make the most sense to put them in the globals folder, since the util folder is for Sass mixins, functions, and other features that then can be loaded in other Sass partials with the `@use` at-rule.

In VS Code, I'm going to go into the scss/globals folder, and create a new file. And I am going to call this `fullwidth`. Because even though it's a duplicate file name of our mixins Sass file, in real life you would be using one or the other. I'm just going to keep the fullwidth mixin file around for future reference.

And since we have a new Sass partial, I need to go into the globals index.scss file and `@forward` the `fullwidth` partial. And now, let's go to the fullwidth mixin file, and I'm going to copy the whole thing and paste it in the globals/fullwidth.scss file. And of course, we need to make this a helper class, not a mixin, so I'm going to remove the `@mixin` at-rule and make the `fullwidth` name a class.

So now, we have a `fullwidth` BEM block, and then a `fullwidth__description`. And to apply these styles, we need to add these classes to the proper elements in our index.html file.

In the index.html file, I'm going to go up to the Full-width Feature section, and in the section tag I'll add the helper class `fullwidth`. Then for the paragraph tag I'll add the class `fullwidth__description` and in the image tag, I'll add the class `fullwidth__image`.

And let's do the same in the Full-width CTA section. In the `fw-cta` section tag, I'll add the `fullwidth` class, and in the `fw-cta__description` paragraph I'll add the class `fullwidth__description`.

And, we need to go into the styles for each section and remove the mixin so it's not doing anything. In the fw-cta.scss file, I'm going to comment out the `@include u.fullwidth` rule, and then do the same in the fw-feature.scss file. I'm commenting them out just for test purposes in this course, for reference and so that it's easier to add the mixin back in.

Now let's make sure everything is saved, and see if the fullwidth styles are getting loaded on the website. Going first to the Full-width Feature section, I'm going to inspect it, and if I select the `fw-feature` section tag, we can see that it does have that `fullwidth` class, and in the styles below, we can see the `fullwidth` class and the 2 rules.

Then, if we click into the `fw-feature__description` paragraph, we can see that it does have the helper class `fullwidth__description`, and in the Rules it has the styles centering it with `margin-inline: auto` and setting the max-width to 70ch. Looks good!

And let's go down to the Full-width CTA section, and do the same thing. It does have the `fullwidth` class and styles in the Rules, and the paragraph also has the helper class and the style rules. So it looks like everything is working!

Whether you use the mixin or the helper class approach, they are accomplishing the same thing, but in 2 different ways. With the mixin, you need to load the mixin in your styles anywhere you want to use it. So we had to include it in both the fw-cta.scss file and the fw-feature.scss file. But we didn't have to adjust anything on the HTML side-- everything is controlled from the Sass files.

With helper classes, you don't have to add an extra style rule to the selectors where you want to use the shared styles. But you do have to add the helper class to the HTML. So it really boils down to where you want to add a little extra complexity in your files-- either Sass or HTML.

The strict BEM approach would not use helper classes, but everything would be handled on the Sass end, and the HTML elements would only have the BEM class name. On the other end of things, if you use all helper classes, like what Tailwind does, your HTML elements would have a lot of class names.

I think both approaches are fine-- I've been using a combination of BEM styles for most things, but also helper classes for components like the button that would likely get reused if new pages and sections get created.
