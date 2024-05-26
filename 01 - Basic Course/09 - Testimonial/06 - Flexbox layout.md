# Flexbox layout

Alright, so let's build out our flexbox layout for the author image and author text, so that on desktop they are side by side, but on mobile they are stacked one under the other.

In VS Code let's go to the index.html file, and figure out which elements will be the flex parent, and which will be the flex children.

The author image is the image tag with class `testimonial__author-image`, and the author text info is in the figcaption tag. So we'll want to have the flex parent or flex container be the div with the class `testimonial__author-wrapper`.

And the flex children will be its direct children-- the image tag and the figcaption tag. However, while the image tag has a class already, the figcaption does not. And we'll probably need to give it a class that we can target in our styles.

Let's add a class to the figcaption tag and call it `testimonial__author-caption`. Then in our styles let's add the selector for that, after the `author` and before `author-description` since the figcaption comes before the paragraph. We'll add `&__author-caption`.

Now we'll be able to target the figcaption as a flex child item using this class.

Let's start setting up our flexbox layout. I'm going to show you building an intrinsic approach, where we don't need media queries for the layout styles, but can use the same set of styles for both mobile and desktop.

Let's start by adding the styles in the browser itself. I'm going to go to the `author-wrapper` div since that's the flexbox parent, and in the `Rules` tab I'll add `display: flex`. Now we have the author text next to the author image. And let's click the `flex` label to turn on the Flexbox highlighting.

Next, we need to add space between the image and text. Going to our design, I'm going to look at the desktop design and between the author text and image, we have 30px of space. Going back to our site, I'll add `gap: 30px`.

After that, we want to vertically center the text to the image. So again in the flex parent rules, I'm going to add `align-items: center`. And now the text is vertically centered.

At this point, we've basically done the desktop styles. If we compare it with our desktop design, things look the same. Now, however, the trick is to get the mobile layout where the text is under the image.

Let's try reducing the viewport width to a mobile width.

Ok, so we still have both image and text on the same row since that's the default styles for flexbox items. Let's try to allow flexbox to wrap the flex child items onto multiple rows if it needs more space. In the parent styles, I'll add `flex-wrap: wrap`. And now the text is wrapped to the second row.

But we do need everything to be centered on mobile. Let's do that with `justify-content: center`. And now we have everything centered. Let's go back to a desktop width to see if anything breaks.

And now, on wider viewport widths, since there's enough room now, the text is once again next to the image. However, the whole flexbox container is centered, due to the `justify-content: center` rule that we added for mobile.

This is a problem-- we want the content to be left-aligned on desktop, but centered on mobile. The reason this is happening is because the flexbox parent, the `testimonial__author-wrapper` div is a block item since it's set to `display: flex`. And block items will by default, take up 100% of the available width unless you explicitly set the width to a different value.

One thing we can do is to change the `display` from `display: flex` to `display: inline-flex`. And now we can see that the flexbox content is no longer taking up 100% of the width, and it's left-aligned.

What's happening is that the `inline-flex` will make the flexbox container behave like a `display: inline` element. Meaning that it will only be the width of the content that it contains. And because we're loading the website in a left-to-right direction, the default alignment of inline elements will be from left to right.

Now, the desktop styles match the design again. Let's check what it will look like on mobile. I'm going to turn on Responsive Design Mode and make sure we have iPhone selected. And it looks almost like what we have in the design. The image and text are centered, but it looks like we might have a bit too much space between the image and the text, from our `gap` of 30px.

Let's check the mobile design and see how much space we have there. In the design, it looks like we have 20px of space. So, going back to the website, we can adjust the `gap` property so that it will have 20px of space between rows like on mobile, and then 30px of space between columns like we need on desktop. In the `gap` property, I'm going to add `20px` before the `30px`. And if we expand the shorthand `gap` property, it tells us that we now have a `row-gap` of 20px, and a `column-gap` of 30px.

Now it looks pretty good on mobile. And I'm going to click the `inline-flex` label to turn off the highlighting. And that looks pretty good. However, you may have already noticed this, but the author info text itself also needs to be centered. We can do this by adding `text-align: center`, but we only want the text to be centered on mobile. On bigger viewports it's supposed to be left-aligned.

Unfortunately, to change text alignment between viewports we have to use media queries-- there's no other way around it. But, it was nice that we could write all our layout rules in one set of rules, without needing media queries.

Before we forget, let's go back to the `testimonial__author-wrapper` and copy all those styles we added. And I'll paste them in our styles in the `author-wrapper` selector. And I think I'll just leave the gap numbers as pixels, since it shouldn't affect readability too much if the gap spaces don't scale up if the browser font size increases.

And for the `text-align: center` rule, I'm going to put it in the `author-description` selector.

With my media queries, I do usually use `min-width` only if possible. But in this case, I think a `breakpoint-down` which uses a `max-width` media query might be most efficient, because we can choose to only target mobile viewport widths and down, and add the `text-align: center` rule there.

If we used a `min-width` media query, we'd have to add `text-align: center` as our default style, and then in the media query we'd have to cancel it out with `text-align: left`. So doing a `breakpoint-down` will let us only need to write 1 `text-align` rule.

Let's add that now. If you need a refresher on the breakpoint mixins, we can go to the breakpoint Sass file, in scss/util/breakpoints.scss. Here we have the `breakpoints-down` Sass map, and we want to target the `small` size. And we can do that by loading the `breakpoint-down` mixin`.

Let's add that In the `author-description` styles, I'm going to write `@include u.breakpoint-down` and then in the parentheses I'll add `small` to only target mobile styles. And in the curly brackets I'll add `text-align: center`.

Now let's save and see how that looks on our website. On our website we still have the iPhone emulation, and it looks good! If we compare that to the mobile design, they match. Let's also check out the tablet view-- I'm going to change to an iPad.

And here we have the desktop version of the styles. A lot of times for tablet styles, they're like a hybrid of the mobile and desktop version, especially if you don't get a specific tablet design. I felt like in this case, giving the tablets the desktop styles makes the most sense, since they do have a lot more horizontal space than the mobile version.

And let's increase that viewport width to see how it looks on larger desktop screens. And the author content looks good!

However, if we look at the desktop design, the quote text is actually a lot narrower-- it breaks to a new line on the word `bootstrapped` and if we check the width, it's less than 800px. But on our website, if I select the `testimonial__wrapper` div, it's the full 1200px width of the wrapper's max-width. So we do need to adjust that width for the Testimonial section.

I think what we can do is add a rule on the `testimonial__wrapper` to set a `max-width` of 800px. Now the width is less, but it's still centered due to the global `wrapper` styles that we have. Ok, I think that's a good solution. Let's go to our Testimonial styles, and up at the top in the `testimonial__wrapper` selector I'll add `max-width: u.rem(800)`.

Now let's save, and on our website, the quote text isn't as wide. So that looks pretty good!

And that's it for the Testimonial section! Let's commit our changes in GitHub Desktop. We want to eyeball the changes, and that looks fine. So for a commit message I'll type in `Testimonial` and click `Commit to main` and then `Push to origin`.

And next up we'll be looking at the Full-width CTA section.
