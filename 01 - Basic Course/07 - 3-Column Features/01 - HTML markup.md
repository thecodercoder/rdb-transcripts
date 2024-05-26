# HTML markup

In this section we're going to build the 3-column features section under the hero. Let's first study the design in Figma and decide how we're going to build this.

In Figma, we see the features section has 3 features, and each has an icon, title, and a description. And if I click on each feature they are all the same width, [XXX].

Now let's export the icon images as SVGs. Again, SVGs are the best type for these icons since they are solid color, simple shapes. I'm going to double-click on the first asterisk icon until it is selected, and in the left sidebar you can see the layer "icon-asterisk" is selected.

Then I can select multiple elements by holding down Shift, and then double-click on the next icon, the bell shape, and checking in the left sidebar that just the layer "icon-bell" is added to the selection, and then, continuing to hold down Shift, double-clicking the last icon, the speech bubbles with the dollar sign, and checking that the layer "icon-payments" is selected.

Then in the right sidebar in the "Export" panel, select "SVG" and then "Export 3 layers."

Now I want to move the exported files from my Downloads folder to my "img" folder in the project folder. If you export multiple layers at once, Figma will put them in a zip file with the same name as the Figma file itself. So if I go into the "Core Responsive Design Beginners" zip file I'll select all the SVG files and copy them with Ctrl-C, then paste them in my project's "img" folder with Ctrl-V.

Also, if for whatever reason you can't get the multiple exports thing to work, you can select each icon individually and export each of them individually, and that's totally fine.

Ok, now that we have our images, let's start writing the HTML markup! Going into VS Code and the index.html file, let's figure out where to put the HTML for the 3-column features section. As a quick refresher, so far in the body tag we have an article tag that's meant to contain all of the main content of the website. We put the hero markup in a section tag within the article tag, and we'll do the same for the 3-column features section since it is part of the main content too.

We need to find the closing section tag of the hero, and under that I'm going to start a new line and add a section tag by typing in `section.features` to use the Emmet shortcut, and then Enter or Tab to add the tag. Like we did with the hero, the section tag's class, `features` is what we're using as the BEM block name.

Then in the features section tag, again following the same pattern as we did in the hero, I'll create the wrapper div by typing `.wrapper.features__wrapper` with no space between `wrapper` and `features__wrapper` so that both classes will be in the same div tag. And press Tab or Enter to add the tag.

Now we can start adding the features content inside the `features__wrapper` div. I know that I'm going to be using flexbox or grid to layout the 3 columns, and I think I can use the `features__wrapper` as the parent flex or grid element. So I can go ahead and start creating the markup for each of the three child elements.

Inside the `features__wrapper` div I'll add a new div for the first feature item, and I'll call it `features__item`. And this is following the BEM approach with the block name `features` then a double underscore and the element name, `item`. Then in the `features__item` div, I'll start adding the content for the feature.

First I'm going to add the icon as an img tag, by typing `img` and then give it a class with a dot of `.features__icon`. The source will be `/img/icon-asterisk.svg`, and I'm going to leave the alt text as empty with just the 2 quotation marks, because the icons are purely decorative images, and don't actually convey any information. For these types of images, you want to have the `alt` attribute but with an empty value like this, because if you leave out the `alt` attribute completely, some screen readers will read the filename, which is unnecessary and could be annoying for screen reader users.

We do need to add width and height attributes so the browser knows right away how much space to leave for the image while the image is loading, and avoiding that layout shift that we talked about when we set the top nav logo image. Let's go back to Figma to get the sizes, the asterisk is 43 pixels wide and 48 pixels tall. So I'll create a `width` attribute and set it to 43 pixels, and create a `height` attribute and set it to 48. And that should be it for the icon image.

After the icon, I want to add the title of the feature. Let's go to our design and check what h-tags to use in this section. And it says that we need to add a hidden H2 tag that says `Features` and then each of the 3-columns will use an H3 tag for the title. Again, this is a header tag that will be visually hidden on the website, but will be detectable by screen readers, to help screen reader users navigate the site more easily.

Let's go to our index.html file and add the hidden H2 tag. I'm going to add it as a child element of the `features` section tag. And the text will say `Features.` Now since this is a hidden H2 tag I need to get the CSS class that we created earlier. If you don't quite remember what class name it was, you can scroll back up the index.html file to see where we used it earlier. We first used it in the header tag-- so there we can see there's an h1 tag with the class `visually-hidden`.

Also, we created the style in the globals boilerplate.scss file. So you could check that file, and look through the styles until you see the `visually-hidden` class. I'll copy that class name, and back in the index.html file I'll add a class to the hidden H2 tag and paste in `visually-hidden.`

Now, for the title for the first of the 3 columns, I'm going to add an h3-tag after the icon image, and give it a class of `features__title`. Then I need to get the copy, or the text, from Figma, `AI-powered matching`, and then go back to our code and paste it in the div. After that, I want to add the description, and I'm going to put it in a paragraph tag. So using Emmet again I'll write `p.features__description` to create the p-tag. And we have to copy the text from Figma and paste it in, and then when we save the file, Prettier will format the text to wrap to multiple lines for easier reading.

Ok, that should be the markup for the first feature. Now, I could copy and paste the `features__item` HTML twice for the other 2 features. But I'm not 100% sure that everything is right-- because when I start writing the styles, I could find some issue that would cause me to have to change the HTML markup or the classes, and then I'd have to copy and paste the changes again to the other 2 features.

So generally what I do when I'm working on the styles for multiple items is get the styles as set as I can with just the first item. And then once it seems like it's working, then I'll copy and paste the markup, make any changes for the other items, and make whatever corrections are necessary.
