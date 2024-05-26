## Setup and markup

Alright, in this part, we're going to be building the Blog post section. So let's start by checking out the design.

We have these blog posts in basically a block grid, and on desktop they are in a grid of 3 across, and you can see that since there's five blog posts, the second row is following the column size of the first row, but has an empty spot where the last column is.

And then, on mobile, the blog posts look the same, but they are all in one column. Looking at the design, my thought is to build this using grid, because on desktop, we have an arrangement of 3 per row, and the blog items are conforming to that arrangement, even when there's an incomplete row.

We're not stretching the two items in the second row to fill the available width, that would be something that we'd need flexbox to do. So yeah, I think that this would be a really good place to use grid and auto-fit to make the browser dynamically decide how many columns will be in each row, based on the available width.

Then, inside the blog posts themselves, they each have an image in the background with a gradient filter effect going on, which we'll be building with the mix-blend-mode property, which you can do pretty cool things with.

Then we have a white block in the center with the blog post title and other text content.

Before writing code, we'll need to export the images from Figma. So if we zoom out, next to the mobile design, there's a whole frame for all the blog photos. And I've included 2x and 3x versions of each one.

To export them, don't select the frame, because then it'll generate one gigantic JPG of the frame with all the photos in it. You'll want to select each one individually. The quickest way to do that is to go to the left sidebar, and expand the Blog Photos frame, then select all the images.

Then in the right sidebar, down in the Export panel, we can export them, make sure we have JPG selected, and just leave it at 1x because I already sized the images.

We got our zip file, so I'm going to open it, and I generally try to optimize all the images so they don't weight down the website. I'm going to copy the files from the zip file and paste them in my downloads folder.

Then let's go to the TinyPNG.com website, and I'm going to drag all the files there.

And we saved lot on file size, which is one reason I really like TinyPNG. Okay, let's get the zip file with all the images, let's open it in our file explorer, then copy all the images, and now I'm in my project root, and let's go into the "img" folder. And I think because we have so many images, I'm going to create a new folder called "blog" and then paste them in there.

Now we should be ready to start writing our code. In our index.html file, let's start writing our markup. The blog section is after the Testimonial section, and before the Full-width CTA section.

So after the "testimonial" section tag, I'm going to create a new section tag, and give it a class of "blog". And in it I'll create a div and give it a class of "section". Now, inside the wrapper we'll need to create our h2 tag-- it's an h2 since it's heading up the section.

And let's get the copy from the design-- it says "Recent blog posts". And I'll just copy that and then go back to VS Code and paste it in there.

Alright, next, we're going to create a div that will serve as our grid parent, and it will contain all the blog posts. I'll create a new div and give it a class of "blog\_\_grid".

In this div I'm going to just create one blog post to start. And once we're fairly sure that the markup won't need to change, then I'll duplicate it to create the others.

First, each blog post needs to be in an article tag. This is because each blog post can be thought of as its own piece of content that can kind of exist on its own. Blog posts are one pretty widespread example of article, tags, although they can also be pieces of content like a comment or even little widgets that you might have on your website.

So, let's create an article tag, and I'm going to give it a class of "blog\_\_item".

[ Figma on R, VS Code on L ]

Let's go back to the design-- in the blog item, it has an image and then a white block with text.

The image you could set as a background-image on the "blog\_\_item" element, but I'm going to create it as an image tag with "srcset". This way, we can display either the 2x or 3x version of the image, depending on the DPR of the user's device, and save a little on bandwidth if the device doesn't need the high resolution image.

In VS Code, I'm going to create the image tag first, because it's under the blog text block, so we're going to leverage the natural stacking order where latter elements will by default get displayed under earlier elements. This is the same thing we did with the hamburger menu.

I'm going to write "img" and then select "srcset". And, let's create a class, and I'll call it "blog\_\_image". In the source field, we'll set it to "/img/blog/blog1-2x.jpg" -- using the lower res 2x image as the default.

And for the alt text, I'm going to leave it as a blank string, so that screen readers will ignore it. Because the photo doesn't really contain vital information for the blog post-- it's really more of a decorative image.

Then for the "srcset", let's set it to the 3x image, "/img/blog/blog1-3x.jpg".

We also want to set the width and height for the image, so the browser knows the aspect ratio of the images and will leave enough vertical space on the website while the image file is still being loaded.

Let's get that info from VS Code. I'm opening the sidebar and going to the images, blog folder. And if I select the first image, it'll open a preview of the image and also list the image dimensions in the very bottom purple status bar.

And in the index.html file, I'm going to add the "width" and "height" attributes to the image tag. And when we go to the image, it is 774 px wide, so we can add that. And it's 1032 px tall.

And I think that's good for the image tag for now.

