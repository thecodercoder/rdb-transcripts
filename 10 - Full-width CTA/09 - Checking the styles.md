# Checking the styles

Ok! So the button was the last element to finish for this section, so let's do one last check and compare the design to what we have on the website, to make sure everything matches the design.

On our website, I'm going to inspect the section tag, and check the padding. In the `Layout` tab it says we have 80 px of padding on the top and bottom. So let's go to Figma and see if it's the same. And if we select the CTA Content and hold down Alt and hover just above the selected content, it tells us that it is also 80px on top and bottom.

Next up let's check the main header text-- in Figma, it's 48px. And the paragraph text is 28px. So 48 and 28 pixels. On the website I'll inspect the header text, and in the `Computed` tab it is 48px, which is right. And the paragraph tag is 24px.

Ok, these are different, so we'll need to fix that. In the `Rules` tab for the paragraph styles, let's trace back and see where the font-size is coming from. It's set on the `medium` paragraph class. Since it's using that helper class, that makes me think that we set those styles based on another paragraph in the website.

Let's go to the typography.scss file, and see if there's a different helper class that we can use that does have the correct styles, or if we'll have to create another set of styles for the Full-width CTA paragraph. In the typography.scss file, we can see the `medium` class and in the clamp() function it has a minimum font-size of 20px, and a maximum font-size of 24px. So that's going to be too small for this paragraph.

The `large` class has a minimum font-size of 24px, and a maximum size of 1.75rem, which if we take out the calculator and multiply 1.75 by 16, it is 28px. We do need the 28px size, and let's also check what mobile font-size the Full-width CTA paragraph needs in Figma. There, the mobile paragraph is 24px. So, going back to VS Code, it looks like the `large` paragraph styles are what we want for the Full-width CTA section.

I'm just also going to convert that 1.75rem to `u.rem(28)` to match the other clamp() functions, so it's easier to pinpoint what the size is in pixels. And, let's go to the index.html file and in the `fw-cta__description` paragraph, change the `medium` class name to `large` instead. And let's save, and now on the website the paragraph is the correct 28px size.

The button styles should be fine, since other than the white background color, they are the same as the other buttons on the website. And for the background gradient, we can just eyeball it and make sure it looks similar enough to the design. And if we flip between website and design I think they look quite similar.

Last thing to check for desktop is the spacing between the elements. On the website, if I inspect the h2 tag, in the `Computed` tab it tells us that we have a `margin-block-end` of 20px underneath. And then if we select the paragraph tag, it has a `margin-block-end` of 40px.

Going to Figma, I'm going to select the header and hold down Alt and hover over the paragraph, and there's 20px of space between them, which is correct. And I'll select the paragraph, then hold down Alt and hover over the button, and there's 40px of space under that to the button. So that all matches, which is great.

Now, let's check out the mobile styles. Since we just checked the spacing on desktop, let's do the same thing on mobile. Under the header text on mobile is 20px of space, and under the paragraph is 40px of space. So the mobile spacing matches the desktop spacing.

Let's go back to the website and I'll turn on Responsive Design Mode and make sure the iPhone is selected. And if I select the header, it is 20px of `margin-block-end`, and if I select the paragraph, it has 40px of `margin-block-end`. So we're good on the mobile spacing side.

Now let's check the font-sizes for the headline. If we inspect it it is 36px, and the paragraph is around 24px-- the decimals are probably due to the clamp() function, but this is close enough. So 36px header and 24px paragraph. Going to Figma, the mobile header is 36px and the paragraph is 24px, so we're good!

And lastly, let's just eyeball the background gradient, and flipping between the design and the website, they look the same.

Alright, so everything looks good. So I think we can consider this section finished, and we can commit our code. Go to the GitHub Desktop App, and let's scan the files to make sure there aren't any files that we don't want to commit, but that looks good. And for the commit message I'll write `Full-width CTA` and press `Commit to main` to commit, and then press `Push to origin` to push our changes up to GitHub.

Awesome! Ok, so up next will be the last section of the website, can you believe it! We'll be working on the footer section.
