## Basic styles

The first thing we need to set up is creating a Sass partial for the blog styles. So I'm going to open up the sidebar and we probably want to put it in the "scss/components" folder, so let's right-click the "components" folder and create a new file. And I'll call it "blog.scss".

Then we'll want to go to the index.scss file, and forward it -- let's put it after the testimonial. And I'll write "@forward 'blog'". Alright, and we can close that.

Now in the blog.scss file we need to load our util styles with "@use '../util' as u". And let's start adding our selectors. I'm going to right-click the blog.scss tab and select "Split down" and then on the top half go to the index.html file.

First we'll start with the "blog" BEM block name class, then "blog\_\_wrapper", then "blog\_\_grid", "blog\_\_item", "blog\_\_image", "blog\_\_filter", "blog\_\_text", "blog\_\_title", and then "blog\_\_meta".

Okay, that's good. And we can close the bottom duplicated tab. Now let's start with just the blog card styles, we'll do the layout styles later once we have the card figured out.

In the design, we have everything stacked on top of one another. And instead of doing this with position absolute, I think this would be a good place to use CSS grid to stack the elements in the card.

Going back to VS Code, to do this, we're going make the card, or "blog\_\_item" class element, a grid parent, with 1 column and 1 row. And then we're going to place each of the grid children, the image, filter, and text, in the same cell. This will make them stack.

Alright let's start. So in our styles, the card is the "blog\_\_item" selector, so in there I'll start writing "display: grid". And we want 1 column and 1 row-- we can actually write this with the shorthand property "grid-template". This property lets you set grid-template-columns, grid-template-rows, and grid-template-areas all at the same time.

Let's set it, so first is the rows, and we just want one set to "1fr". Then if we add a forward slash, we can add the grid-template-columns. And again we just want one set to "1fr".

Now, if we save, let's see what our website looks like. Let's turn on the grid highlighting for the "blog\_\_item". And, in the "Layout" tab, in the grid diagram, it looks like there's two rows.

If I highlight the grid children in the markup, the blog\_\_image is on the first row, then the blog\_\_filter is technically on the second row, but because it's empty it has zero height. Then the blog\_\_text is on the third row.

Since we didn't place the children in the template explicitly, the browser by default will put each child in their own row. So going back to our styles, we need to place all the grid children in the first cell of our grid template.

We could do that using each of the child selectors, however since they are all going to have the same value, I think it might make more sense to create a direct child selector for the "blog\_\_item", which would target all the grid children.

Let's try that. In the "blog\_\_item" selector, I'm going to nest the direct child selector with right angle bracket and then the wildcard to target any element. Then, in the styles we want to assign all the children to be in the first cell of the grid template, meaning in the first row and the first column.

If you want to try this yourself, pause the video here, and then you can unpause when you're ready to see how I did it.

[ pause ]

Okay! Let's first place the children in the first column. I'm going to do this with "grid-column" and have it start at 1 and then forward slash and have it end at we could say 2 but since we're making it go to the end of the template I like writing it as "-1".

Then we're going to do the same thing with the rows. So I'm going to duplicate that line, and then change the "grid-column" to say "grid-row". Alright, let's save!

Alright, on our website now all the card content is in the same cell of the grid template.

Next up, let's get the photo filter working. Going back to Figma, let's see how the gradient and everything is set up. If I click into one of the images until I get to the "Blend Overlay" layer, in the right sidebar let's click on the gradient swatch.

And Figma has added some pretty cool info about the gradient, including the color stops so that we don't need to guesstimate anymore. So let's have VS Code on one side, and start adding this gradient.

In our styles, we'll be adding them to the "blog\_\_filter" selector. Linear gradients are added on the "background-image" property, and then use the "linear-gradient()" function. And in the function, we want to first load the direction of the gradient.

This one is going from left to right, so we could either write that as "90deg" because 0 degrees goes up vertically, kind of like analog clock hands at the12 o'clock position. So 90 degrees is one quarter after that. Or we can use the shorthand keywords "to right" which is my personal preference, and then add a comma.

Then we need to load the two gradient colors which we saved as CSS custom properties. If we go to the colors.scss file, we have the "blog-gradient1" and "2" custom props. So I'm going to copy the first one, then go back to our blog styles and in the linear-gradient() function write a var() function and then paste it in.

And if we reference the linear gradient pop-up in Figma, the color stop is 30%, so after the var() function we can add a space and then write "30%" and then a comma.

Then we can add the second color. I'm going to copy our first color and the color stop, then paste it after the first color. And we want to change the color name to "2" instead of "1".

And actually for the color stop it's at 100% which is the default for the last color, so we can delete the color stop number. And let's save and see how the website looks.

Cool, so we can see our gradient, and it does seem to be going in the right direction. However at the moment it's covering up the photo. This is because we haven't added the "mix-blend-mode" to it yet.

This is something that you can actually set in Figma. So in the linear gradient pop-up menu, there's this little droplet icon on the right side under the close button. If we hover over it, it says "Blend mode".

And if we click it, we can see all the different options. Currently we have "Lighten" set, so let's put that into our styles. In VS Code, in the "blog\_\_filter" styles, I'll add "mix-blend-mode" and set it to "lighten".

And now, on the website, we can see that the gradient is semi-transparent and we can see the photo through it, as if it was a filter. Mix-blend-mode allows you to make an element visually blend with its background in different ways.

In the browser styles, you can click into the value and if you backspace to delete, you can check out all the different options and see how they look. I don't fully understand all the different filters and what they do, but just aesthetically I liked the look of "lighten" for the design.

And the image does now look similar to what we have in Figma, so I think we're good on that front.