Going back to the design, the blog images have a sort of filter on them. If I click into one of them, there is a layer called "Background" and then one called "Blend Overlay". And in the blend overlay is a linear gradient.

We're going to be using the CSS property "mix-blend-mode" to blend the linear gradient with the blog images. Let's start by getting the colors of the gradient and saving them as CSS custom properties. I'm going to click on that little color swatch and we can see that it is made up of a blue color and then a magenta color.

I'm going to first copy the hex code for the blue color, and then in VS Code, let's create a new custom property. Since the Blog section is before the Full-width CTA section, let's add it right before the "fullwidth-bg". And I'm going to call it "--blog-gradient1".

And then I'll paste in the hex code. And add the hashtag so we get the color swatch, then click on the swatch and click the title bar to convert it to HSL.

Now let's go back to Figma and copy the magenta color, and then in VS Code I'm going to duplicate the first custom property. And in the second one we'll rename it to "2" and then replace the color with our copied hex code. And then let's convert it to HSL.

Alright, we have our photo, now for the gradient, in order to do the blending, we want the gradient to be on top of the image. So again, using the default stacking behavior, we need to put the gradient in an element that comes after the image tag.

I'm going to create a new div for this, so in our index.html file, after the image tag, let's create a new div and give it a class of "blog\_\_filter" since it's adding a kind of filter effect on the image. And it will just be an empty div with no content.

Next, we'll want to create the white text block. Going back to the design, we want the text to be on top of the image and filter, so let's create a new div. I'm going to give it a class of "blog\_\_text" and then in it, we want to first add the blog post title.

Since the section title is an h2 tag, we should make this an h3 tag. And I'll give it a class of "blog\_\_title". Now let's go to Figma and copy that first blog post title, then go back and paste it in.

Next is the little blurb, and I'm going to create that as a paragraph tag. And let's go to Figma and copy that over, and paste it in.

Okay, before we write the markup for the bottom elements, we need to figure out how we want to handle the layout of the text elements in the white block, and the bottom text which contains the post meta. I'm calling it "meta" because it contains information about the post, like the date, which falls under metadata.

My main question is, do we want to use grid or flex to layout all of the elements, or use margin to add space between the title and blurb, and then use grid or flex only on the bottom two post meta elements?

One thing that I can check to help us make the decision is to look at the spacing between the three sort of rows of elements in the white block. If they're the same, we can make them grid or flex children and use gap to add space between them all pretty efficiently.

If the spacing is different, we might have to use a combo of gap plus margin, or not use grid or flex and only use margin. So let's check this out in Figma.

I'm going to select the middle blurb text and then hold down Alt. And this is telling us that we have 16 pixels of space between the title and blurb, and another 16 pixels of space between the blurb and the post meta. So since it's the same, I think it would be simplest to use grid for the white block.

By default, creating a grid parent will put each child on its own row, as opposed to flex which will put each child in its own column. So this will put the text elements under one another without having to add any additional properties.

And I'll probably wrap the post meta elements in their own div, and use flexbox to align them to the outer sides with "justify-content" "space-between". And I want to use flexbox in this case because the two elements will be put in the same row just with "display: flex".

We will get to all that a bit later on with the styles. But the decisions I'm making for the layout are helping to determine the markup, at least for the post meta.

Since I want to use flexbox for them, I'm going to create the div to contain the meta, and give it a class of "blog\_\_meta". Then, we'll add the date, in a "time" tag. And let's copy that date text, and paste it in the time element.

The HTML time element is used for date and time for things like blog posts or other dates associated with pieces of content. And, when you're using the time element, it needs to either be in a "year dash month dash day" format, or, if it's not like in our case here, you can add a "datetime" attribute and set it to the proper datetime format.

So for us, we'd write it with "2024-06-14" for June 14. Including the datetime format allows the date to be machine readable for things like search engine indexing. If you've ever done a search and noticed a date as part of the search results to help you understand how recent or old the results are, a lot of that is due to putting the date and/or time in a time tag.

Okay, after the date we'll add a paragraph tag, and in it write "8 min read".

The other thing that we need to do is add the links to the card, since each card is meant to be a link to the actual blog post. One thing that you need to make sure not to do is make the entire card a link by wrapping everything in an anchor tag.

This is not great for screen readers because if the user is navigating with tab to go through focusable elements on the page, the screen reader will read out the text content of the link. So if you make the entire card a link, the screen reader will read the entire content of all the text in the card, which is not a good user experience.

So for our card, I think we'll just make the title a link. I'm going to go inside the h3 tag, since anchor tags are not supposed to contain any other tags-- it is considered invalid HTML.

And let's create our anchor tag, and I'll select "link" and then generate it. And I'm going to make the href blank since this link isn't actually going anywhere. And then move the closing tag to the end of the title text.

Alright! I think this looks pretty good for our HTML markup. Next we'll start getting into our styles.
