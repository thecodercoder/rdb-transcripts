# HTML markup

In this section we'll be building the Full-width Feature section. As always, let's first take a look at the design in Figma and figure out what HTML markup to use.

In our design, this section is almost identical between mobile and desktop versions. All the content is in one column and centered on both. The main difference is that on desktop, the text and image are larger than what they are on mobile.

So, and this is completely optional, if you want to try to write all the HTML markup for this section yourself, feel free to do that!

If you're not sure how to do something, look back in the index.html file and the styles to see what we've done previously, and use that to go off of. But if you don't feel comfortable doing so at this point, that's totally fine too!

Alright, pause, give it a shot, and then whenever you're ready, unpause and I'll show you how I'm setting it up.

Ok, in our design we just have the one laptop image so let's export that as an SVG. I'm going to select the desktop version, and it's in the layer called `laptop-dashboard`. Then in the right sidebar down at the bottom, in the `Export` panel, I'll make sure `SVG` is selected as the file type and then hit the `Export laptop-dashboard` button. Then I'm going to get the file in my File Explorer and copy and paste it into the image folder.

Now let's go to VS Code and start writing the HTML markup. In our index.html file, like the other sections, I'm going to create a section tag after the previous section by writing `section` and then a dot for the class name. The last section the block name was `features`, so for this one I might call it `fw-feature` for Full-width feature.

Ok, we got our section tag, now what's next? One thing I like to do is if I'm not 100% sure, I can always look back at the code I've already written and follow the same pattern. So if I look at the previous Features section, I can see that in the section tag we put a hidden h2 tag, and then the div with the block and element name with the double underscore, and then the `wrapper` class.

Now, in our new Full-width Feature section, I can follow that. If we look at the design we don't need a hidden h2 tag, since this section does have a title visible. So going back to VS Code, the first element I'll create is the wrapper div. And again, the wrapper will center the content and limit it to 1200px on desktop, and on mobile it will add space on the left and right sides.

To create the div with the class names that we want, I'm going to type `dot` `fw-feature__wrapper` `dot wrapper` and hit Tab or Enter. And VS Code will create a div with the two classes, `fw-feature__wrapper` and `wrapper`.

Inside our wrapper div, I'm going to first add the headline with an h2 tag. In the previous section we had h3 tags for each feature with a class name of `features__title`. So I'm going to follow that pattern and create this h2 tag by typing `h2.fw-feature__title` and hitting Tab or Enter.

The class is in case we need section-specific styles for this h2 tag other than what we have globally. Let's get that headline text from Figma, and paste it in the h2 tag.

Next up we have the description, so under the h2 tag let's create a paragraph tag by typing `p` then a dot and we'll give it a class of `fw-feature__description` and then hitting Tab or Enter. Going back to Figma, let's copy that description text and paste it in the paragraph tag.

After the paragraph we need to add the image of the laptop with an image tag. So I'll type `img.fw-feature__image` and hit Tab or Enter. Then in the `source` attribute I'll type forward slash, `img` and then select the image we just exported, `laptop-dashboard.svg`. Then we'll add alt text, and you can be pretty descriptive here, so instead of just typing like `laptop` I'm going to write `open laptop showing a dashboard on the screen`. Just imagining how you would verbally describe what this image looks like.

Let's see what else we need to add for this image-- I'm going to scroll up and check the image tag from the previous section. And we have the class, source, alt text, and we still need to add the width and height attributes. Let's go to our new image and add `width` and `height` and we need to go to Figma to get the dimensions.

In Figma the laptop image has a width of 792px, and a height of 467px. So we can go back to our code and I'll add `792` for the width and `467` for the height.

I think that's all the markup we need for this section. Let's save what we have and even though we haven't written any styles yet, let's just see what it looks like on the website. Alright, that looks pretty good-- we have the text and the image.
