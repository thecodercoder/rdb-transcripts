# Set up hero styles

Now that we have our HTML markup for the hero section, we can start setting up our hero styles. The first thing we want to do is to create a Sass partial for the hero styles.

For this, I'm going to give you the chance to see if you can set it up yourself first.

In VS Code, first, take a look at the scss sub-folders that we have. Which subfolder do you think the hero Sass file should be added to? Free free to pause the video here if you want a little time to take a look.

Alright. I would add the hero Sass file in the scss/components folder. In the components we're keeping styles that are just for specific areas of the website and not reused throughout the site, like the Top Nav styles that we already have.

The globals folder is for styles that are used and reused throughout the entire site like colors and text. The layout folder is for styles related to controlling the layout-- right now we just have wrapper styles in there.

And the util folder is for Sass mixins, functions, and variables that can then be imported into other Sass partials with the `@use` at-rule.

Now, here's the next part for you to try, if you want. Can you create the Sass partial for the hero styles, in the components folder, and add a style rule to set the background color of the Hero section to be that purple color from the design, using one of the CSS custom properties we've already set?

I know this might sound like a lot, but I'd encourage you to pause the video and at least give it a try. If you get stuck, try looking at how we set up the background color for the Top Nav styles and try to follow a similar approach.

Ok, ready? You can pause the video, now.

Alright, so let's cover the steps that we need to do here. First, we need to create a Sass partial for the hero styles, and make sure that it works. Second, we need to make the hero background color that purple color, using one of our CSS custom properties.

I've found it helpful to break down what I need to do into different steps like that. And a lot of times I'll even write down each of the steps. I'm always a fan of breaking things down into smaller steps, because it helps you plan out what you need to do ahead of time, so you can figure out if that's the right approach, instead of just jumping in and potentially going down the wrong path.

Also, breaking things down makes the whole task seem easier to accomplish, because you can just take it one step at a time.

For the first step, in our app/scss/components folder, I'm going to create the new Sass partial. All the Sass partials' filenames need to begin with an underscore, to indicate that they are only part of your overall styles, and shouldn't be compiled into their own CSS file.

This is important especially if you are using the Live Sass extension. If you are, and you don't begin your Sass partial filenames with an underscore, the extension will compile every single individual Sass file that doesn't start with an underscore into its own CSS file.

So you really only want your main style.scss file to be the only Sass file that doesn't start with an underscore, and all your other Sass files that you want to include in your styles should begin with an underscore.

Ok, so I'm going to name this new file `_hero.scss`. Like we've done before, we're using `hero` because we want the filename to be the same as the BEM block name that we started using in our index.html file.

In the scss/components folder, since we created a new Sass partial, we need to make sure we forward it in the components index.scss file, so it gets included when compiling all our Sass files. In that index.scss file, I'll add a new `@forward` at-rule and then just the name of the Sass file, without needing the underscore or the `dot scss` file extension, since Sass can find it with just the name.

And, this is bonus if you remembered this step-- we want to make our `util` Sass features, like our breakpoint mixins, accessible in this Sass file. So we need to add our `@use` at-rule and load the util subfolder, first the two dots to navigate out of the current components subfolder one step up to the scss folder, then `slash util` to load the util folder. And then we'll give it a namespace `as u` so we don't have to type out `util` anytime we use our mixins.

Now what will happen is that in our main Sass file, style.scss in the main scss folder, it is forwarding the components subfolder, which will see that index.scss file and then forward the top nav and hero Sass partials.

Now, any styles that we want to add in the hero Sass partial should get loaded on our website. What we want to do is get that purple background color. But if you just want to do a quick test to make sure the hero styles get loaded, you could write a style rule that will make a very visible change. So let's add a selector, the `hero` class, which again is our BEM block, and I'm going to add `color: magenta.`

Then save, and check that there are no errors when compiling Sass, and I don't see any errors. So now we want to go to our website and check that the new style rule went through. And yes, our text on the hero is magenta, so that tells us that our hero Sass styles are successfully getting compiled!

