# Hero prep and HTML markup

Alright, in this section we're going to be building the Hero. So let's start by looking at the design and figure out how we want to build it.

In Figma, the hero section has that purple background color, and it is two columns on desktop with text on the left and image on the right, and one column on mobile with the image first and then the text underneath it.

First, let's export the image of the unicorn into our files. Double-click on the unicorn a couple times to move through the Hero layers until you have selected the "unicorn" layer, with both unicorn and stars selected.

Then in the right sidebar with the "Design" tab open, go to the bottom panel that says "Export." Like I mentioned earlier in the course, since the unicorn is a flat illustration made of shapes, we should export it as a SVG. You could also export it as a PNG, as PNGs are good for these illustration type images, and they can support a transparent background.

JPGs would not be a good option for a few reasons-- JPGs can't have a transparent background like SVGs and PNGs. And since they're designed for complex photographic type images, they'll end up being a larger file size than SVGs and PNGs.

But, just to compare, let's export the unicorn image as an SVG, PNG and JPG and see how they match up. We did this with the Mythos logo, but since the unicorn image is more complicated I think it'll be worth comparing again.

In the "Export" panel, I'm going to expand the preview so we can check that the unicorn and stars are included, and we can tell that the background is transparent because it has that checkerboard white and light gray background. So we have everything we need in the export.

First I'll export it as an SVG. Then as a PNG, making sure to export it at 2x so it won't look pixelated on retina and other high pixel density displays. And last, let's export it as a JPG, again keeping it at 2x.

Now if we check out the file explorer, we can see immediately that the SVG file is smaller than the PNG, and the JPG is a lot larger than the PNG. However, let's optimize the JPG and PNG files with TinyPNG, just to see if we can get them any smaller in size.

So on a new tab I'll go to TinyPNG.com and I'm going to drag the JPG and PNG files and we'll see how much space we can save. Ok, so now the optimized JPG is [XXX] which is still larger than the SVG, but the PNG file is [XXX] which is smaller than the SVG. However, I think I'm still going to use the SVG file just because it can be sized up without losing quality.

For example, let's say the design changes and the unicorn needs to be bigger. If we used a PNG we'd have to re-export a new PNG at the bigger size, but with an SVG we could use the same file and just set the size to be bigger.

So, let's copy the SVG unicorn to our project files, in the img folder.

Now before we start writing code, let's look at the design and figure out what our approach is going to be. I'm going to build the mobile version of the hero first, where everything is in one column. Then I'll add some more styles to get that 2-column layout for desktop.

One of the differences between the mobile and desktop layout aside from the columns is that on the mobile version the image is first, but on the desktop version the text is first, being on the left. The good thing is that we can control the order of the content in both flexbox and grid, to flip the order for desktop.

We'll be getting into that later on, but for now, let's go to VS Code, and start writing the HTML markup! What we want to do is follow a similar structure to the header, where we have one element with the class name of the block, which will be `hero`, similar to what we did with the Top Nav, and then a child element that has the wrapper class to limit the width of the text and image content.

The hero is going to be a child element of the main tag and the article tag-- as a refresher, all the website content except for the header and footer go inside the article tag, and that includes the hero.

So, in the article tag, let's first delete everything in it that we created earlier, since we don't need it anymore. Then I'm going to add a new section tag by using the Emmet shortcut and typing `section dot` and give it a class of `hero` and then in that section tag I'll create a div with a class of `wrapper` by typing `dot wrapper`.

As I mentioned in the Top Nav section, we don't want to put the `wrapper` class in the section tag because we want that purple background color to extend out to the full width of the section. So the background color will be added to the `hero` section tag, and then the `wrapper` div will be a child of the section tag and limit the content to 1200px wide.

Let's also add a hero-specific class `hero__wrapper` to the wrapper div, like we did in the Top Nav, in case we need to add some Hero-specific styles to it. Then in the wrapper div, we'll put the unicorn image and the hero text content.

In terms of which to put first, I usually follow the order of the mobile design when writing the markup, then change the order when necessary for other viewports using CSS. So since the image comes first on the mobile design, I'll add an image tag for the unicorn image.

Following the BEM approach, I'll create the image tag by typing `img` and then give it a class by writing `dot` and the class name, which will be `hero__image`. And then pressing Enter. In the class name, `hero` is our block and `image` is the element.

In the `src` field I'll link it to the /img/unicorn.svg image, and I'll add an alt text of `unicorn with stars.` And we also want to add width and height attributes so the browser knows how much height the image should take up on the page while the image file is loading.

We can look at it in Figma, but another way you can look at image is in VS Code. I'm going to navigate to the `img` folder and then open the unicorn.svg file.

In the SVG code, you can see that there are a lot more paths in the unicorn than there were for our Mythos logo SVG. In the SVG tag itself, the width is 483 pixels and the height is 486 pixels, so going back to the index.html file, in the image tag I'll add width equals 483 and height equals 486. Now let's check the website to make sure the image shows up-- and it is, which is great.

Now let's add the text content with the buttons after the image, with a new div that we'll give a class name of `hero__text`. This `hero__text` div is on the same level as the image tag, with both direct children of the `wrapper` div. We're doing it this way because in order to make the 2-column layout work with either flexbox or grid, we need a parent flex or grid element, which we will make the `wrapper` div.

Then the unicorn image tag and the `hero__text` div will be flex or grid child elements. So when writing the HTML markup I try to think ahead a bit for what the different layouts will be for mobile and desktop.

Now, in our `hero__text` div, we need to add the copy from our design, so let's go to Figma.

First, I'll copy and paste the main header text, `Find that elusive unicorn`. And in our HTML, we want to put it in an h1 tag since it's the main header of the website. So I'll create the h1 tag by typing `h1`. And add a dot to give it a BEM style class name, `hero__title`. And then I'll paste in the text.

Next, let's go back to the design and get the copy for the text under the main header. And I think I'm going to put it in a paragraph tag with a class of `hero__content`. Let's type in the tag name which is the letter `p` and then to start adding the class type in a `dot` and then the class name `hero__content` and press Enter. Then VS Code will generate the markup, and in the paragraph tag we can paste in the text from Figma there.

As a side note, I've also seen people use an h2 tag for this type of content, since it could considered a subhead. But for me, it just seems to be more of a paragraph type of thing than an actual subheader, as I'm using the h2 tags to help title each section in the website.

Going back to Figma, under the hero text content, we have two buttons-- one says `Free Trial` and the other says `Pricing.` So in VS Code, let's add the markup for those-- I'm going to create an anchor link by typing `a` and selecting `a:link` from the pop-up, and press Enter. And let's give the button a class of `hero__button`.

Then for the `href` attribute which is the URL that the link will go to, let's just leave it blank. Normally, it would navigate to another page on your website like `free-trial` or `free-trial.html`, but we don't have multiple pages, just this one, so we'll leave it blank.

And then in the anchor tag, we'll add the button text, which I'll write as `Free Trial`. Even though it's uppercase in Figma, I'm writing it with regular title capitalization and we'll make it all uppercase in our styles, the same way we did with the Top Navigation links.

Then for our second `Pricing` button I'll duplicate our Free Trial button by selecting it and pressing Ctrl-D. And then changing the button text on this one to `Pricing`.

And that's it for the HTML markup for our hero section!
