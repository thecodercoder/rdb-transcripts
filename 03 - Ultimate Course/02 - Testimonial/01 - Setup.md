# Setup

In this section we're going to be making some changes to the Testimonial section.

If we look at the design, it looks very similar to what we currently have, but the colors are different. On our website now, we have a white background, the quotation mark images are teal, and the text is the dark gray.

However in the new design, we kind of have a dark theme going. The background color is the blue-purple color that we have in the header and hero, the quotation mark images are a white color with 50% transparency, and the text is white.

The reason I made this design change is because under the Testimonial section, we're going to be adding a new Blog Post section. And color-wise, since the Alternating Features section has a white background, and the Blog Post section will have a white background too, it made sense to make the Testimonial section between them have a dark background color. Just so things look better design-wise.

And we're not just going to change the Testimonial colors and be done with it-- I'm going to create a color theme for this new design. Where just by adding a helper class to the Testimonial section tag, it will change all the colors in the section.

This theming is something that can come in really handy if you want to have multiple styles available and you might be switching between them. And, we'll be setting up this theme with CSS custom properties in a way which I think is a little more organized and easier to read.

Let's take a look at our current website, and figure out how we want to map our colors out.

The background color we'll set on the "testimonial" class in the section tag. Then for the text, we can probably also set the color property also just in the "testimonial" class, since the h2 and paragraph tags will inherit that color.

Then the other color we need to set is the quotation mark icons. Right now, we built those as image tags, but I think that we're going to want to change those to inline SVGs, like what we did in the footer with the social media icons.

This will let us change the color of the SVG just in our styles, without needing a whole new image for the different colors. Okay, so that's three colors we'll need to set up.

Now let's go to VS Code, and first go to the colors.scss file. So far in our website, we've been putting all the colors into global CSS custom properties that we've set on the ":root" pseudo-class. And this works just fine.

However, if you end up working on a really large website with lots of pages and different components and styles, at some point, you might want to start separating out the colors into the components that they're being used in.

So what we're going to do is create the Testimonial colors as custom properties, but instead of setting them on the ":root" element, we'll create them in the "testimonial" class.

Limiting the scope of these custom properties to the Testimonial section means they can't be used outside of it. But that is perfectly fine for our purposes here.

In our "testimonial" class, I'll start with the background color. Let's call this "--testimonial-bg". And initially, I'm going to set this to be our current color of white. So let's go to the colors.scss file, and I'm going to reuse the "main-bg" color since this is what we're using as the default background color on the website.

So I'll copy that, and then back in the Testimonial styles, we'll load that "--main-bg" color with the var() function, and then paste it in.

Next let's create the text color. I'm going to call this "--testimonial-text". And it's the dark gray that we've been using on the site, so let's go to colors.scss, and copy the "text-dark" custom prop, and paste it in a var() function.

Okay, the last color we need to set is the quotation mark images. Let's create our custom prop and call it "--testimonial-icon".

Then we need to get that teal color. In our colors, even though the teal color is used in some other places, like the "button-primary-bg" and in the gradient, I don't feel like they're related enough to the quotation mark image color to reuse those custom props. So let's go to the actual SVG file to get the color itself.

I'm going to use the Quick Open menu, and type in "quotation-mark" and go to the SVG file. I'm going to wrap the lines with Alt+Z.

And, in the path element, at the end is the "fill" color. So I'm going to copy that hex code, and paste it in as the value for the "testimonial-icon" color. And let's convert it to HSL, by clicking the color swatch, and clicking the title bar.

Alright, we have our colors, now let's actually use them in our styles. The background color I mentioned we want to set it on the "testimonial" class section tag.

So under the custom props, I'm going to add "background-color" and then set it to "var(--testimonial-bg)". Next I'm going to set the text color with "color" and then we'll set it to "var(--testimonial-text)".

And let's save our changes. Right now, we haven't actually changed any colors, and it might seem redundant that we're adding more styles setting the background color and text color to the same colors they were before.

But this will make sense once we build out the dark theme styles, which we'll be doing next.
