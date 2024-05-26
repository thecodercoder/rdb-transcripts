# Using clamp() for responsive typography

Let's start looking at the different font sizes that we have in our Figma design, and start putting those in our style rules.

I'm going to go into Figma, and if I select the heading, I can see in the right sidebar under the "Text" panel that the size is set to 72px. Let's also check the heading size in the "Mobile" frame. In mobile it is set to 42px. So we'll need to go back to our code and modify it to fit those sizes.

In VS Code, open the globals/typography.scss file, and we're going to update what we have for the h1 tag font-size property. This is using the CSS clamp() function. As a refresher again, the clamp() function is super useful for creating fluidly responsive typography on one line of code, without needing to set media queries.

Clamp() takes three parameters. The first parameter is the minimum value that will be allowed, the middle parameter is the "preferred" value which should be fluid and will change based on another factor like viewport width. Then the last parameter is the maximum allowed value.

So generally with clamp, you want your font-size to be whatever the middle parameter is and in our case it will get bigger or smaller if the viewport is bigger or smaller. And then the minimum and maximum values will prevent it from getting too big or too small.

For our h1 tag font size, the design had the mobile font-size set at 42px. I'm going to set the first parameter to that, since I don't want the font-size to be smaller than that. So in our code I'll set the first parameter to `u.rem(42)` to use our rem function which will convert 42 pixels to rem units for better accessibility.

Then in the same way, since the desktop style is set to 72px, I will set that as the maximum size allowed, and set the third parameter to `u.rem(72)`.

Now we need to figure out what to set the middle parameter to. Right now we have a combination of rems and viewport width units.

In my opinion, it is important that we use rems for the majority of the size, and viewport width units just enough so the font size will increase the amount we need.

Because while viewport units are relative units, meaning they are dependent on another factor, they are not accessible because they will not be affected if you change the browser base font size.

So it's better to add the rems to the viewport widths, and the more rems we use the more it will change when the base font size changes.

But how much should we set the rems and viewport widths to? It is possible to mathematically calculate and plot out what the final font size will be at different viewport widths, I think you can also just kinda try different values and kind of eyeball how the final result looks on the website.

So let's try some estimates. We know we want this to be between 42px and 72px, so I'll start by choosing a rem value that is less than 42, maybe something like 30. So let's write `u.rem(30)` to start.

Then we'll add the viewport width value, which will control how much the size will change as the viewport changes. I'll start with a small number, like 2vw. So after the `u.rem(30)`, let's add a `plus 2vw`.

Now let's see how this looks in the website!

In the developer tools, I'll have the Inspector and Computed tab open so we can see how the font-size changes. Then we'll start by sliding the Developer Tools panel over to a small, mobile size viewport.

We can see that the minimum value is working, as the font-size is stuck at 42px. This is what we want. Now, as we slide the panel to the right to increase the viewport width, we can see the font-size increasing.

Ideally, I'd like it to get close to 72px at desktop widths, around when the wrapper content gets capped at 1200px wide and you see that extra space growing on the left and right sides. Up in the top, I'm going to manually change the viewport width to bigger than 1200px, let's try 1250.

---

This is a lot of work tweaking things manually, as you can see.

If you don't want to mess around with this yourself, there is also a tool out there that you can use to create a clamp() function that will give you the exact font-size you need at the different viewports. It's a huge time saver, so let's try that too.

In our browser, search for "fluid typography calculator", and it should be the first result. (https://royalfig.github.io/fluid-typography-calculator/)

In the calculator, for our Min Font Size let's set it to the mobile font-size of 42px, then the Max Font Size will be the 72px for desktop. For Min Viewport I'll use the iPhone's width, which if you're not sure you can check by going back to our website, and in the Responsive Design Mode with iPhone selected, and it tells you that it is 375px.

So I'll put 375px for the Min Viewport. And for the Max Viewport, this is the viewport width that you want the font size to be the Max Font Size. I'd like the font-size to hit 72px right when it matches the wrapper width of 1200px. So I'll put 1200px for the Max Viewport.

Once you have all the numbers in, the Result should change, and then you can copy the font-size. The calculator gives you a fallback font-size of the minimum font-size. This is for older browsers that don't support clamp() yet. At the time of recording, all modern browsers support clamp, except for IE 11 and Opera.

A good way to check browser support for clamp() or any other CSS property is to go to CanIUse.com and then type in clamp(), and it'll show you the browser support. So if you need to support IE11 for whatever reason, you can include that fallback.

Going back to the calculator, under the fallback font-size, we have font-size with the clamp() function. How fallbacks work is that you want to include both font-size style rules.

For older browsers, they will load the first font-size rule, and will ignore the second one since it uses the clamp feature which it doesn't support. Then for modern browsers, they will load the first font-size rule too. But they will override it with the second font-size rule using clamp().

This is because of the "cascade" part of CSS (Cascading Style Sheets). CSS rules that come later in the stylesheet will override rules of the same specificity that come before them.

So I'm going to copy both font-size rules, and back in our code I'll paste it above the clamp() function we made ourselves. I'm also going to simplify the decimals so that they only have 2 decimal places. So that will be 1.77rem and 3.64vw.

Now let's save, and check out our website to see how close the 2 clamp functions are to each other.

Now in our website, if we inspect the h1 tag styles, we can see the 2 clamp() functions. The first one, from the calculator, is crossed out because it's getting overridden by the second one which is the one we made ourselves.

It's a bit hard to see since one is crossed out, but it looks like the minimum and maximum numbers are the same, which makes sense because we set those to 42px and 72px, converted to rems.

The middle number with the rems plus viewport widths, is different, but they're pretty close. I'm going to go back to our code, and do a combination of the two clamp() functions.

I'd like to keep the rem() functions, so that if the font sizes for mobile or desktop ever change I can change it more easily. But the middle rem plus viewport width from the calculator is more accurate, so I'm going to copy that from the first clamp() function and paste it in the second one. Then I'll delete the first one.

I'm also going to use the rem() function for our fallback font-size. The calculator uses the mobile font-size for the fallback, so I'll copy the `u.rem(42)` value and use that for the font-size.
