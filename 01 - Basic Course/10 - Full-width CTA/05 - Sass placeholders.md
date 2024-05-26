# Sass placeholders

Sass placeholders work with the `@extend` at-rule, but instead of extending styles from an existing selector, you can group the styles that you want to share under what's called the `placeholder`.

This is a selector that you designate with a percent symbol at the beginning of the name. And the placeholder itself does not compile to CSS. It's essentially invisible, and its style rules will only get compiled when the placeholder is extended.

Let's see what this looks like by creating a placeholder for those full-width styles that we do want to be shared between those two sections.

In VS Code, let's have the fw-feature.scss file open on the right, and the fw-cta.scss file on the left. As we mentioned, in the fw-feature styles, we don't need that background-color, but we do want the white text color and the centering.

So what we can do is create a placeholder. For convenience's sake, let's create it in the fw-feature.scss file. I'm going to create it by first typing the percent symbol, and then the name for the placeholder-- I'm going to name this `fullwidth`. And then let's add curly brackets for the rules. And I'm going to select the `color` and `text-align` rules, cut them, and paste them in the placeholder.

Now we can extend the fullwidth placeholder in the `fw-feature` class by typing `@extend %fullwidth`. And we can do the same thing over in the fw-cta.scss file by changing the `@extend` rule to load the `%fullwidth` placeholder.

Now, on our website the Full-width Feature section has the white text styles and the centering, and so does the Full-width CTA section. Let's inspect the CTA section. In the `Rules` we still have a compound selector-- this is because both `fw-cta` and `fw-feature` class selectors extended that placeholder. But the difference is that the magenta background-color from `fw-feature` is no longer part of the shared styles.

So adding a placeholder is a bit more efficient way of using the `@extend` at rule for shared styles. However, there is one issue that can come up that could potentially really trip you up when using placeholders and `@extends` with Sass modules.

For our `%fullwidth` placeholder, we created it right in the fw-feature.scss file. But since it has shared styles, it might make more sense to put it in our global styles as opposed to the fw-feature.scss file. So, in VS Code, I'm going to go to the scss/globals folder and create a new Sass partial, and call it `_fullwidth.scss`. And we'll need to forward it in the globals index.scss file by writing `@forwad 'fullwidth'`.

And now, I'm going to go to the fw-feature.scss file, select that placeholder and cut it, then paste it in the fullwidth.scss file. And it looks like we do have an error in the Sass compiler, where it can't find the `%fullwidth` placeholder since we moved it. So what we need to do is in the fw-cta.scss file, instead of using the fw-feature.scss file, we need to load the globals since that's where the placeholder is.

So in the `@use` statement, I'll change the path to be similar to loading the utils folder, where we have two dots to navigate up out of the scss/components folder, then a forward slash and the folder name `globals`. And we don't need to worry about a namespace since placeholders don't need them.

And we want to copy that `@use ../globals` rule and paste it also in the fw-feature.scss file so that it can also access the placeholder in globals. And now when we save we shouldn't have any errors, and on the website everything looks the same on the Full-width CTA and the Full-width Feature sections.

That all seems good. But, let's take a look in our compiled CSS file. I'm going to go to VS Code, and load the dist/style.css file. And let's save to run Prettier and unminify our styles, and I'm going to press Ctrl-F and search for `.fw-cta` in order to find our placeholder styles.

Ok, we have that compound selector for `fw-cta` and `fw-feature` with the placeholder styles. But the weird thing is that they're located after the button styles, and before the wrapper styles. And if we continue our search for `fw-cta`, the styles from the fw-cta.scss file are all the way at the bottom.

As I mentioned earlier, when you use the `@extend` rule, the styles getting extended will be located where the originating styles are. Before when we were extending the `fw-feature` styles for the Full-width CTA, in our final CSS file the extended styles were located where the fw-feature.scss file got compiled.

But now, since we've put the placeholder styles in the globals folder, the placeholder styles are getting loaded in the global styles. If we open the globals/index.scss file, we have our `fullwidth` placeholder styles getting forwarded after the button styles. And what comes after the global styles? If we open our main style.scss file, we can see that after the global styles are loaded, we then load the layout styles, which right now just contain the wrapper class styles.

That's why, in our style.css file, the placeholder styles are located between the button styles and the wrapper styles.

Having these styles loaded with the global styles can cause issues with the cascade aspect of CSS. For example, on our website, I'm going to inspect the Full-width CTA section. And then click on the wrapper div. In the wrapper we have a padding-block of 80px for desktop. But hypothetically, what if we wanted to change the padding-block size to be bigger than 80px for full-width sections like this Full-width CTA section?

Let's go to the fullwidth.scss file. I might want to create another placeholder that we can load for full-width section wrapper class divs, to change the padding-block size. Let's create a new placeholder under the `%fullwidth` placeholder, and I'll call this `%fullwidth-wrapper`. Then in this selector I'll write `padding-block` and let's write a larger number, 120px.

Now, I want to extend this placeholder in the Full-width CTA styles. In the fw-cta.scss file, in the `wrapper` class selector, I'm going to write `@extend %fullwidth-wrapper`. What we want to happen is for the Full-width CTA wrapper div to have a padding-block of 120px instead of 80px.

Let's save and go to the website. However, the Full-width CTA looks the same as it always does. If we inspect it and select the `fw-cta__wrapper` div, we can see what's going on in the styles. And what's happening is that the `fw-cta__wrapper` is extending that 120px padding-block from the placeholder.

But because the placeholder is getting loaded along with the global styles, it's coming before the wrapper styles in the final CSS file. So according to the cascade, since the wrapper styles are coming after the `fw-cta__wrapper` styles, they are going to override them and the padding-block of this wrapper div is 80px instead of the 120px that we were expecting.

So if you do use placeholders and the `@extend` at-rule, you really want to be careful if you are extending styles across different Sass partials in different locations because of this quirk.

It won't be as much of an issue if you put the placeholder in the same Sass partial as where you're extending it. But that kind of goes against the organization of our Sass partials, because the fullwidth placeholders are essentially global styles, since they are going to be used in multiple different sections.

So ideally we should be able to put the placeholder styles in the globals folder, and it shouldn't mess up the cascade.

Along with this issue, there is another big issue with using the `@extend` at-rule, and that's that you can't use `@extend` inside a media query. For example, in the fw-cta.scss file, if we wanted to use that 120px padding-block just for the desktop wrapper styles, we might want to add our breakpoint mixin, `@include u.breakpoint(large)` and put the `@extend %fullwidth-wrapper` in the curly brackets. Unfortunately, when we save, it throws an error, saying `You may not @extend selectors across media queries`.

I'm not saying that you shouldn't use placeholders or `@extend`. I've used them in the past and they can be quite helpful. And I think they're ok to use if you are creating and extending styles all in the same Sass partial. But the cascading issue when you're using them across different partials I would consider a pretty big one, and they don't seem to play well with the newer Sass modules.

However, placeholders and `@extend` are still used on websites, and so you likely will come across them if you work with any legacy Sass code. I wanted to show you how they work, as well as their downsides and reasons that you might not want to use these Sass features moving forward.

But if you're not going to use placeholders and `@extend`, what can you use? Well, Sass mixins are another option for shared styles-- mixins are very powerful, and we've been using them to write our media queries, for example. And I do think that they are a decent option for when you do want to have shared styles.
