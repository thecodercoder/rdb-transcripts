# Sass functions

We've established that it's best to use a relative font size like rem or em units. But, as you saw, I had to pull out the calculator to divide by 16 in order to go from pixels to rems. This gets old really quick, as you might imagine. There is one workaround that you may have heard of, where you set the font-size in your html element to 62.5%. This makes 1rem equal to 10px since 62.5% of 16px is 10px. Then you simply divide your desired pixel size by 10 to get to rems, for example 3rem will equal 30px.

I don't see any actual issues with this, but I personally prefer to try to keep to that default 16px size. And with Sass, we can create a Sass function to do all our conversions for us.

In our project files, I'm going to create a new Sass file in the util folder, called `_functions.scss` and I'll forward it in the `_index.scss` file.

In our functions file, I want to create a function that will divide a pixel amount by 16 in order to get to rems.

To create a function, we'll write `@function` and give it a name. I'm going to name this `rem`. This function will take one parameter, which I will call `$pixel`. Then in the function we need to do some math to divide `$pixel` by 16. In the old version of Sass we used to be able to use a forward slash to divide with math. But with Sass modules needing that slash for loading the file path, we can't do that anymore. But there is a built-in Sass module that comes with some math functions, so we can use that! If we search for `Sass math` we'll find the documentation on the Sass website that can help us get this working.

First off, let's go to the Overview of the Built-In Modules to see how to use them. If we look at the code example, it tells us we can use the `@use` at-rule to import the module, the same way that we're importing our Sass modules from our actual files. Up at the top of the functions Sass file, we can write `@use 'sass:math'` to import it with a default namespace of `math.`

Now let's look at how to divide with sass:math. I'm going to do a quick search for the word `div` for `divide` and there's a section at the bottom about "Other Functions." There is a `math.div` function that takes two parameters and divides the first number by the second number.

Back in our functions Sass file, in the rem() function let's use the `@return` at-rule to return the result of `math.div` with the parameters of $pixel divided by 16. And we'll need to add the `rem` unit at the end. That should be all we need. Now let's use our rem() function!
