## Menu shadow

In Figma, make sure the background rectangle is selected, and in the right sidebar, towards the bottom, there's an "Effects" panel. And it says "Drop shadow".

If you click the little sun icon on the left, it'll pop up another menu with the settings. And these can correspond to CSS drop-shadow, in the order X, Y, Blur, Spread, and then the color of the shadow.

X and Y control the position, so you can use them to move the shadow horizontally or vertically in relation to the element itself. Then Blur is like you'd imagine, it blurs the shadow so the higher it is the less sharp of a line you'll have. And Spread, which is an optional number, controls how far out the shadow extends from the element, essentially making the shadow bigger.

The naming here is a little confusing when you want to convert to CSS, because these numbers actually correspond to the CSS property box-shadow, not the CSS drop-shadow() function that you can set on the filter property.

The main difference between the two is that box-shadow will add a shadow around the "box" of the element. And drop-shadow(), which is a bit newer can be used to add shadow to box elements, but also to shapes, like SVGs or PNGs with transparent backgrounds. And drop-shadow() doesn't have Spread like box-shadow does. And I think the way they blur looks slightly different.

Again, they're very similar, I feel like box-shadow is currently used more, and I would use box-shadow unless I needed to add a shadow around a shape with a transparent background.

Let's go to VS Code and start adding the shadow in. In the "topnav\_\_menu" selector, I'll add "box-shadow" and we're going to punch in the numbers from Figma, as pixels. So we have 0 for X, 12px for Y, 12px for Blur, and Spread is 0 so I will leave that blank, so we just have the 3 numbers. And then we want to add the color of the shadow.

This is a new color, so I think I'm going to add it to our list of CSS custom properties in colors.scss. In VS Code let's go to colors.scss, and since we're using the "header-bg" for the background, let's add the shadow after it.

So I'll create a new line and create the new property, let's name it "--menu-shadow". And I'll add in the HSL numbers for the color, which is 232, 58%, 35%, and it's at 60% opacity, so we'll add that at the end too.

You might notice that the shadow color has the same hue and saturation as the purple background color above it, but I just decreased the lightness from 55% to 35%, and made it 60% opacity.

Now let's copy that "--menu-shadow" name, and go back to our topnav styles. And in the "box-shadow" property, after the numbers, I'll write "var()" and paste in the name of "menu-shadow". Let's also delete that yellow outline since we don't need it.

And save, and now we have our shadow! So that looks pretty good.

I think now we have all the basic styles set, so let's start working on the animation part.

What I want to happen is that initially, the menu is off screen to the top, and then when you open the menu, it will slide down. When you're moving things with CSS animations, you usually want to use the "translate" property. This lets you move elements horizontally on the x-axis, vertically on the y-axis, and even in 3d space on the z-axis.

We just want to move the menu vertically, so we'll only be using the y-axis.

Just in the browser styles, let's make sure the "topnav\_\_menu" is selected, and I'm going to add "translate". This used to be a function that you'd add in the value of the "transform" property, but they sort of recently broke out all the transform functions into their own CSS properties, which makes things easier if you're working with multiple ones.

In the translate property, initially everything is zero. So I'm going to set it to "zero zero" for the x and y axis. And we don't have to set the z-axis.

And just to demonstrate, let's say we did want to move the element horizontally. If I increase the first number, it stats moving along the x-axis to the right, and if I decrease it, it will move to the left.

Then for the second number, if I increase it, the menu will move along the y-axis down, and if I decrease it, it will move up. Ok, let's go back to "zero zero".

For units, you can use pretty much any length unit. And we know that we want to move the menu up and off screen. Now, as a little mini quiz, do you know what we need to set the second number, the y-axis, in order to move the menu up so it's all the way off screen?

Feel free to pause if you want to try this yourself first.

[ pause ]

Ok, so we know we want a negative number to move the menu up. And we could use pixels and set it equal to the height of the menu but just negative. So it's 442px, so if we set it to "-442px" it will be off screen.

However, the height of the element may change if links are added or subtracted. So in this case it will be more efficient to use a percentage unit. For translate, the percent will be a percent of the size of the element itself. So to match the height, we can set it to 100%, and make it negative, so "-100%".

And now it is off screen. And if I just go into the value and use the arrow keys to increase the number, you can see it starts moving down. And let's go back to -100%. And it looks like the box-shadow is sticking out since it is extending below the menu itself, so let's decrease the number a bit more, with the arrow key. Maybe "-106%".

So that is moving the element off screen. And to bring it back on screen, we can add another style rule to change "translate" to be back to "zero zero".

[ toggle "translate: 0 0" ]

Using translate and moving an element between zero and 100% or vice versa, is super useful and it's the best way to move elements between being off and on screen.

However, we do want to animate this moving, so it's not just suddenly appearing and disappearing. To do this, we'll want to add a transition. So again in our browser styles, let's add "transition" the shorthand property. This takes 4 values to set 4 transition properties.

First is "transition-property", the property that we want to animate. I'll set this to "translate". Then we have "transition-duration", how long the animation will last. I usually start with 250ms or 0.25 seconds.

Then we have "transition-timing-function" which is the speed or acceleration of the animation, and I usually use "ease-in-out" to have it be faster in the middle, and slightly slower at the beginning and end.

We don't need the last property, "transition-delay", since we are not delaying this animation, so we can just leave it as blank and have our 3 values.

Now, if we keep toggling the "translate: 0 0", we can see the menu is moving up and down, as it moves from -106% to 0 on the y-axis.

This seems slightly fast to me, so let's double the duration to make it slower, with "500ms". That's better, maybe let's make it slightly faster, with "400ms". Okay, I'm happy with that.

Now we need to copy these styles and put them in our Sass styles. Initially we want to use translate to move the menu off-screen, so I'm going to copy the first "translate" style, and also the transition. And in our styles, I'll add them to our "topnav\_\_menu" styles.

And we can just remember that when we animate the opening of the menu, we need to change "translate" to "zero zero". You can just try to remember this, or we can also create a comment and write it there, so we'll have it for later.

Alright! I think we're good for the styles, for the menu and how it will get animated.

Next, we're going to actually dive into some accessibility features and add styles to animate the menu.
