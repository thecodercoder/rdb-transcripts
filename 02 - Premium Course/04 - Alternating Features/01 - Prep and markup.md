## Prep and HTML markup

The next section we're going to build is the alternating features section! As usual, before we code anything, let's look at the design in Figma, export any images, and think about what our general approach is going to be.

In Figma, we can see that on desktop, we have these alternating text and image sections, where in the first pair, the text is on the left and image on the right, then in the next pair below that they are flipped so the text is on the right and image is on the left, then in the last pair they are flipped again back to the text on left and image on the right.

And on mobile, we have the same content but for each pair, the image comes first and then the text is below that. So the alternating part is only on desktop.

Having the text and image alternating tells me that we'll need to control the order of items-- something that we can do with both flexbox and CSS grid, which we'll get more into the details of later. Right now we're just trying to get an idea of the main style features that we'll be building.

A few other style things that I can see is that in the text, we have some magenta text which is meant for links. And taking a look at how things are aligned, the text is left aligned in both mobile and desktop. On mobile the images are centered. And on desktop, it looks like the text and images are vertically centered.

Those are all the main style things that I can see at the moment, so next, let's export the images as SVGs. I'll export the desktop versions, and again since they're SVGs they're vector images and they will scale up and down just fine, without losing any information or getting pixelated.

First up, I'll select the "laptop-check" image, then in the right sidebar down in the "Export" panel I'll select "SVG" and then click the "Export laptop-check" button. Then let's click on the next image, "tablet-phone", and do the same thing, select "SVG" and hit the "Export" button. And last we'll select the "tablet-payments" image, select "SVG", and export that one as well.

Now let's move the exported image files into our project folder. In File Explorer, I'm going to open up my project folder's "img" folder, and then also open my Downloads folder and select the three SVGs we just exported, and move them or copy and paste them into the "img" folder.

Let's also create our Sass partial for the Alternating Feature block. Since we used "fw-feature" for the Fullwidth Feature section, maybe "alt-feature" for Alternating Features. I'll right-click the components folder and select "New File", then call that file "\_alt-feature.scss".

Then in the components index.scss file I'll load it by writing "@forward 'alt-feature'". Let's also try to keep the partials in the order that they are in the design. Since the Alternating Features section is after the Fullwidth Feature and before the Testimonial section, let's move it between those two sections.

In the alt-feature.scss file, the first thing I want to do is load our utility styles. So I'll write "@use '../util' as u" and save. Ok, now we can start writing our markup!

Let's open up the index.html file. Similar to the previous sections we've done, I'll start by creating a new section tag under the "fw-feature" section, by typing "section" and then let's add a class by writing "dot" and let's call it "alt-feature". Then in the section tag, we want to add the "wrapper" class div, so write "dot" ".wrapper".

Since in the previous Fullwidth Feature section we didn't end up using the section-specific "wrapper" class, I think we can just start with the "wrapper" class. And we can always add an "alt-feature\_\_wrapper" class if we need section-specific styles for the wrapper element later on.

In the wrapper div, we need to figure out how we want to handle the alternating rows. In previous sections like the 3-column Features, we used the wrapper div as the flex or grid parent element, and then added the child elements in that.

Actually, let's go to Figma so you can see what I'm talking about. So before, we had the 3-column section, with 3 items all on one row for desktop. But in our Alternating Features section, we have multiple rows, each with these pairs of text and image.

I think I'd like to have each row be able to stand alone, and we'll have 3 sets of the image/text pair. That way it's more modular, and you can add and remove rows pretty easily without messing anything up style-wise.

Let's go back into VS Code and the index.html file. In the wrapper class div, I'm going to create a new div for the first set of features. Using Emmet, I'll type in "dot" for the class symbol, and then give it a class of "alt-feature\_\_row". Then in the row, I'm going to add the image and then the text. I'm following the order from mobile, where image comes first and then the text is after it.

First, let's create an image tag and give it a class of "alt-feature\_\_image". For the source, I don't remember which image we need first, so let's go back to Figma to check. If we click into the laptop image, the layer is called "laptop-check". So back in VS Code in the source attribute, I'll type in forward slash, then navigate to the "img" folder, and then select "laptop-check.svg".

The image isn't just for decoration purposes, so the alt text should describe the image-- I'll write something like "laptop with green check mark". And since this is an image tag we again want to add in the width and height attributes.

Since it's an SVG image, we can get that information if we open the SVG file itself. I'll load the Quick Open menu with Ctrl-P or Cmd-P on Macs, then type in "laptop-check" and select the SVG image. In the SVG markup, I'll copy the width and height attributes, then close the image file. And in the index.html file, I'll paste it in the image tag.

Ok, after the image we want to add a div for the text content. We're going to use grid to layout the text and image side by side on desktop, so we want to put all the text content together in one div. Under the image tag I'll create a new div with "dot" and then adding the class name, let's use "alt-feature**text". Now, inside the "alt-feature**text" div we'll add the text elements.

Let's go back to Figma to double-check what we need to add, and figure out what tags we want to use. In each text block we have a headline, like "Avoid human error", but before that is some smaller text, "AI-powered matching", which is also sort of like a subheadline or subtitle, but it comes before the title.

I wanted to include this since I have seen it used sometimes in designs. But what tags do we want to use for the kicker and the headline? If we go back up to my outline notes, I wrote down to use h3 tags for the headlines, as we're treating the Alternate Feature topics like an expansion of the Fullwidth Feature block topic, "Angel investment in real time." So that makes sense.

The kicker is a bit tricky because it's less prominent than the h3 headline, so you might want to use an h4 tag for it, since it's not the main headline of the text. But we shouldn't use an h4 tag for it because it comes before the headline in the website, and according to best practice, the h-tags should go in order, so you shouldn't go from an h4 tag to an h3 tag. The website won't break, but it won't be following that outline order that you ideally want your h-tags to be in.

One solution that I like is to put the kicker text inside the same h3 tag as the headline, but wrap it in a span so we can target it in our Sass files and style it differently from the rest of the headline. This way, if you're using a screen reader and navigating between headings, they will include the kicker text when they read the h3 tag. So let's follow that approach. Then below the kicker and the headline, we'll have a paragraph of description text.

I'm going to copy the kicker text, and then in VS Code, in our "alt-feature\_\_text" class div, I want to create an h3 tag with a span tag inside it. So I'll type "h3 right angle bracket span" and press Tab or Enter to generate the markup. For now, we'll hold off on adding any section-specific classes, because hopefully our global typography styles will work for the h3 and paragraph tags.

Then in the span tag I'll paste the kicker text. Let's go back to Figma and copy over the rest of the text for this row. We'll copy the headline, "Avoid human error" and paste it in the h3 tag after the span tag.

Then let's get that description text, copy it, and add a paragraph tag by typing "p" and then pasting the description. And when we save VS Code will wrap the paragraph text to multiple lines so it fits on our screen. By the way, it's fine to put text on multiple lines like this, as the browser will treat it the same as if it was on one line.

And now in our website we can see what we have so far! We have our image and our text. The image is really huge because of our default "width: 100%" for images, but we can size it later on.

Let's also add all the selectors for the elements in our alt-feature.scss file. I'm going to do the split editor thing and right click the alt-feature.scss tab and select "Split down" so it's duplicated on the bottom. Then on the top I'll go to the index.html file and make sure the "alt-feature" section is showing.

So now let's add selectors, starting with the "alt-feature" class as the BEM block name. Then nested in it I'll add "alt-feature**row", then "&**image", then "&\_\_text", and that's all.

Let's save our changes and close the duplicated tab.
