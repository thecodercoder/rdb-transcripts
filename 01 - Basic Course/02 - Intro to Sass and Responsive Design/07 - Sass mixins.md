Sass Mixins and Built-in Modules

Let's go back into our styles and look at some more Sass helpers that will make our code more efficient.

I'm going to use what's called a Sass mixin to rework our media queries. Mixins in Sass are bits of style rules that you can create and reuse. They're sort of like variables, because they let you type shorter code instead of having to manually write things out all the time.

We're going to create a mixin that we can use every time we want to write a media query. First off, I'm going to create a new Sass file in the util folder called `_breakpoints.scss`. And I'll forward it in the util `_index.scss` file.

In our breakpoints Sass file, I'd like to save the breakpoint widths so that I don't have to remember all the numbers. And what I'm thinking is to have 3 different breakpoints: one for mobile, one for tablet, and one for desktop. Mobile devices will be at 700px and less, then tablets will be between 700px and 900px, small monitors will be between 900px and 1440px, and large screens will be 1440px and larger.

To save these values, we're going to use one of the built-in Sass Modules called Sass map. The built-in modules are functions and other things that come out-of-the-box with Sass. And with Sass map, you can save data in key/value pairs similar to an object in JavaScript or other programming languages. This may sound kind of complicated, but what it boils down to is that I want to set widths smaller than 700px width as `small,` widths between 700px and 900px as `medium,` widths between 900px and 1440px width as `large,` and width greater than 1440px as `xlarge.` That way when I'm writing media queries I don't have to keep remembering the number, but can use the sizes: small, medium, large, and xlarge.

Let's make our Sass map! I'm going to call this map `breakpoints-up` and we will be using it with our `min-width` media queries. To create the map, similar to creating Sass variables, the map name needs to start with a dollar sign. So we'll write `$breakpoints-up` then add a colon, and a parentheses. In the parentheses, we'll start adding our keys and values. The `keys` term is a programming word that means the name or property that we will be giving a value. With min-width media queries, our mobile styles will be the default styles and so don't require a media query. So the first key will actually be `medium` which we'll save as a string so it'll be in quotes, then add a colon and we'll add the value which is considered a number in Sass, so it doesn't need quotes.

Now the medium breakpoint is 700px, but if you remember we don't want to use pixels but a relative unit. Now while I use the rem unit for setting my fonts and other sizes, when I did research on the best font for media queries, it seems like `em` or `M` units are best for those. You can use rems but there were apparently some bugs in Safari for them if you zoom in on the browser, so I use `em` units. To get from pixels to em units, 1em is calculated relative to the parent element. And for media queries, an em unit will be based off the browser's base font size. The base font is by default 16px, making 1em equal 16px. So to convert from 700 pixels to em units, we'll pull out our trusty calculator and divide 700 by 16 to get 43.75em. Then for the `large` breakpoint we'll divide 900px by 16 to get 56.25em. And the `xlarge` size will be 1440 divided by 16 to get 90em.

Ok, now that we have our Sass map for the min-width breakpoints, let's create the mixin that will use that Sass map to write the media queries.

I'm going to create a new mixin by using the Sass at-rule `@mixin` and name the mixin `breakpoint` with curly brackets. Then in the curly brackets we'll add the media query that we want to write:

```
@mixin breakpoint {
   @media (min-width: ){

   }
}
```

But how do we get the breakpoint values from our Sass map into the media query? Because we want to set the min-width to the breakpoint numbers when we write the name `medium,` `large,` or `xlarge.` To load a value from the Sass map, we can add the Sass function `map-get` where we normally would type in the breakpoint width.

The `map-get` function will take two parameters: the name of the Sass map we're loading data from, and the name of the key that we want to load the value from. The first parameter will be the name of the Sass map: $breakpoints-up. But the second parameter to load the key name, could be any of the keys that we created.

Since we want to keep that option open, we can load the key name as a parameter of the mixin. So in the `breakpoint()` mixin we'll add a parameter called `$size` and set the second parameter of the `map-get` function as that parameter. This way, when we use the mixin in our styles, we'll have the ability to say either `medium,` `large,` or `xlarge` to load whichever breakpoint value we want. Lastly, in the media query itself, we'll write `@content` which will load all the style rules inside the mixin when we are using it.

If this is the first time you've used mixins I can totally understand how this can sound very confusing and complicated. But let's use this mixin in our actual styles, and I'll point out where each part is coming from.

So back in our `_grid.scss` file, we're going to update that media query for the `.grid` parent element. Instead of saying `@media (min-width: 900px)` we will load the mixin with another Sass at-rule called `@include` and write `@include breakpoint(large)`. Then we will keep all the style rules as is.

When we save we're getting an error saying `undefined mixin`. This is similar to Sass variables, in that we need to load the util Sass modules in the `_grid.scss` file, similar to what we did in the `_boilerplate.scss` file. We can do this by up at the top writing `@use` and then navigating up to the util folder with '../util' and then loading it in a namespace with `as u`. Then when we call the mixin we will load it as `u.breakpoint`. And now we've gotten rid of the error.

Let's check out how this looks in the browser. In our website when we slide the inspector panel over, the layout still switches between 2 columns on desktop and 1 column on mobile which is great! And if we click on the `grid` element in the HTML markup, we can see that the `.grid` style rules have that media query loaded and it says `min-width: 56.25em` with all our styles, which means that our mixin works!

Let's look back in our code and trace how the mixin is getting loaded. In `_grid.scss` we're using `@include` to load the mixin called `breakpoint` with a parameter of `large.` Then in the `_breakpoints.scss` file the `breakpoint` mixin will write a media query, and it will get that min-width number by loading the `breakpoints-up` Sass map and using that `large` parameter will return `56.25em.`

So back in `_grid.scss` for widths of 56.25em or 900px wide and greater, the style rules for having 2 columns in the grid template will override the 1 column grid template for mobile.

I did want to point out one big difference in writing media queries between Sass and CSS, that I briefly mentioned earlier. In the Sass file we're able to write the media query inside the selector that it applies to. But in pure CSS this would not work. The CSS syntax for media queries is opposite of in Sass-- the media query at-rule can't be nested within the selector, but the selector itself is nested inside the media query.

Let me show you what I mean in the final CSS file that gets generated in the dist folder. I'm going to hit Save to trigger Prettier to run and format the minified CSS file into non-minified so we can more easily look at the style rules.

If we scroll down to the `.grid` selector, we can see that first we have our mobile rules with the 1-column grid template. And after the `.grid` selector is the media query which then has another instance of the `.grid` selector inside it, with the desktop style rules for the grid.

This is another way that Sass is a bit more efficient than writing pure CSS. You don't have to write out the selector another time for the media query. Instead you can just nest the media query inside the selector.
