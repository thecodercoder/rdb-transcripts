## Prep and markup

In this section we're going to be adding to our Top Navigation-- we'll be building a hamburger menu for mobile devices with some JavaScript, and we'll also make the top nav sticky so that it's still visible after scrolling down.

Let's first check the out the design, so we can figure out what we need to do. In Figma, I'm going to zoom in on the mobile part. And we can see that instead of having the 3 text links we have a hamburger icon on the right side.

Then the frame next to it shows the open hamburger menu with the navigation links. We'll probably animate it coming down from the top, like a drawer opening. And we have a close button in the top right. And the rest of the website is covered in a transparent overlay.

We do need to export the hamburger and close button images from Figma. So I'm going to select the hamburger button, then on the right sidebar scroll down to the "Export" panel, and let's export it as an SVG. Then I'll select the close button, and do the same thing to export it as an SVG.

And let's get those files, so I'll go into the File Explorer, and in the Downloads folder I'll select both files and copy them, then go to the project folder which I have here, and we want to paste them in the "img" folder.

Alright, we have our images, and now let's get our markup set. We'll be adding the hamburger and close buttons, and we'll also have to rework some of the markup for accessibility purposes, which we'll get into later.

In VS Code, I'm going to go to the index.html file, and look at our current markup for the Top Navigation. That's going to be up at the beginning, and everything is in the header tag.

We have our hidden header H2 tag, then our wrapper div, and in it we have our homepage logo link, and a nav tag, which contains the list of navigation text links.

And one thing to note is that we have a new text link that says "Home", which will let you navigate to the homepage if you're on a different hypothetical page.

Everything we're going to build will be in the nav tag, so that includes the hamburger button to open the menu, the close button, and then of course we have our links.

Now, if we look back at the design, initially the links and close button are not visible. And when the menu is opened, they are visible, and the rest of the regular website content is not accessible.

So, going back to VS Code, I'm going to create a new div in the nav tag to contain all the content that's in the menu itself-- just so we can target that div to either be hidden or shown, depending on if the menu is opened or closed.

In the nav tag, I'll create a div, with a class of "topnav\_\_menu". Then I'll move the unordered list into the div. And let's create that first "Home" link. I'll select the "Features" li-tag, duplicate it and change the first text to say "Home".

We also need to add our open and close buttons. The open button will not be in the "topnav\_\_menu" but outside it, so that it's visible initially.

So before the "topnav\_\_menu" div I'll create a button element with a class of "topnav\_\_open", and in the button we want to load the hamburger image, so I'll create an image tag, and set the source to "/img/hamburger.svg".

I'm leaving the alt attribute blank, because we're going to make the button itself accessible to screen readers, so we don't need to do the same for the image.

But we do want to add the width and height attributes, so I'm going to open the SVG file with the Quick Open menu, Ctrl+P, and type in "hamburger" and select "hamburger.svg". And let's copy the width and height, and paste it inside.

And let's create our close button. I'm going to save a little time and select the open button, press "Copy", and then in the "topnav\_\_menu" div, paste it before the links, since it's going to be at the top of the menu.

Then let's rename the class to "topnav\_\_close", and delete the "hamburger.svg" file name, and start typing "close" and select "close-button.svg".

Let's get the width and height too, so I'll use the Quick Open menu, type in "close" and open the "close-button.svg" file. And I'll copy the width and height, and then back in our markup paste it in.

Okay, that's pretty good for the markup for now. Let's save and see how the website looks. And we can see our two buttons-- they have that browser default gray color. But everything is showing up, which is good.

Next, let's start writing the styles for the hamburger menu.
