## Dark theme

We still need to set up the quotation mark image color. First we need to go to the index.html file, and change from using an image tag for the icons to inline SVGs.

So here is where the image tag is, and let's get that SVG code, which we should still have open. And then in the quotation-mark-teal.svg file, I'm going to select all and copy. And then back in our HTML, I'm going to paste it in [ before ].

Alright, on the website now we have 2 copies of the first quotation mark image. We want to keep the class, so I'm going to copy that and paste it in the SVG, and then I'm going to delete the image tag. And now we have just one first quotation mark. And that looks good!

When we had the image tag, since the image is more decorative, we left the alt text a blank string so screen readers will ignore them.

But with inline SVGs, we have to do something a bit different since they don't have alt text. If you did have alt text, you could add it in a "&lt;title>" tag inside the SVG. And if you want screen readers to ignore the SVG, what we can do is add an attribute called "aria-hidden" and set it to "true". So I'm going to do that.

Let's do the same thing for the second quotation mark image. I'm going to copy the SVG code, and then I'm going to replace the second image tag with the SVG again.

And when we save, everything looks good! Okay, now that we have our markup set, let's go back to our styles. And I need to map the fill color of the SVG path to our custom property.

The quotation mark images are in the "testimonial\_\_icon" selector, we can add it there. So the SVG tag itself is what has the "icon" class. And the path element is a child element in the SVG tag.

So in our styles, I'm going to add a child selector with the "path" tag. I'll add it after the media queries-- I'm going fold them both up so we can see everything better. Then after them I'll create a new selector for the path, and in it, we want to set the "fill" property, and set the value to "var()" and in it, "testimonial-icon".

Let's save our changes. Again, we haven't changed any of the colors yet. To set up our dark theme for the Testimonial block, I want to put those styles in a utility class that we will add to the "testimonial" class section tag.

Let's go back up to the top of the file. And under the background-color and color styles, I'll create a new selector, and I think we need the ampersand and then "dot dark" since we'll be adding the "dark" class on the "testimonial" section tag too.

In here is where we're going to make our custom property magic happen for the theming. Instead of writing another copy of the "background-color" and "color" and the "testimonial\_\_icon path" style rules, instead we're going to change the value of the CSS custom properties here.

I'm going to actually copy the three custom properties we created, and paste them in the "dark" class. And here we will change the colors to the colors from the design.

So the "testimonial-bg" we want this to be the blue purple color. If I go back to the colors.scss file, I think we'll just copy the actual HSL color, just because the other places it's used is header and hero, and we probably want to keep those separate.

I'm going to copy the value, "hsl(232, 58%, 55%)", and then in our testimonial styles, I'll paste it in as the value for the dark "testimonial-bg" custom prop.

Next up, we want to change the text color from dark to white. And I think we can use the existing "text-light" color since it does make sense that we'd want it to match in the Testimonial section. So we'll copy "text-light" and then paste it in to replace the "text-dark".

And lastly we want to change the icon color from teal to the semi-transparent white. I don't think we've used that color anywhere else, so let's go back to Figma and get that color.

In Figma, if I select the quotation mark icon, and in the right sidebar in the "Fill" panel, I'll click that color swatch, and it tells us the HSL color, so let me put the code on the left side so we can copy it over.

So in the hsl() function, it'll be "0, 0%, 100%" and then I'll add "50%" for the opacity. And I'm going to change the HSL to be HSLA.

Alright, so that's all the colors. Now let's see if our theming will work. In the index.html file, we want to add the "dark" class to the Testimonial section tag. And the order doesn't matter, but I'm going to add it after the "testimonial" class.

And when we save, on the website, we have our new theme!

That works pretty well. Going back to our styles, we did need to put in a bit more work to create the custom properties and everything, as opposed to you know, just changing the colors in the style rules without all the custom props.

And that would be fine, but if you are working on a website that has blocks where the designers does want different themes, it might save you time in the long run to set up the theming and tie it to a helper class.

One reason why this can be helpful is that you can quickly switch between themes just be changing the class name. And also, if you have the website in a CMS, a content management system like Wordpress or something else, then whoever manages the content of the website can more easily make changes themselves without being dependent on a developer.

Once everything is hooked up in the CMS, they could potentially change the CSS class of the element in question in the CMS without needing you, the developer, to go in and write new styles and have to redeploy everything.

Obviously, this is more for if you're working on larger projects with a bigger scale. But I also think it's nice from just an organizational standpoint.

Imagine if instead of one dark theme you had like 3 or 4 different themes. Instead of having to keep rewriting all the styles and selectors in each utility class, you just have to change the value of the custom props, so you save a bit on lines of code that you have to write.

Cool! So I think we are good on this Testimonial theming. I know the website looks kinda weird now because we have the blue purple and then the full-width CTA which is also kinda blue. But next up we're going to create the new Blog Post section between the Testimonial section and the Full-width CTA.

Alright, so let's commit our changes. In GitHub Desktop, we'll eyeball all the files with changes, and that looks good. So I'll write a commit message, "Testimonial dark theme". And then select "commit to main" and then "push to origin".
