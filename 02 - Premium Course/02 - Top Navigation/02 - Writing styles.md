## Writing the styles

In the design, let's zoom in to the underline and get the sizing and spacing so we can put it in our styles.

If I hold down Ctrl and select just the underline, it tells us that in addition to being a gradient background, it is 3 pixels tall. And if I hold down Alt, it is 3 pixels below the text link.

Now we have the information we need to start building the underline. Let's go back to our website first, to figure out what element we need to target in our styles to contain this "::after" pseudo-element.

You can pause the video now and inspect the website, and decide which selector we need to target for this.

Ok, so I'm going to inspect one of the text links, and I think we should target the "topnav\_\_link" anchor tag. Let's go into VS Code, and we'll want to open our Top Nav styles.

Again, instead of searching through the sidebar to find the file, I'm going to open the Quick Open menu with Ctrl+P, and then type in "topnav" and just make sure that the path is correct and says "app/scss/components/topnav.scss". Then press Enter and open the topnav.scss file.

And if we scroll down, to "topnav\_\_link", we can see our ":hover" pseudo-class that we used. Since we don't need the text-decoration styles anymore, let's delete those but we do need to keep the hover state pseudo-class.

Now, the question is where to create our pseudo-element. We could create it in the hover state, but I also want to fade in the underline instead of it just appearing immediately. And we can't do that if the pseudo-element only exists in the hover state.

So what I'm going to do is create it in the "topnav\_\_link" selector, and then we'll fade it in using the opacity property in the hover state.

To get started, in the "topnav\_\_link" after the desktop media query, I'm going to create the pseudo-element. First let's add an ampersand since the pseudo-element is on the main element, then add a double colon and the name, "after".

Now, the first thing you should do in the "before" or "after" pseudo-element is add the "content" property. You can use this to display text or symbols as the content, but since we don't need any of those I'm going to set it to an empty string with two quotation marks. Again, it's very important to have the content property because it won't exist if you don't, even if you add other styles.

Now, we need to style what we want the underline to look like. Since it is a gradient, and the gradient needs to be set on the "background-image" property, we need to create an element that is the size of the underline. So 3 pixels tall. I'm going to add "height: 3px".

Pseudo-elements by default will be "display: inline", so if we want to be able to control the height, we need to change it to "display: inline-block" or "block". I usually just set it to "block" so that it will default to 100% of the parent's width to be the same width as the text link.

Next, let's start adding the linear-gradient. I'm going to set it on the "background" shorthand property just to use a shorter name as opposed to "background-image". And as the value to create the gradient, we'll add the "linear-gradient()" function, and to start let's add the 2 colors of the gradient.

In the parentheses I'll add the first color. It's a CSS custom property so I'll write "var()" and then we need the name of the custom prop we just created. We can check in the "colors.scss" file, and it's the "--link-gradient1" color.

Let's copy that, go back and paste it in the "var()" function.Then for the second color, we'll add a comma, and I'm going to copy the first "var()" function and paste it in, then change the number to "2".

We haven't set anything like the direction of the gradient or where each of the color stops are. We'll get to that-- right now I just want to make sure that the underline is showing up in the first place.

I'm going to save, and let's check out the website. Alright! We can see the underline is indeed showing up. If I inspect the link, in the Markup View we can see under the text of the link it now has the "::after" pseudo-element.

If we click on it, then we can see the Rules. We can see the "height: 3px" is grayed out and the tooltip says it's not having an effect because the element is display inline. But I think that might be a bug because we're on the anchor link itself but it is showing the pseudo-elements that it's a parent of. And we did set "display: block" on the pseudo-element. So I think this is just a bug because the underline is showing up.

In the Markup View, let's click that "::after" element. And now in the Rules everything looks fine.

This is a great start. We do need to tweak the linear-gradient. Right now it is not going in the right direction because by default they will go from top to bottom. If I click into the height and increase it, you can see it's going from top to bottom.

We'll need to change that-- we can set it to "to right" so that it will move from left to right. Let's go to VS Code, and in the "linear-gradient()" function before the colors we can set the direction. I'm going to use the keywords "to right" instead of degrees or other ways we can set the direction because it seems simpler.

Let's save, and back on the website, the gradient looks a lot closer to the design! I do want to double-check the design to make sure the color stops are at the correct percentage. By default they're going to be the first color on the left at 0%, and the second color on the right at 100%.

I'm going to go into Figma and look at the gradient. I'm going to hold down Ctrl and hover over the underline until it's highlighted, then select it. And in the "Fill" panel let's click on that color swatch and check out the gradient.

The first teal color on the left is all the way to the left at the 0% percentage, so that's good. The second color however, isn't all the way at the right at the 100% location. It's a bit short, so we just need to eyeball about where that is, maybe around 75%? Let's try that to start.

