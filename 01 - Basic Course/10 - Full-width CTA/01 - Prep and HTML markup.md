# Prep and HTML markup

In this section we'll be building the Full-width CTA section. As always, let's check out the design and figure out what our approach is going to be.

We're getting close to the end of the website, which is exciting!

So this section has a lot of similarities with the Full-width Feature section we built previously. They are both centered, with a headline and a paragraph. But instead of the laptop image, we have a CTA button. And the background here has a gradient background instead of a solid color.

Like before, let's go to VS Code and add the HTML markup for this section. Since we know it's very similar to the Full-width Feature section, I'm going to go up to the section tag with the `fw-feature` class and copy the whole thing, then go under the Testimonial section, and paste it there.

Since we don't need the image I'll delete that. And we need to use a different BEM block name other than `fw-feature`-- maybe `fw-cta` since this is the Full-width CTA section. I'm going to do a Find & Replace, to change the `fw-feature` name to `fw-cta`. But I don't want to change anything from the original `fw-feature` section, only in this new section.

We can do that by using a Find & Replace within Selection option. First I'll select the `fw-feature` text, and then press Ctrl-F. Selecting the text you're searching for before opening up the Find menu will automatically search for the text you've selected. Right now it says there are [XXX] total matches, and VS Code also highlights the matches in the document, which you can see if you scroll up a bit.

Now, we want to only search within the second section tag, so I'm going to select that whole section tag in the file, and then in the Find menu I need to turn on the `Find in Selection` option, which is the three lines icon to the right of the down arrow. Now, there are only [XXX] matches, and if you scroll up the matches in the first section tag are no longer highlighted.

Then, to the left of the text is a right angle bracket. Click that to expand the `Replace` tool. Then in the text box there type in `fw-cta`. Then you can either replace individual matches with the first `Replace` button. Or if you're feeling confident you can replace ALL matches with the second button to `Replace All.`

One way to get to the Find and Replace menu quicker is if we first close out of the menu. Then highlight the `fw-feature` text, and instead of Ctrl-F, press Ctrl-H to automatically open the Find AND Replace menu. Then select the section tag and click the `Find in Selection` icon. Then you can replace either one by one, or all at once.

So now it's saying that there are no results for `fw-feature` within the selection, since we replaced them all.

Now that we're done with that, let's save, and then copy over the actual text from the design for the header and paragraph for this section. Going over to Figma, I'll select the header text and copy it, then in VS Code paste it in the h2 tag and replace the old text. Next, let's copy the paragraph text and then paste it in the paragraph tag.

After that we need to add the CTA button. In the design it says `Free Trial` like the button up in the hero section. So I'm going to go back to the index.html file, go up to the Hero section, and copy the markup for the Free Trial button, then go back to the Full-width CTA section and paste it in under the paragraph. And we'll want to replace the `hero` block name with `fw-cta`. And for now let's leave the `primary` class name, but we'll be changing this later to get the solid white button styles.

Now let's create our new Sass partial. Like the other sections, I'll create it in the scss/components folder, and let's call it `_fw-cta.scss`. And we'll need to add it in the components index.scss file, with `@forward 'fw-cta'`.

Then, in the `fw-cta.scss` file itself, the first thing we'll want to add is using the utils, with `@use '../util' as u`. And now we can start adding the selectors for the elements we added in the HTML. I'm going to split the code editor in half and put the index.html file on the bottom-- right-click the index.html file tab and select `Split down` and it will duplicate on the bottom half. Then in it, I'm going to scroll down to the Full-width CTA section so we can see the elements.

In our Sass file, the first selector will be our BEM block class, `fw-cta`. Then nested in it will be the BEM element selectors, starting with `fw-cta__wrapper`, then `&__title`, `&__description`, and then `&__button`. Now let's save, and then close the duplicate index.html tab.

And that's it for setting up our HTML and Sass partial. Now let's get on with writing our styles.
