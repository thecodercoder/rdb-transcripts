## Gradient variations

Let's take a look at the website and see how we can change up the gradients a bit, so we don't have this "striping" effect going down the cards.

If I inspect the "blog\_\_filter" element, let's see how we can change the gradient. Right now they are all going in the same direction, from left to right. So maybe we can try changing the direction.

The "to right" value means it's angled at 90 degrees. Zero degrees means it will start from the bottom and go up, like a clock hand pointing at twelve o'clock.

Just in the browser for now, let's change the direction to "0deg". And now the gradient is more horizontal, and still stripe-y. Let's try 45deg... and now it's a bit more angled. Not too bad, but I think it might be really cool to have different angles of the gradient direction for the different cards.

Like 0 degrees for the first card, 45 degrees for the second, 90 for the third, and so on. Incrementing by 45 more degrees each time.

I'm going to try figuring this out in our styles, and then see if we can make it a bit programmatic using some pretty cool Sass features.

In VS Code, let's first hide the image and the text block, so we can focus just on the gradient direction. So in our styles, I'm going to go to the "blog\_\_image" selector and add "opacity: 0", then copy that line and then in the "blog\_\_text" selector paste it in there too.

Okay, now we just have the gradient. Next, let's start by targeting the first "blog\_\_item" child, and then in that, set the linear-gradient with the 45 degree direction on the "blog\_\_filter".

In our styles for the "blog\_\_item" selector, I'm going to nest a new selector, to target the first child. So I'll add an ampersand, and then instead of writing "first-child", I'm going to write "nth-child" and then in parentheses, "1". This is so we can target the other children by increasing the number.

Now, I want to target the "blog\_\_filter" class in this first child. So we'll add on ".blog\_\_filter" to our selector. And in here, we're going to reuse the "background-image" with linear-gradient() from the initial "blog\_\_filter" styles.

Let's select the whole style rule, copy it, and then paste it in our first child styles. And we'll replace the "to right" with "45deg". Now let's save and see if this works.

Alright! It looks like our new styles for the first child "blog\_\_filter" are working! The first gradient is now at an angle, and if we inspect it, we can see our new style rule.

And it is overriding the original rule because the original one.

Okay, so we have our new style rule for the first child, how about the other ones? Going back to our styles, I'm going to select the whole rule and duplicate it.

Then I'll change the nth-child number in the second one to "2". And I want to change the degree to be another 45 degrees greater, which is 90. However, we can use math to calculate this for us.

I'm going to use the CSS calc() function, and in it write "45deg" and then asterisk to multiply, and then "2". I really like the calc() function because you can combine different units and it just works. And let's also use this for the first child.

I'll copy the calc() function and then paste it to replace the "45deg" in the first child. And instead of 2 we'll set the multiplier to 1.

Now let's save and just make sure it works, and on our website it looks like the calc() function is working for the first one, and if we inspect the second one, the "blog\_\_filter" is using the nth-child(2) style rule, which is great.

Now, let's write styles for the other children. I'm going to select the second style rule and duplicate it for the 3rd, 4th, and 5th children. And I'm going to go to each of them and update the number to be 3 in both places, and then 4... and then 5.

And when we save, now on the website, we have our rotating gradient! Pretty cool, right?

But if we look at our styles, there is a ton of duplicated code. The only difference is the number of the nth-child and the multiplier that are increasing each time.

I just wanted to demonstrate to you how doing this the long way would look. Now let's make this a lot more efficient by putting all this code into a for loop in Sass.

A for loop is something you can do in programming where you are running the same piece of code a certain number of times, with some changes each time based on the order of the item.

I know that this may sound confusing if you haven't done programming before, but I'll show you how everything will work, in the next video.
