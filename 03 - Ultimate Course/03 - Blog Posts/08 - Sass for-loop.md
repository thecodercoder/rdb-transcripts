## Sass for loop

Let's look at the Sass documentation to see what we need to do. In Firefox we'll search for "sass for loop". And the first result is the "@for" page at "sass-lang.com" which is what we want, so let's go there.

They have an example here of a for loop. So what's happening is that we first have to determine how many times we're going to loop through the code, using a variable to keep track of what the current number is.

Here, we have a variable, $i, which will start being equal to 1, on the first loop around. Then on the second time, which is also called an iteration, $i will be equal to 2, since it will increase by 1 each time. Then the third time it will be equal to 3. And that will be the last loop because we set the loop to run from 1 to 3.

Then, each time it loops, it's going to output the code inside the curly brackets. So when $i is 1, the selector will be "ul:nth-child(3n + 1)", and in the code it's generating a color, and in the lighten() function that they're using, the second parameter will be 1 times 5%.

Then it'll go back through and output the same code again, except this time it'll be nth-child(3n +2), and in the lighten() function it'll be 2 times 5%. And then it'll go through again for i equals 3.

That's how the for loop operates. One other thing I wanted to mention is that in the "nth-child(3n + i)", the "$i" variable is contained in a hashtag and curly brackets. This is something called "interpolation" which I mentioned briefly back in the Basic course Footer section.

We need interpolation when we are loading a variable inside a string-- in the nth-child pseudo-class, the content inside the parentheses is a string, like "3n + 1", that will get passed on to the browser.

But when we compile the value of "i" when compiling Sass to CSS, we don't want the variable "i" to be a literal letter "i". We need to tell Sass that we want the actual value of "$i", either 1, 2, or 3. And we can do that by surrounding the $i variable with the hashtag and curly brackets.

We don't need to interpolate the "$i times 5%" because the lighten() function is a Sass function, and it already knows that the second parameter will be some kind of number.

I'm mentioning the interpolation because we will need to use it in our own for loop.

I'm going to copy the for loop example code, and we'll use that as a starting point. First, we need to figure out what number range we're going to use, which will result in the number of times we want to loop. In the styles we created, we went from nth-child(1) to nth-child(5). So let's change the number range from going from 1 to 3, to 1 to 5.

Then, inside the curly brackets, we need to add the code that we want to repeat. So I'm going to copy the entire "nth-child(1)" style rule and paste it in to replace the example code.

Now, we need to integrate the $i variable into the code, otherwise every loop will generate the exact same code. If you want, try pausing the video and looking at all the 5 nth-child style rules, and see if you can figure out the places where we need to add the $i variable in the loop code.

[ pause ]

Alright, in our loop we're going from 1 to 5. And in our nth-child style rules, the nth-child number goes from 1 to 5. So we want to make the number the value of the variable $i.

Since the nth-child pseudo-class is a browser thing, and doesn't get compiled in Sass, we can't just write "nth-child($i)" because it would literally just say "nth-child($i)" in the CSS which wouldn't accomplish anything.

But just for comparison's sake, let's see what happens if we just say "nth-child($i)". When we save, we get an error in the Sass compiler, down at the bottom. And if we look at the error message in the terminal output, it says "Error: expected 'n'". This means that it just read the $i as a string saying "dollar sign i" and not the variable.

We'd get the same error if we changed it to say "xyz". So, we need to interpolate the variable to tell the Sass compiler that this isn't a string saying "dollar sign i", this is a Sass variable and it needs to get the actual value of the variable i.

So let's interpolate it by adding the hashtag and putting it in curly brackets, so it reads "hashtag curly bracket $i curly bracket".

Now when we save, we don't get an error. This is good, but we want to make sure that the correct final CSS is getting generated from our Sass code. Before we check, let's select all the hardcoded nth-child styles and then comment them out with Ctrl or Command forward slash, since our Sass code will be replacing it.

Now let's check that by opening the sidebar and going to the dist folder, and opening "style.css". And if we search for ".blog" then we should be able to find the "blog\_\_item:nth-child" styles.

And here it is. And it looks like we have the nth-child() numbers all here, going from 1 to 5! So that is great, and it means that the variable is successfully getting compiled to the final value in each loop.

Now let's update the contents in the calc() function to also use the variable. Again, in our hardcoded styles which we commented out, in the calc() function it goes from "45deg times 1" to "45deg times 2", and so on all the way to 5.

We should be able to replace the number multiplier with our variable, since it also matches the loop number. And do we need to interpolate this? Well, one quick way to find out is to just try and see if it throws an error or not.

So if I replace the "1" with "$i" and save, there is no error. And let's check the CSS file. And in our CSS, it starts at 45deg, then goes up to 90, 135, and keeps increasing. Looks good! Let's go back to our blog styles and delete the commented out styles, since we don't need them anymore.

