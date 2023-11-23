# HTML markup

Let's go to VS Code and start writing our HTML markup. Like we've done for previous sections, let's create a new section tag for the Testimonial section by typing `section` and give it a class name with `dot testimonial`, then hit Enter to generate the markup. So `testimonial` will be our BEM block name. Then in the section tag we'll add our wrapper div, with `dot testimonial__wrapper dot wrapper`.

Going back to the design, let's see what else we'll need to add. There's no headline for this section, so we should add a visually hidden h2 tag to help with screen reader navigation. I'm going to add the h2 tag as a direct child of the section tag, and write `h2 dot visually-hidden`, to use the `visually-hidden` class that we created. Then write `Testimonial` as the h2 text.

Then, in the wrapper div, we'll add the other content for this section. Let's refer back to the design. We'll want to load the quotation mark image, so in the index.html file, in the wrapper div, I'll add an image tag with `img` and then give it a class of `testimonial__image`. In the source attribute, I'll type forward slash, `img`, then select the `quotation-mark-teal.svg` file. And since this image is purely decorative, with no real information in it, I'll leave the `alt` attribute blank so that screen readers will skip over it.

And, like our other images, we need to add the `width` and `height` attributes. And let's go back to Figma and get the image size. In the desktop design, the quotation mark is 78 by 66 pixels. So back in VS Code I'll set the width to 78 and the height to 66, so the browser knows the aspect ratio of the image.

Let's go back to the design, and after the image is the actual quote text. I'm going to copy that text, then go to VS Code, and after the image tag, we need to add the markup for the testimonial quote and author information.

For this, we'll be using the `blockquote` HTML tag. If you're not familiar with this, or want to make sure you're adding it correctly, my first step is generally to search for `mdn blockquote`. And let's go to the first result.

Here, there's an example with the blockquote tag, then the quote text is in a paragraph in it, and the author and cited work is in a footer tag with a cite tag around the book name, `Brave New World.`

However, when I was doing more research, the actual HTML spec said something different. You can see this if you scroll down to the `Specifications` and click on it.

In the HTML spec, in the examples, it says "Attribution for the quotation, if any, must be placed outside the blockquote element." Which is what MDN did in its example. This just goes to show you that people will do things in different ways. I don't think it's a disaster to include the attribution inside the blockquote tag, but in this case I'm going to go with what the HTML spec says and put attribution outside the blockquote tag.

This first example has the blockquote tag, a paragraph tag with the quote text, then outside the blockquote tag is another paragraph tag with the author name.

In the next example, there is also a `figure` tag that contains the blockquote, and the attribution is in a `figcaption` tag which has a `cite` tag for the name of the source work.

So while I think the simpler example would be fine, I think this might be a good opportunity to use the `figure` and `figcaption` tags since we do have more complicated content, like the quotation mark icon and the author image.

The figure tag is a semantic tag that lets you group together content like images, illustrations, and so on, that can sort of stand alone from the main content of the website without disrupting the flow of information.

In our website, the testimonial quote and author photo and description is this type of self-contained content, so I think I'll be including all of it in a figure tag. We'll use the blockquote tag for the quote text, and put the author name in a `figcaption` tag. And we don't need the `cite` tag, since we don't have a work that is being cited here.

We'll keep this tab open so we can reference it as we build this out. Let's go back to VS Code and set this up.

I think the quotation mark image should also go inside the `figure` tag, so I'll create a figure tag by typing `figure` and pressing Enter, then I'll move the image tag in the figure tag. After the image tag, I'll add a `blockquote` tag with a paragraph tag nested in it by typing `blockquote > p` without any spaces, then pressing Enter or Tab, and then pasting in the quote text from the design.

After the blockquote, we'll want to add the author image. Like I mentioned earlier, we're going to load the images and give the browser the option to load the 1x, 2x, or 3x image file, based on the DPR of the device loading the website.

In order to do this, we're going to use a pretty cool HTML feature called `image source set`. First add an image tag by typing `img` into VS Code, and then selecting `img:srcset` in the pop-up dropdown.

The `srcset` attribute is what we'll be using to load the 2x and 3x images. But first, in the `src` attribute, we'll load the default 1x image. I'll type forward slash, `img slash`, and then select `author-1x.jpg`.

In the alt text, I want to display the name of the fictional person in the testimonial, so going back to Figma, I'll copy the name, `Janice Hsu`. And in the image tag alt text I'll write `Headshot of Janice Hsu`.

Then, in the `srcset` attribute, we're going to load first the 2x image. I'll type the path to the 2x image, `/img/author-2x.jpg`, then a space, and then `2x`. Then I'll add a comma, and type the path to the 3x image, `/img/author-3x.jpg` then a space, and a `3x`. What we're doing here is loading the path to the image file along with the DPR. And separating multiple images and DPR sets with a comma. So now if we load the website with a device that has either 2x or 3x DPR, it will load the proper image. And for computers and other devices that have a standard 1x screen, it will load the default 1x image.

Let's save and see how this looks. Ok, so we have our unstyled Testimonial section, and the image is loading, which is great. And let's also test to make sure the different DPR images can load. In the dev tools in the top bar, instead of the `Inspector` I'm going to click the double right angle brackets, and select `Network`.

The `Network` tool lets us see exactly what files are being downloaded for the website. I want to just display our author image, so I'm going to click the `Images` label, and then reload the website. And if we look in the list, we can see the `author-1x.jpg` filename. Let's also filter for the word `author` to make it a bit easier.

So this is good because it tells us that we have successfully loaded the 1x image. Now, I'm going to turn on Responsive Design Mode, and select the iPhone. It's really tiny, but up at the top above the emulated iPhone we can see that it says `DPR: 3`. So let's reload for good measure, and now in the `Network` tool we have the 3x author image getting loaded, which is great.

Ok, now that we're done with the image, let's go back to our markup and see what else we need to add. After the author image, we need to include the author information. Like I mentioned earlier, we have all the testimonial content in a `figure` tag, and the author name and description can be thought of like the caption for the quote and author photo.

So let's add a `figcaption` tag. And then going back to the design, I'll copy the author info text and then paste it in the `figcaption`. Now, in the design, the text is on 2 lines, with the author name on the first line and their description on the second line.

To break the text into 2 lines I am going to add a line break tag after the name. You may have heard that you shouldn't use br-tags when you can use CSS, but I am using the line break in the way it's meant to be used in this case-- to break text into multiple lines.

You shouldn't use the br-tag to add space between design elements, but it's ok to use it for the tag's originally intended purpose.

The last thing we want to do is to wrap the author image tag and figcaption in a div. This is because we'll have to use either flexbox or grid to layout the author information responsively, where the photo and text are side by side on desktop, and then stacked on mobile. So I'm going to add a div after the blockquote and give it a class with `dot` and I'm going to name it `testimonial__author-wrapper`. I know it's a bit long, but I think it will be helpful as a descriptive class.

Now let's select the image tag and figcaption and then hold down Alt and press the up arrow to move them into the div. And while we're here let's add BEM classes to the other elements. The quotation mark image has a class of `testimonial__image` but maybe I'll rename that to `testimonial__icon` so it doesn't get confused with the author image.

Then for the blockquote paragraph tag, I'll add a class of `testimonial__quote`. Then the author image, let's make that class `testimonial__author-image`. And the figcaption, I'll make the class `testimonial__author-description`. And I think that should be it!

And now when we save and check out the website, we have all the Testimonial content that we need showing up! Now we can begin styling the content.
