# Sass @extend at-rule

As I mentioned, the Sass `@extend` at-rule lets you apply all the styles from a different selector to your current one. Let's go to VS Code and I'll show you how we can extend the Full-width Feature rules to the Full-width CTA section.

In VS Code, I'm going to have the fw-cta.scss file open, and then also open the fw-feature.scss file. Then I'm going to right-click the fw-feature.scss file and select `Split right` to have it open on the right half of the editor. Then in the left half, let's have the fw-cta.scss file open.

Now, let's decide which selectors from the Full-width Feature styles we want to extend to the Full-width CTA styles. The `fw-feature` class has the white text color, and the `text-align: center` styles that we do want to use in the CTA. So let's start there.

On the left, in the `fw-cta` class selector, I'm going to extend the `fw-feature` styles by writing `@extend` and then the selector we want to get the styles from, `.fw-feature`. However, when we save, the Sass compiler throws an error, so let's take a look at that.

In the terminal, the error is coming from the fw-cta.scss file, and it says that the target selector `.fw-feature` was not found. This is because we need to load the fw-feature.scss file as a Sass module in the fw-cta.scss file in order for it to be accessible there. This is similar to how we need to load the util styles with the `@use` at-rule at the top of all our Sass partials.

Let's load the `fw-feature` styles. Up at the top, under the util `@use` at-rule, I'm going to write `@use 'fw-feature'`. The fw-feature.scss file is in the same folder as the fw-cta.scss file, so we don't need to navigate to a different folder, and we don't need to write the underscore or the `.scss` file extension, just the name `fw-feature`.

And now when we save, the compiler is successful and there is no error, which is great! Another thing to note about the `@extend` rule is that unlike the util styles, which use the namespace `u`, we don't need to add any namespaces to load the `fw-feature` class in the `@extend` rule. This is because for `@extend` we only need to type in the selector, the `fw-feature` class, so I think Sass treats it differently from when we're loading named functions and mixins from other Sass modules.

Ok, now that we've added our `@extend` rule, let's check out our website and see if it worked. And it looks like the styles were successfully extended to the Full-width CTA section-- the text color is white, and all the content is centered. If we inspect the section tag, in the style rules, we can see that using the `@extend` rule created a compound selector for both `fw-cta` and `fw-feature` classes, and they are both using all 3 style rules that were originally just for the `fw-feature` class.

Then, the background with linear-gradient() is getting added over the magenta background-color.

One thing to keep in mind if you use `@extend` to reuse styles is that when the Sass is compiled to CSS, the extended styles are located in the part of the stylesheet where they originated from. In our website, you can see this in the compound `fw-cta, fw-feature` selector-- Firefox tells us that it's coming from the fw-feature.scss file, which is where the original style rules are located.

Let's find where these styles are in the final, compiled CSS file in the browser. Up at the top, where we have the `Inspector` tool loaded, I'm going to click that double right angle bracket and go to `Style Editor`. Here, we can see a list of all the CSS and Sass files that are getting loaded on the website.

Let's click on the `style.css` file, which is our compiled styles. This is a pretty cool feature because we had minified our style.css file, but here in the Firefox Style Editor they've unminified it so the styles are more readable.

Anyway, let's click into the editor and press Ctrl-F, and search for `.fw-feature`, and then press Enter. And here on line [XXX] we can see that compound selector for both `fw-feature` and `fw-cta`, with those 3 style rules that we extended to the Full-width CTA section. Now let's do another search, this time for `.fw-cta`. And here we have the styles from the fw-cta.scss file, all the way at the bottom of the stylesheet.

The reason for this is because, if we go back to VS Code, in the scss/components folder, the index.scss file there is forwarding the `fw-cta` styles last after everything else. If we go to the fw-cta.scss file, it does seem a little weird to have the extended styles from `fw-feature` not load in the actual `fw-cta` class.

But this is how the `@extend` at-rule works-- in order to share the styles, it will take the selector using the `@extend` at-rule, which in our case is the `fw-cta` class, and it will add it to the originating selector, the `fw-feature` class, creating that compound selector.

One downside of extending styles from another selector is that you might end up extending some style rules that you don't really want or need in the target selector. In our case, the `fw-cta` selector is getting the magenta background-color from the `fw-feature` styles, but we don't need it in the Full-width CTA section.

And this is just one style rule which isn't a huge deal, but depending on the styles in the originating selector, you might be porting over a bunch of styles that you don't need.

One way around this problem is to use Sass placeholders.