And if we check out the website, we can see that the gradients are changing.

However, there is a bit of a problem with this approach. In our loop, we've only gone 1 to 5, which will generate styles for the nth-child items from 1 to 5. But what happens if we end up with more than 5 blog posts in the grid?

Let's try and see. This is another example of stress testing that I try to do-- I try to think about how in the future, the content of the website might change. And if we can handle those different situations beforehand, it will save us time in the future.

In our index.html file, I'm going to select all the "blog\_\_item" elements and then duplicate them. So now we have 10 total blog posts.

And let's save and see what happens on the website. Alright, so we now have 10 items in the grid, and we can see the gradient rotating from the first through the 5th item. But the sixth item and on have just the straight gradient.

If we inspect one, and go to the "blog\_\_filter" element, it's getting the initial styles we put on the "blog\_\_filter" class. This is better than nothing, since it's at least not blank. But it's not really desirable because we have that same-y effect going on.

So is there anything we can do that will handle as many blog items as we want, even if we went super extreme and had like 30? Going back to our blog styles, it seems a bit inefficient if we made the loop go to like 30 or 100 and generated all that code.

But, there is something that we can do! Remember when we were talking about the odd and even nth-children when we were making the Alternating Features section?

If we go back to the website and inspect the first row, in the styles it says "nth-child(2n+1)". And if we click the "alt-feature.scss" link, Firefox will load the initial Sass style so we can see that "2n+1" means the "odd" numbers, so 1, 3, 5 etc.

It works because the browser will apply this to all values of "n" from 0 up to basically infinity, all in that one style. So we can try to apply this in our for loop, so that the browser will be able to handle any number of blog items.

Before we write the code, let's take a look at our website to figure out how we want this to work. We have 5 nth-child items in our loop, so I'd like to repeat them every 5 items. So the first gradient where we have a 45 degree direction will get applied to the first child, then it'll go through the other 4 variations until we get to the sixth child and that will use the first variation again.

So each of the 5 variations will repeat every 5 items, 1 2 3 4 5, 1 2 3 4 5. [ move mouse cursor to each block ]

Let's go to our styles and see how we can do this. In our loop, let's just think about the first variation. We want this to be applied for nth-child 1, then add 5 to get 6, then add another 5 to get 11, and so on-- adding 5 each time.

Then the second variation, we want to get applied every 5 items, starting with 2. So 2, then add 5 to get 7, then add 5 to get 12, and so on. Each number will be 1 more than the numbers from the first variation.

And we'll keep going like that for all 5 loops.

So, since we know each variation will repeat every 5 times, we can multiply the i variable value by 5. So we can write this as "5n + 1".

This means that the first variation will repeat starting from n equals zero, then n equals 1, and so on to infinity. So when n = 0, it'll be 0 + 1 = 6. Then when n = 1, it'll be 5 + 1 = 6. And it'll keep increasing by 5.

And for the second variation, when $i equals 2, when n = 0, it'll be 0 + 2= 2, then when n = 1, it'll be 5 + 2 = 7, and so on.

So this should work for all our loop numbers. Let's try saving our "5n + i" change and check out the final CSS file. And here we can see the nth-child parameters begin with "5n" and then add the different values of i.

That seems good. Let's see how that looks on the website. And in our blog grid, we start at the 45 degree angle, then it rotates until the 5th item, and then the 6th item starts again with the 45 degree gradient. That seems good!

And one other change we can do is to try to get the full rotation so it goes all the way around. If we're starting in the top right corner for 1, then going 2, 3, 4, 5, then to get the full rotation we'll need 6 going left, 7 for top left, then 8 for top.

So we'll want 8 loops to make the full rotation. Back in our blog styles, in our loop I'll make it go to 8 instead of 5. And we'll have to update the nth-child number to be "8n" since with 8 variations we'll want to repeat every 8 instead of every 5.

And now when we save we're going from 1, 2, 3, 4, 5, 6, 7, 8 and then it goes back to the first variation in the top right corner.

And let's bring back the images and text blocks, I'm going to delete the "opacity: 0" rules. And now we have our gradient filters looking a lot more different from one another!

These are looking pretty great. Let's go back to the index.html file and delete the extra 5 items we added.

And here we are! Let's try to compare with the design, first for desktop view. And if I toggle between them and just try to eyeball, it's looking pretty good.

Now let's try the mobile view, I'll turn on Responsive Design Mode and go to iPhone view. And let's put the design next to it. And yeah I'm pretty happy with that.

So I think we're pretty much done with the Blog posts section!

Let's do our usual thing and commit our changes, in GitHub Desktop. I'll eyeball the files, and it looks like they're all good to commit. And in the commit message I'll write "Blog section". Then click "commit" and "push to origin".

And let's also check the Netlify deployment and see how everything looks on the live website.