Now that we know the hero styles are working, we can move on to the second step, making the hero background purple. So let's go back to the website to figure out what selector we need to target to add the background color to. Looking at the HTML in the source code, I'm going to start with the hero section tag and hovering over it, we can see that it is full-width. So that is probably what we want to target.

Going back to VS Code, we'll add the `hero` class selector with the dot to denote that it's a class name. And then in the curly brackets, we'll add `background-color:` but, we need to figure out what color to use.

We stored all our colors in the scss/globals/colors.scss file, so let's open that and see which one to use for the hero. If we look at the names of the CSS custom properties, we can see that there is one called `hero-bg`, which seems like the right one we want. I'm going to copy that name including the two hyphens, and go back to the hero.scss file.

Now if you need a quick refresher to make sure you're loading the custom property correctly, you can refer to the scss/components/topnav.scss file to see how we've loaded CSS custom props in the past.

Up at the top there's actually a background-color rule, using the var() function and then the name of the color. Going back to the hero styles, for the background-color value we can then type `var()` and in the parentheses paste the `--hero-bg` name.

And one note about the background, you can use the `background` shorthand property to set multiple background-related properties all at once, and that's fine. I just personally like to use the `background-color` property because it's more specific, and we're not using any other background properties like background-image here.

Let's save the file, do a quick check to make sure there are no errors in the Sass compiling, and then check out the website. And now we can see the purple color!

If you tried this on your own, how did you do? If you couldn't do everything yourself, don't worry-- the more you keep doing this, the more you'll remember. If there were parts that you got stuck on, try to keep those in mind, or even write them down in a notebook or digital notes, for future reference.

Now that we have our hero Sass file set up, let's starting adding our hero styles. Going back to the hero.scss file, I'm going to add the selectors for all the hero classes we've created so far. And like we did previously, I'm going to do the split screen thing. In VS Code, I'm going to right-click the index.html file and select `Split Down`. Then in the top half we'll go to the hero.scss file.

Looking back in the index.html file, we have our block, `hero,` which we already have a class selector for. Then we have our `hero__wrapper` div. So in our hero class selector I'll nest another selector and type `ampersand underscore underscore wrapper` which is shorthand for `hero__wrapper`.

Then we'll continue going down the HTML file. The next element is the image tag with the class `hero__image` so in our Sass file under the `hero__wrapper` I'll write another selector nested in our hero block selector, `&__image`.

After the `hero__image` selector, I'm going to add another selector under it, but still in our main hero block class, and write `&__text`. Then for the `hero__title` class, even though in the HTML the `hero__title` h1 tag is inside the `hero__text` div, in our Sass styles I'm going to put the `hero__title` selector under the `hero__text` selector.

If you nested the `&__title` inside the `&__text` selector, the resulting CSS class would be something other than what we want-- it would be `hero__text__title`.

So in our Sass files, we want all the BEM elements, like `hero__image`, `hero__text` -- everything that starts with `hero` and has that double underscore, to be direct children of the block `hero` class selector. After the `hero__title` we need to add `hero__content`, and then last is `hero__button`. And those should be all the selectors that we have, now! So I'm going to close the bottom tab.

Alright, we got our HTML markup added, our Sass partial set up, and our selectors ready to go. Let's check out our design, and then compare it with what we have so far on our website. Here's the design, we have desktop and mobile-- the unicorn image, text, and then buttons.

Now, on our website, we have the unicorn image, and we have the h1 tag which is the right font-family and color, maybe a bit big for mobile styles. And it has a ton of space under it, probably too much. The `hero__content` paragraph under it is way too small. And under that text is the buttons, but they are just the text links, and don't look like buttons yet.

What I usually like to do is start from the top, and first focus on getting things the right size and color. Once those are pretty much set for all elements in the section, then I'll work on the responsive layout between mobile and desktop.

So for the hero, getting the content to be in 1 or 2 columns; and alignment-- like if elements are centered or aligned to one side. Then once that's set, we'll go back through everything make sure all the spacing and everything is correct and matches the design as closely as possible.
