# Styling the navigation links

Let's start adding our styles for the top navigation. Since I created the `topnav` class to serve as the BEM block, I want to create a Sass file that uses the same name.

If we look at our scss folder in VS Code, the styles for the top nav don't quite fall under the `globals` or "Layout" or `util` styles. The top navigation is one section of the website, and styles there will be used just in that section, and are unlikely to be used outside the top navigation section.

You can divide up the website into these different sections, and some people call the sections "components." So I'm going to create a new subfolder in the scss folder called `components`, for the top nav styles, and we'll be adding more component styles as we continue building the different sections of the website.

And since we created a new scss folder we'll need to create a new `_index.scss` file to load all the other partials from this folder.

We'll also need to forward the components styles in our main style.scss file. So let's open that and add a new at-rule, `@forward 'components'`, just like we did for the globals and layout folders.

Then back in the components subfolder, I'll make a new file, `_topnav.scss` and I'll forward it in the components index.scss file. And, in the topnav.scss file we'll most likely need access to our util functions and mixins.

Do you remember what we need to add here? If you want, I recommend pausing the video to see if you remember how to do that.

And as always, don't worry if you don't remember the code-- we've done this before, so you can always look in another similar file to see how we did it. Ok, pause the video, and we'll see you in a bit!

Ok, and we are back. At the top of our topnav.scss file, I need to write the `@use '../util' as u` at-rule to load everything from the util subfolder and we're giving it the namespace `u`.

Now let's start writing the selectors to match all the classes for topnav elements that we have in our index.html file. We need our block class, `topnav` as the first selector. Then nested in it, I'll add the selector for the `&__homelink` class, then the `&__logo` class, then `&__links`, `&__item`, and `&__link`.

Now, even though we haven't added any styles yet, let's look at our website and see what it looks like to start out. So in our website we can see our links, and they have that bullet because we are using an unordered list, and by default they will be bulleted items.

The logo is there, and it is loading the SVG file, but since the logo is white we can't see it.

So first things first, let's add that purple background color to the header tag, which has the class `topnav`. I stored all the colors as CSS custom properties in the globals/colors Sass file, so let's take a look at that.

Ok, the purple color was stored as `--hero-bg` and it's used in both the header and the hero. I think I might duplicate it and create a separate custom prop for the header-- just in case the design ever changes in the future and the header and hero need to be different colors.

So I'll duplicate that line and then rename the first one to `--header-bg`. And let's copy it. Then back in the topnav.scss file I'll set the background-color of the topnav block to `var(--header-bg)`.

Now when we look at the website, we can see our logo SVG image and the links!

Next, we need to style the list items so that they match the design. Lists have a lot of default styles that the browser will automatically add, so we will need to cancel them out in our styles. One is the dots which are the bullet points that are a default style that comes with using an unordered list. The property that controls the bullets is `list-style-type`. So just in our browser styles, let's add `list-style-type` and set it to `none`. And now the bullets are gone.

Let's look at what other styles we might need to cancel out. If we inspect the ul-tag, and hover over it, it looks like there are top and bottom margins, and then some left padding. These default browser styles can be a bit tricky, because they won't actually show up in the "Rules" tab of your code inspector.

If we scroll down the Rules panel, there are no rules displaying for margin or padding of the ul-tag. But if we click on the "Layout" tab, we can clearly see a top and bottom margin, and a left padding. So we want to zero all those things out for the ul-tag. In our browser styles for the ul-tag, let's add `margin: 0` and `padding: 0`. And you don't need a unit when the value is 0 because zero is zero no matter what.

So this looks pretty good-- we've gotten rid of that margin and padding. We'll have to keep adding styles to the top nav items, but for now let's add these style rules to our code. I'll copy the styles, and we want to add them to the ul-tag which has the class `topnav__links`. In VS Code in our topnav.scss file, that will be in the `&__links` selector, since the ampersand symbol loads the parent selector, the `topnav` class.

We can paste the style rules there, and now when we save and recheck the website, we can see that we don't have bullets, and there are no extra margins or padding!

We also need to fix the text styles of the top nav items. Since the list items in the navigation are links, they have that purple default color. And we probably need to add other text related styles.

Let's refer back to the design to see what styles we need to add. In Figma if we select a top nav item, it tells us that it is bold and `16px` and is white. There's also a 5% letter-spacing-- the percent thing is a Figma way of saying letter-spacing, but it won't work in CSS, so we'll need to see how to write in CSS if we click on the "Inspect" tab. It's telling us that the letter-spacing is `0.05em`.

Since it is in em units, that means the letter-spacing will be dependent on the font-size of the text itself. If you want to do the math to figure out what it ends up being in pixels, we can pull out our calculator, and put in the font-size of `16px` and multiply it by `0.05`. And the result is `0.8px`. We'll still just use the em units in our styles, because if the font-size ever changes, the letter-spacing of `0.05` will scale up or down based on the font-size, so we won't have to change the letter-spacing.

Now we need to figure out which selector we want to add the style rules to. In our index.html file, the links are in the a-tag, with the class `topnav__link`. Again, I've used `links` plural to refer to the entire group of links, and `link` singular for each individual link. In our topnav.scss file, the selector for the `topnav__link` class is `&__link`.

First let's add font-size, and set it to `u.rem(16)` using our `rem()` function. And we'll need to set font-weight to `700` which is `bold.` I generally like using numbers for the font-weights, where 400 is Regular and 700 is Bold. But you can use the keywords if you prefer that-- I think they're pretty much the same. And for the letter-spacing, let's add the rule `letter-spacing: 0.05em`.

Let's see what we got on our website, and then compare with the design to see what else we need to change. Ok, so one big thing we need to do is that in our design, the top navigation links are all uppercase. While you could just use all caps when typing out the link text in the index.html file, you can also control the capitalization with CSS.

Let's go into our code. And in our `topnav__link` class selector, if we add a rule that says `text-transform: uppercase` it will accomplish the same thing. I like doing it this way because if the design ever changes and they get rid of the uppercase thing, it's less work to remove that one rule rather than having to manually retype every single navigation link text. And now on the website, all the links are uppercase.

Lastly, we need to set the color to white. Right now they have the purple link color from the browser default styles. Let's check the color custom properties that we created in util/colors.scss. And it looks like we'll need to use `--text-light` for that. Back in topnav, we'll add `color: var(--text-light)` to the `&__link` selector. You want to make sure that you change the color on the a-tag selector, since that's where it gets the default color from in the browser. If you change the color on the li-tag by mistake, it won't affect the color.

Now when we look at the website, the link text styles look like what we have in the design! Of course, they're simply stacked one on top of the other, so next up, we will have to write styles to control the layout of all the top navigation elements-- the logo and the links.
