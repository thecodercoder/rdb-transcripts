## Prep & setup

[ have 2 File Explorer windows open, one for Downloads and one for the project ]

Alright, in this video, we're going to be modifying the Hero section to make it a little more fancy. Let's first take a look at our existing, Basic website, and then compare it with the Premium design to see what we'll be changing.

On our website, on desktop, we have the text content first on the left, and the unicorn image on the right.

[ highlight "hero__wrapper" ]

And it looks like they are vertically centered. Right now the unicorn is taller than the text, and the text is centered vertically so there's equal space above and below it.

Then if we turn on Responsive Design Mode and load the iPhone view, the image is first, and it's centered. Then below it is the text.

So that's our current website, let's now check out the design in Figma.

In Figma, the biggest change I can see is that we have this curved wave shape at the bottom of the hero instead of just the flat bottom that we had before.

On desktop, the unicorn image looks like it's slightly overlapping that curve. Also the alignment of the text and image is a bit different. Instead of being vertically centered, it looks like the text is aligned to the top, and the unicorn is a bit below the top of the text.

Then, if we look at the wave shape, it is 80px below the text. And it looks like it's aligned with the bottom of the unicorn. This is a pretty common design pattern I've seen, where you have a curved shape for the bottom of a section, with some image slightly overlapping it. Which is why I wanted to put this in the course.

Let's check out the mobile design. It looks very similar to the previous version in terms of alignment. The only new addition is the wave shape at the bottom.

Since that wave image is new, we will need to export it and add it to our project files. Since it's a shape like the unicorn, we'll want to export it as an SVG, so that we can scale it without making it look pixelated.

And, I am using the same SVG image for both desktop and mobile versions. The mobile version looks a bit more bumpy, I guess you could say, because we're squashing the image to fit the smaller viewport. And I think that's totally okay because it is just a shape so it doesn't matter if it looks slightly different as the viewport changes.

I'm going to export the desktop version. If I hold down Control or Command for Macs, then I can click right into the hero-wave layer without having to double-click through the groups.

With hero-wave selected, I'm going to go to the right sidebar and down in the "Export" panel, make sure "SVG" is selected and click "Export hero-wave".

And it's downloaded, so let's go to our File Explorer, and I'm going to copy the image from the Downloads folder, then go to the other window where I have the project files, and I'm going to paste it in the "img" folder.

Let's now go to VS Code and open our Hero styles. I'm going to press Ctrl+P for the Quick Open menu, type in "hero" and select "hero.scss" to open it.

Since we're redoing the hero section, I'm going to clear out most of the styles from the scss/components/hero.scss file. In the file, I'm going to delete the layout style rules from the selectors, but keep the selectors.

So in the main hero class selector, I'll keep the background-color and color rules, since those probably won't be changing. But I'm going to remove everything from "hero**wrapper". Then for "hero**image" I'll delete the styles except for the width: 61%, max-width: u.rem(483), and the width: 100% in the large breakpoint.

Then in "hero**text" we'll remove everything. And we'll keep the styles in the "hero**button" since that's just adding space between the buttons.

And when we save and look at the website on desktop, all our layout styles are gone and we have the unicorn image and the text below it.
