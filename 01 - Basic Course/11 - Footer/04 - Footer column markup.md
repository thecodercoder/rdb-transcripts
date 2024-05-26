# Footer column markup

Going back to the index.html file, I want to select the `footer__column` section tag. And since we want 4 total columns, I'll duplicate by pressing Ctrl-D 3 times. And we'll want to update the copy for all the other links. I'm going to go back to Figma, and select the second column, `Support` and press Ctrl-C-- this will copy the text of the content here.

Then in VS Code I'm going to paste inside the second `footer__column` section tag. And now we can copy and replace the existing text with the new one. So first is the h3 tag for `Support`, then the links-- Customer Support, Community Forum, Knowledge Base. And this column only has 3 links so we can delete the last link. Now when we save, Prettier will automatically get rid of all the extra space.

Now for the third column. In Figma I'll select the `Follow` layer and copy with Ctrl-C, then in VS Code I'll go to the 3rd `footer__column` and paste the text there. The `Follow` column has those social media icons, which we'll add later on. And again we'll replace the old text with the new ones. So first the `Follow` h3 tag, then Twitter, Facebook, Instagram, and YouTube. And then press save to delete the extra spaces. And again, we'll come back to the icons later on.

Now for the last column. In Figma I'll select the `Resources` links, copy with Ctrl-C, and then in VS Code I'll paste them in the last `footer__column`. And then cut and paste the new text-- Resources, Privacy Policy, then Terms of Use. And delete the last two list items, and save.

Looks good, let's save and check what this looks like on the website. Ok, so we have our text styles, obviously we need to add more styles for the layout. Before then, let's work on adding those social media icons to the `Follow` links.

Going back to VS Code, I believe we already exported the icons-- they are in the img/social folder. Previously when we've worked with SVGs like the hero image and other images and icons, we loaded them in an img tag. We could do here too, but I wanted to also show you a case for loading SVGs as inline SVGs, instead of in an image tag.

Let me show you what I mean with the first icon, for Twitter. In VS Code, let's double-click the `twitter.svg` file to open it. Let's press Alt-Z to wrap the lines so we can see everything. You can see that Font Awesome comment that gives attribution for using this free icon.

Let's copy the whole SVG tag, and then in the index.html file, I'm going to go up to the `Follow` column, find the Twitter `footer__link` anchor link, make a new line before the text, and paste. And this is what it means to have an inline SVG-- we're literally pasting in the SVG code directly into the index.html file.

And without doing anything else, let's see what that looks like on the website. Ok, so we have the icon displaying, but it's a lot bigger than its supposed to be. One interesting thing that you might notice is that the Twitter SVG is the exact width of the `Twitter` text. If we click into the `Twitter` text and write another `Twitter`, then press Enter to reflect the change, the Twitter icon grows along with the text length.

This is because the SVG is taking up as much space as its parent element, the anchor link. And the anchor link, which we've set to `display: inline-block`, is going to size itself based on its content, which in this case is the text inside it. Then the SVG will take the same size. If we set this `footer__link` to be `display: block`, it will take up the full width of the footer wrapper, and the Twitter SVG will then grow with it.

To control the size of the icon, we'll add some styles later on. You can add `width` and `height` attributes to the SVG tag, kind of like we do with the image tags. But I don't think we need to do it for inline SVGs that already have the `viewBox` element.

The viewBox is a bit more of an advanced aspect of SVGs which we don't really need to work with here. But briefly, the `viewBox` attribute controls the size and composition of the `viewport`, which is a frame through which you view the different elements inside the SVG tag-- for example in this SVG we have just one element, the path tag which is the Twitter bird shape.

You can imagine the viewBox a bit like the viewfinder of a camera, where you can control where to position objects in the frame, and how much you want to zoom in or out. The 4 numbers in the viewBox set the x-coordinate, y-coordinate, and width and height of the frame.

Since it does have width and height information, the browser knows how to size the SVG.

Again, this is a bit more advanced aspect of SVGs, so you don't need to worry about it for our purposes here, as we will be sizing the SVGs in our styles later on. But it's good to have a general idea of what it is.