Going back to VS Code, we don't need to set 0% for the first color since it defaults there already. For the second color, we want to add the percent after the second color. So I'll add a space and then "75%".

Now let's go back to the website, and the underline looks pretty good. Let's try clicking back to Figma and get out of the menu. If I go back and forth and eyeball where that yellow starts, it looks like there's more yellow on the website compared to the design. So I think we should start the yellow later, a bit closer to 100%. Just in the browser, I'm going to click in and use the up arrow to change it to 80%.

Now if we compare the design to the website, I think that's a little closer, and good enough. Let's update our styles. In the topnav.scss file, I'll change that 75% to 80%. And save, and now the gradients look pretty good!

Ok, I'm kinda going back and forth eyeballing the design versus the website to see how close to the design we are. This is a bit more nitpicky, but it looks like the underline is farther away from the text on our website compared with the design.

In the design, the text link is 16px tall due to the line-height being 16px which is what the font-size is. And the underline which is 3px tall is also 3px under the text link. And if we select them together, they have a combined height of 22px.

However on the website, if I inspect one of the links, it is 33 pixels tall. Let's figure out where this difference in height is coming from. The first thing we want to check is the font-size of the text links. In the "Computed" tab, the font-size is 16px. And it looks like there is no line-height set in our styles, so this means the line-height will use browser defaults, which is usually a bit larger than the font-size.

Let's try setting a line-height of 1 in VS Code. In the "topnav\_\_link" class selector, under the "font-size" style, I'll add "line-height: 1" so that it will be 16px. When we save, on our website it looks like the height is still the same, 33px.

So the height is coming from something else. In the Rules, I do notice that the "topnav\_\_link" anchor tag doesn't have a "display" property set, so that means it's defaulting to "display: inline". This could be affecting the height, so one fix I try in cases like this is setting the anchor tag to "display: block" which helps get rid of other factors that may be affecting the height of inline elements.

Let's try that. In VS Code I'm going to add "display: block" at the top of the styles, and save. And now on the website the underlines are a lot closer to the text. And if I inspect one of the Topnav Links, it's 19px now instead of 33 like before.

This is good. Now let's try adding the 3px of space between the link and the "::after" pseudo-element. In our styles, in the "::after" selector, I'm going to add "margin-top: 3px".

And I am using pixels for both the height and the margin-- just because they're small sizes and they aren't text elements that need to be in rems if the browser base font size increases, so I think it's a bit simpler to just say pixels. And it won't affect readability of any text.

Now the website looks good, we have a little bit of space between the links and underlines. And the whole anchor tag is 22 pixels tall now, which is what we had in the design.

So that's the basic underline styles working. Now we need to control the hover state, so that the underline isn't visible by default, but will fade in when you hover over the link.

Since we want to fade in, I think the best way to do that is to initially set the opacity to zero, then on the hover state, change the opacity to 1. And we'll add a transition to animate the fade.

Let's go back to VS Code, and in the "::after" pseudo-element, I'm going to set "opacity: 0". And in the hover state selector, we'll need to add a nested selector for the "&::after" pseudo-element selector. And in it we'll change "opacity" to be "1".

Also, since this is the only thing going on in the hover state for the links, we can get rid of the nesting so the selector reads "&:hover::after". Just to be a bit cleaner.

Let's save and check that the opacity changes correctly, before writing the styles for the fade in. I try to just change one thing at a time when I'm writing styles, so that I can make a small change, then confirm it on the website before moving on. Because if you write a whole bunch of things and then something's not working, you'll have more to go through to double-check. I find it better overall to make these small incremental changes one at a time.

On the website the underlines are there but they are not visible. And if I hover over the links, the underline appears! Awesome.

Now that that's working let's go back to our styles and add a transition to fade in the change. I want to add the transition on the element that is changing opacity, which is the "::after" pseudo-element.

I'll add it at the bottom, and let's use the "transition" shorthand property. First we want to write the property name that we are transitioning, which is "opacity", then add a space, and let's set the duration or the length of the animation. I usually start with 250ms.

Then add another space, and we can set the easing which controls how fast the animation starts and stops. I like using "ease-in-out" to have the animation a bit slower at the beginning and end, and it speeds up a bit in the middle.

Let's save that, and now on the website, if I hover over the links, the underline smoothly animates and fades in and out. That looks good!

Alright, so that's it for the animated underline. And that's also the only thing we're changing in the Top Navigation, so this section is basically done. We're just starting out with something a little quicker. The next section, the Hero, is going to have a lot more changes.

Before we go to the Hero, let's commit our changes in GitHub. So go to your GitHub Desktop App, and in the project repo we want to eyeball the files that are getting changed. That all looks pretty good. So let's write our commit message-- I'm going to say "Top Nav add animated gradient underline". And then press the button to commit the changes to the main branch.

Next up, we'll be making changes to the Hero section!
