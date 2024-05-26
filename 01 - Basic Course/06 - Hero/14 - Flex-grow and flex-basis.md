# Flex-grow and flex-basis

I did want to show you one more thing in relation to flex-basis and flex-grow, and how they together determine the Final Size. To do this, just for this little demo, I'm going to go inspect the `hero__image`, and in the `Rules` tab, uncheck the `max-width` rule, so that it doesn't override the flexbox rules.

And now in the `Layout` tab, the Final Size isn't clamped by a Maximum Size, but is allowed to grow according to its flex-grow value.

So in our `Rules`, we had set the hero image to have a flex-grow of 5, and the hero text to have a flex-grow of 6. And both have their flex-basis set to 0, so they will both increase from zero width to their final size, at a rate based on their flex-grow number.

If we look at the flex-grow numbers, the `hero__image` width to `hero__text` width ratio should be 5 to 6. And if we divide 5 by 6 on our calculator, we get 0.8333 repeating. And on our website, if the widths of both elements is set based on the flex-grow values, we would expect the ratio to be the same. Let's see if that's true.

If we inspect the `hero__image`, we can take the Final Size, [XXX] and put that in the calculator. And then divide it by the `hero__text` Final Size, which is [XXX]. And the result is 0.8333 also. It's not exactly the same-- probably because the browser rounds the width to 2 decimal places, but it's very very close.

So this tells us that the Final Size for both flex child items does match their flex-grow values. However, this is with both of them having a flex-basis, or initial size, of zero.

But what happens if we set a flex-basis on one of them that's greater than zero?

For this mini demo, I'm going to set both of their `flex` values to 1 to start off. This means both their flex-basis values will be zero, and since their flex-grow values are both 1, they should increase from zero at the same rate of growth. And if we inspect them, they are both the same width, of [XXX] px.

Now let's change the flex-basis of one of them, how about the `hero__text`? In VS Code, I'm going to go to the `hero__text` class selector, and add a new `flex` rule under our existing one.

And I'll set it to `1 1 100px` so flex-grow and flex-shrink are both still 1, but flex-basis is now 100px. Due to the cascade, the second `flex` rule is going to override the first rule.

Now if I save and go to the website, I can uncheck the second rule to toggle between the two rules, to make it easier for us to see the change between `flex: 1` with the flex-basis of 0, and the second rule with a flex-basis of 100px.

it looks like with the new flex-basis of 100px, the `hero__text` element gets bigger. And it is taking some width away from the `hero__image`, which is shrinking.

With the new style rule in place, let's go to the `Layout` tab to see exactly what's going on in more detail. Ok, for the `hero__text`, we can see that the `hero__text` now has an initial size of 100px, due to the flex-basis of 100px that we set. I'm not exactly sure why it's labeled `Content Size` instead of `Base Size` like we can see on the image, but my guess is that it's because it doesn't have any style rules setting the width, like the `hero__image` has.

But the important thing is that the `hero__text` has an initial size of 100px, which you can see in the diagram is that dotted blue rectangle. And then from there it grows 490px to be a total of 590px. On the other hand, the `hero__image` still has an initial size of zero, due to flex-basis being 0, and then it also grows 490px to be a final width of 490px.

They are both growing 490px because they have the same flex-grow number. But the `hero__text` has a Final Size that is 100px more than the `hero__image`. You can think about this like it having a 100px head start over the `hero__image`, but then they both grow the same amount after that point. So the Final Size is going to be the flex-basis plus any flex-growth factor.

Let's try another experiment. In the `hero__image` styles, I'm going to change it from `flex: 1` to `flex: 2`. The flex-basis doesn't change, but now the image will grow twice as much as the `hero__text`, since it has a flex-grow value of 2, versus the `hero__text` still having a flex-grow of 1.

In the `Layout` tab, the image has an initial size of 0, then it grows 653.33px, which is its Final Size too. To compare, the `hero__text` has an initial size of 100px from flex-basis, then grows 326.67px, which is supposed to be half the growth of the `hero__image`, since the `hero__text` is `flex: 1` instead of `flex: 2`.

Just to confirm this, if we take our calculator and put in 326.67, if we multiply it by 2 it will be 653.34px, which is pretty much the amount that the `hero__image` grew by. And again, that matches the flex-grow of the image being double that of the `hero__text` element.

To review, the final size of a flexbox child will be dependent on its initial size, which you can set with flex-basis. And flex-basis will automatically be set to 0 if you set it with the `flex` shorthand property.

Then the Final Size will be dependent on how much it grows based on the flex-grow property. The amount of growth will be calculated based on how much available space there is in the flex container, and then divided among the flex children based on their flex-grow number.

And, as we saw earlier with the unicorn image, the size may also be affected by min or max-width style rules, or by the natural dimensions of the image file itself.

I haven't talked about flex-shrink, and that's because I don't think it needs to be utilized as often. Flex-shrink is kind of the opposite of flex-grow-- if the flex children are larger than the flex container, their flex-shrink number will determine how much they will shrink relative to one another, in order to fit in the container.

But if you're using the `flex` shorthand, it sets flex-basis of all the flex child items to zero, and then they grow to fit. So while it's good to have flex-shrink set to 1, just in case they need to shrink, I personally don't use it very much when building layouts.

Okay, so that's the flexbox layout for the hero. I also have a couple of optional videos next, with an alternate way of building this layout using grid. If you don't want to watch them, you can go ahead to the `Double-checking` video.
