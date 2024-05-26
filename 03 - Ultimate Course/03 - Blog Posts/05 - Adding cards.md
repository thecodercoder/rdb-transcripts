## Adding cards

We've gotten the basic card styles pretty set, at least for now. So let's go back into our markup and create the other cards with their images and text.

Each blog post is going to be one of the "blog\_\_item" article tags, so let's fold up the article tag, and select it, and then duplicate it 4 times. I'm using my custom shortcut Ctrl-D but the default one is Alt-Shift-DownArrow.

So now we have all our article tags, now let's start updating the content. I'm going to fold up the first article tag, and go to the second one. And let's update the image source-- I'm going to update the "blog1" to "blog2" in both places.

And we'll need to update the width and height of the image, so let's open the sidebar and go to the images, blog folder, and open the "blog2" image. And it is 1161 by 774.

And now let's copy the text from Figma. I'm going to copy the headline text and then paste it into the h3 tag. Then the paragraph, and paste it in. And the date.. and then the read time.

[ update other blog posts ]

Okay, we've gotten all the images and text content updated. Now let's check out how things look on the website.

I'm going to load this with the iPhone view, so we can start with just the mobile styles. And the cards look pretty good, although we do need to add space between the "blog\_\_item" elements.

I'm going to inspect the markup to see what we have so far. All the blog posts are children of the "blog\_\_grid" div, and if we inspect that, we don't have any styles there yet. And what we want to do is make that the grid parent for both mobile and desktop.

So let's go into VS Code and start adding our styles. In our blog styles, if we go up to the top, in the "blog\_\_grid" selector, I'll add "display: grid", and then after that, "gap".

And let's go to Figma to check what the space between the cards is going to be. On mobile there's 20px of space between the items. And on desktop it looks like there's also 20px of space.

Back in VS Code, we can set the gap to be 20px, and I'll keep this in pixels. Now on the website we have space between cards.

However, the cards are all different sizes. The first one is super tall, but then the second one is really short. This is probably because of the image tag-- if I inspect the first one, and hover over the filename, we can see that it's a vertical or portrait image, and if we do the same thing to the second blog post, that image is more horizontal or landscape in its aspect ratio.

So right now the cards are getting sized based on how if the image is more vertical or horizontal, because the image will have its width be 100% of the width available. And then the height will be whatever fits the aspect ratio of the image file. So the taller images will have taller cards, and shorter wider images will have shorter cards.

Let's go to Figma and figure out how we want to fix this. If we look at the mobile design, the cards are all 350px tall. And on desktop they are also 350px tall.

So what we could do is set the minimum height of the the card to be 350px. Let's try adding that in our styles, for the "blog\_\_item" I'll add "min-height" and set it to "u.rem(350)".

I try to never set a static height or width for elements that can potentially change size if the amount of content in it changes.

Because for these cards, if I set the height to be a static 350px, even if that's what it looks like in the design, if there ever ends up being a blog post that has a super long title, it will make the card taller since there's more text.

And if it gets taller than that 350 mark then you'll get overflow problems.

So it's safer to set a min-height, because it will be allowed to get taller than the 350px if need be.

And let's save, and see how the website looks. We're getting there! This did help with the shorter cards which are now taller. But the tall cards are still just really tall.

This is all happening because of the images and their aspect ratios making the cards taller than what we want. So we might need to take the images out of the normal document flow and make them position absolute. And then size them to be whatever the height of each card is.

Let's try this. In our styles, in the "blog\_\_image", I'm going to add "position: absolute". And when we save the images are going outside the bounds of the card, even though in our styles for "blog\_\_item" we have "overflow: hidden".

Because with just "position: absolute" the element will not be bound to anything. So we want to limit it to the card in our styles for "blog\_\_item" adding, maybe up at the top, "position: relative". This will force that image to be within the bounds of the card.

And now all the cards look like they're at a similar height to each other. If I inspect them, it looks like they are all at 350px.

Let's do a little stress testing and see what happens if one card gets a super long title. I'm going to the index.html file and in the first card's title, I'll write "lorem30" to make it super long. And let's save.

Ok, obviously this is a very extreme example, but basically, I want to make the card look as good as possible in all circumstances. I think I want to add some space around the top and bottom of the text block, like what we have on the sides.

If I inspect the text block, we had added space on the sides with "margin-inline". So let's change that to just "margin" to add it on all sides. In VS Code we can do this in the "blog\_\_text" selector-- I'll remove the "inline" part of the property.

And now on the website, the super long card looks decent, and at least doesn't look broken. So I think that's good. I'll go back and remove the extra text from the title.

Let's look at all the cards, so the first image was the tall image, and that looks pretty good. The second image, was one of the more horizontal ones, and it looks like it's stopping before the bottom, and if we hover over the image tag, you can see it stops partway down the card.

Ideally, I'd like to have the image fill the card, so we don't have blank space like this. Let's go into our styles, and I'm going to make the filter a bit transparent so it's more clear where the image ends.

In our styles for "blog\_\_filter", I'm going to add "opacity: 0.5". So now the image is more clear. And let's also do the same thing for the text block so we can see the images better while we're debugging. So I'll copy the opacity rule and under "blog\_\_text" I'll paste it in.

And save, and maybe we'll make it even more transparent, I'll change it to "0.2".

Now, in order to make the images fill the vertical space on the card, I'm going to set the "height" to "100%". So on the website the whole card is now filled with the image.

However, you might notice that some of the images look stretched. And this is because we already have the width of the images at 100% from our default image styles, and with height also 100%, it's making the images stretch and get skewed.

We can see this if we inspect one of the images, and then toggle that height style rule.

What we can do to fix this is to use the "object-fit" property. Object-fit lets you control how the actual image file gets sized within its container, the image tag.

By default, it is set to "fill", which means the image will match the width and height of its container. And if the container's aspect ratio is different from the aspect ratio of the image, that will cause the skewing.

Let's go into our styles, and for the "blog\_\_image", let's add "object-fit" and set it to "cover". Now on the website what's happening is that the image will cover the entire width and height of the container, and the browser will crop the image to fit if necessary.

So if I toggle the "object-fit" rule, you can see in the first image, the top of the sky and the bottom of the buildings are getting cut off in order to fit. And, you do have some control over how the image gets cropped, with the "object-position" property.

It will default to "50% 50%" which is horizontally and vertically centered. You can change it by adjusting the numbers, or you can use keywords like center, top, bottom, left and right, to choose which side of the image you want to be visible.

For example, just in the browser, if I set "object-position" and then set it to "center top", it will horizontally center the images if there's extra image on the sides. And if the image is taller than the container, it will position the images so their top edge matches the top edge of the container, and it will crop the bottom out.

So in the first image, "center top" will result in the top of the sky being visible, and it's cropping out the bottom part of the buildings. And if I change to "center bottom", then it will line up the bottom of the image with the bottom of the container, so the top of the buildings and sky are cropped out instead.

And you can do the same thing for "left" and "right". It all depends on what you want to be visible. Generally it's a safe bet to use the default "center" value, especially if you're going to be working with multiple images.

The positioning is very similar to how you can control the positioning of background-images. But it's nice that we can use this with object-fit to control actual image tags.

Going back to our styles, I think we're good with the height of 100% and the object-fit cover styles. Let's delete the opacity styles from the filter and text selectors. And save.

And now the card images are taking up the full height of the cards. Looks good! Next up we'll be starting the layout styles.
