## Setup & Pseudo-elements

Alright, let's start by getting VS Code set up. I have VS Code open and I have opened my project folder called "Responsive-Design-Beginners." To do that go to File, Open Folder, and select your project folder.

Once you have your project open, make sure you're running the Live Sass extension by going to the bottom Status Bar and clicking the "Watch Sass" button, and making sure it's running with no errors.

Then you'll want to run the local server by clicking the "Go Live" button. After a few seconds VS Code should open a new browser tab with your local website. And now we should be good to go!

In this section, we're going to be tweaking the Top Navigation links and making them more fancy. Let's go into the Figma design and checking out what we'll be building.

In Figma, in the Top Navigation section, let's take a look at the navigation links that we have on the right. Previously, when we hovered over a text link it would have a solid white underline. But now we have a gradient background with the underline.

This is the only change that we'll be adding, so let's start by getting those colors for the gradient. One trick that I learned recently was that you can immediately click to an individual element without having to double-click to get through all the groups by holding down Ctrl (which should be Command for Mac users).

So I'm going to zoom into the "Pricing" link, then holding down Ctrl. Then when I hover over the gradient underline, a little underline appears, and when you click, it'll go right to that element and select it.

Now in the right sidebar, we should be able to see in the bottom "Fill" panel, a gradient color swatch that says "Linear." Then when I click on the color swatch, in the pop-up menu I can see the colors in the gradient.

It's made up of 2 colors, a teal and a yellow color. I'm going to save each of those as new CSS custom properties in our colors. Let's start with the teal, so if it's not selected you can click that square. Then I'm going to copy the hex color which we will convert to HSL in VS Code.

So copy that, then let's go into VS Code. I'm going to slide down the bottom panel with the Terminal to save some real estate.

And we want to open our colors.scss file. Now, we could go to our Solution Explorer and manually click to open the file,

[ open Primary Sidebar, then close it ]

But, since we know the file name, there's a faster way to open it. Press Ctrl+P to open what's called the "Quick Open" menu, and then type in "colors". And we can then press Enter to open the file. I've been trying to learn more VS Code shortcuts, and I really like this one so I don't have to hunt through the files and folders to find the one I want to open.

In the colors.scss file, we want to create new custom properties for the Top Nav underline gradient colors. In the properties, I'm going to try to keep the order of properties roughly following the visual order in the website.

The Top Nav is the first element in the site, so after the "main-bg" and text properties I have the "header-bg". I'm going to put the gradient colors right after that and before the "hero-bg" since the hero is under the Top Nav.

Let's create a new prop and I'm going to call it "--link-gradient1" since we have 2 colors. And then "colon" and then paste in the copied hex code. Then add a hashtag so it's valid hex color format. And now we have the color, but we want to convert it to HSL. So hover over the color swatch, and then in the color picker pop-up, click the color bar so that it changes to HSL format. Alright, we have the first color, and let's save.

Now let's go back to Figma to get that second color. I'm going to click on the yellow color swatch and in the same way we just did, copy the Hex code. And let's go back to VS Code and we want to create a new property for it.

I'm going to duplicate the line of code for the first color. So put the cursor on the line, and I'm going to use my custom shortcut keybinding, Ctrl+D to duplicate. The default shortcut if you didn't change your keybinding is Alt+Shift+DownArrow since we want to create it below the first line.

Let's change the name of the second property to "--link-gradient2" instead of "1". Then I'm going to paste to replace the HSL color, and add the hashtag in front of the hex code. And then hover over the color swatch, and click the color bar to convert it to HSL. Cool!

Now that we have our colors, we can start creating the underline for the Top Nav links. Let's first go to our website so we can see where we're starting from, and figure out an approach for writing our styles.

Right now, if we hover over a text link on desktop, we have that white underline. Let's inspect one of the links by right-clicking and selecting "Inspect". Then in the style rules, I want to force the hover state so that we can see what styles we have.

So with a Top Nav link selected in the markup, in the Rules I'm going to click the ":hov" label next to the "Filter Styles" textbox. And then check the "hover" state.

Now on the website the underline is visible, and in the styles for the "topnav\_\_link:hover" selector, we can see the hover state styles we initially wrote. Here on hover we are adding an underline that is 2px tall and it's offset 4px down from its normal position.

Unfortunately we can't use this approach for a gradient underline, because a gradient is considered an image that is generated through the CSS styles. And it has to be set on the "background-image" property, which isn't possible in the "text-decoration" style rules.

But we can create a gradient underline by using a pseudo-element. Previously in the course, we've used pseudo-classes to target different states of elements in our styles. For example, the hover state that we've forced here is a pseudo-class.

But pseudo-elements, even though their name sounds similar to pseudo-classes, are a completely different thing. Pseudo-elements don't have anything to do with states, but instead are parts of existing elements that you can target and style in different ways from the rest of the element.

For example, there is a pseudo-element called "first-letter" which lets you target just the first letter of the element. Just for demonstration purposes, if I inspect the Hero Title, I can add a selector for the "first-letter" by clicking the "plus" symbol to generate a new selector for the "hero\_\_title" class. Then in the selector, I'll add a double colon right after with no spaces-- this signifies that it's a pseudo-element, then add the name of the pseudo-element called "first-letter".

And now, in the styles, let's make the first letter really large by adding "font-size: 200px". And the first letter is now 200px, but the rest of the Hero Title is the previous size from our h1 typography styles.

And, if I click off the h1 tag in the Markup View, then click back onto it, the style rule is now in a new expandable panel called "Pseudo-elements".

There are several pseudo-elements. If you're curious to read more, we can search for "MDN pseudo-elements" and if we scroll down you can see the list of all possible pseudo-elements. We can see the "first-letter" one and there's another one called "first-line" which lets you target the first line of an element.

Most of these aren't used very often, to be honest. The most commonly used ones are the "before" and "after" pseudo-elements, and we'll be using the "after" one for our underline. If I click on "before", on the page, MDN tells us that it is essentially the first child of the selected element.

What makes it a PSEUDO element instead of a regular child element is that it doesn't exist in the HTML markup at all. It only gets created if we target the "::before" pseudo-element in our styles. And if we scroll down to the "Syntax" section, this tells us that the "::before" pseudo-element won't get rendered unless we set the "content" property to something other than "none" or "normal".

And, if we go back to the previous web page, and click on "::after", it is very similar to "::before" except that when it's created, it acts as the last child of the selected element. We'll be using the "::after" pseudo-element to create our gradient underline.

If we go back to the design, the underline is below the text link, so it makes the most sense to use the "::after" pseudo-element for it since it is coming after the main element.

So, that's the basics of pseudo-elements. Next up, let's start creating this underline.
