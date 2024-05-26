# Using the rem function

If we go back to `_typography.scss` in the h1 tag selector, let's go back to the font-size where we initially used pixel numbers. So I'll delete that second line and uncomment the first line. And I'll do the same for the h2 tag, and in the paragraph tag I'll change 1rem back to 16px. So this is how we started before converting to rems last time.

In the h1 selector I'm going to replace the 28px value with the `u.rem()` function, and in it I'll add `28` as the parameter. And I'll do the same for the 16px number, and the 40px number. Now let's save and make sure there's no errors when the Sass is compiled. Everything seems ok, so let's look at it in the website!

If we inspect the h1 tag we can see that the font-size is indeed using rem units which is good, and it means our function is working properly. If we slide over the inspector panel, the font-size of the h1 tag will go all the way down to 28px at minimum, then as we increase the viewport it will increase steadily until it hits 40px, and it won't go higher than that. This looks like everything is working!

However, if we make a typo when using the function, let's say I forget that I shouldn't add the `px` unit, and write `u.rem(28px)`, what happens? When we save there's no error, so let's see what the website looks like. And this is not great-- in the browser the font-size property for the h1 tag is invalid. If we look closer, that first parameter in the clamp function says `1.75pxrem` which is not a valid CSS value. What happened was since we left that `px` in the parameter, the function still did the math and converted 28 to 1.75, but it kept the `px` and just added on `rem` since we have that in the function.

This isn't great because it fails silently, with no error. So what I want to do is throw an error in our compilation if the parameter of the rem() function is using the `px` unit by mistake. This sounds like actual programming, and it kind of is. Sass comes with a lot of functionality that you might not initially associate with just writing styles. Some things you have to import a built-in Sass module, kind of like how we imported sass:math for our rem() function. Other things come with Sass out of the box, like using `@if`, `@else`, and other things.

In our function I want to check the $pixel parameter to see if it has a unit or not. So on the Sass site let's do a search for `unit` and check out the results. And this looks promising: "Returns whether $number has no units." This is exactly what we want to do, so let's look at that.

It looks like we can use the `math.is-unitless()` function and it will return true or false. And we need to add an if condition, so that if the $pixel parameter is not unitless, it will throw an error. Let's also read the Sass docs on how to write an if/else condition, and how to throw an error.

Doing another search on the Sass site for `if` there's a page on `@if and @else` at-rules. We can write the `@if` followed by the condition, and then run the coe in curly brackets. And the same using `@else`.

And one more search on `error` will send us to the page and we can throw an error by using the `@error` at-rule. Those should be all the components that we need. Let's add them into our code.

In our rem() function, we first want to add an `@if` condition and check if the $pixel parameter is unitless. So we'd write `@if math.is-unitless($pixel)`and add curly brackets. This first condition is if the number has been input correctly with no unit at all. If this is the case, then we'll run the rest of our function to divide by 16. So we'll put the whole`@return` statement in this first condition.

Then if $pixel is not unitless, meaning it has a unit, we want to not run the rest of the function but throw an error. After the closing curly bracket of the `@if` statement, we'll add `@else` and another set of curly brackets. Then in that, we will write `@error` and then some kind of error message. I'll write: "Don't use units when using the rem() function, only numbers."

Now, when we save, in our output for the Live Sass Compile extension, it seems to be erroring out. And if we scroll to find the error message, it tells us that the `u.rem(28px)` should not have the unit. This is good! We do want it to throw this error so that you'll fix the problem. Going back to `_typography.scss` we'll remove the pixel unit from that 28, and when we save there are no errors. Let's check the output CSS just to confirm. And it looks like the h1 tag has a valid value of 1.75rem instead of that 1.75pxrem that we had earlier. Lastly if we open our website and inspect the h1 tag, the font-size property is also valid. So we are good for now!

Just a note, there is a lot of Sass functionality that I personally don't use, and won't be covering in this course because it can get kind of advanced. But I am showing you all what I actually use myself. But you can of course explore more of what Sass does outside of this course. I recommend CSS Tricks and Andy Bell for places you can go to find some more advanced Sass topics and tutorials.

Now that our rem() function is working, let's go through our styles and replace any instances of pixels with the `u.rem()` function. So in `_typography.scss` we can update the h2 and paragraph tags. And in the `_grid.scss` file, we can update the gap, width, and padding pixel values.

I do acknowledge that there are a lot of steps to size our typography in a way that is accessible and scales up nicely. I totally understand why people like working with pixels because it's simpler for the developer. But, we have to keep the end user in mind when we're building websites, and using pixels will not be accessible to users who need to change their base font size in their browser. So even though there is an extra step with using the rem function, I think it's worth it in the end. And, once you have the function created, you can keep reusing it in all your projects.

And actually, we can create a very similar function for converting from pixels to em units, that we can then use for our breakpoints. When we initially created our Sass maps for the breakpoint values, I just calculated manually. So using an em function would save us time in the future.

In our `_functions.scss` file, I'm going to copy and paste the rem() function, and then rename the copy to `em.` And I just need to update any instances of `rem` with `em` and this should be good to go. And the math is the same for ems when they're used in media queries, because they're based off the base font size which is 16 by default. So we don't have to change any of that part.

Now, in our `_breakpoints.scss` file, we can use the em() function for our values. First, we need to import the `_functions.scss` file as a Sass module. Since the `_breakpoints.scss` file itself is already in the util folder, we can't import util like we have been in other Sass files, because it will try to import itself and that doesn't work. But we can import just the `_functions.scss` file. So I'll write `@use` and then the functions file is on the same level in the folder as breakpoints, so I can just write `functions as f` to import it with `f` as the namespace.

Then in the $breakpoints-up map, the medium value can now be set to `f.em(700)`. And before we update the other values, let's just check and make sure that this is working correctly in our final CSS file. In style.css, if we scroll down to the `grid` class selector, we can see the media query does seem to be loading the 43.75em breakpoint value. So we can go ahead and replace the other Sass map values with the em() function.

And once that's done I'm going to remove the comments since I only had them to be able to reference the original pixel values. And we don't need them anymore thanks to the function!
