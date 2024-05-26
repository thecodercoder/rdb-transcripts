# Paragraph styles

Ok, let's check the paragraph under the h1 tag. If we inspect it, it's getting its font styles from the global styles in the typography.scss file. Now, one difference here is that while we just have one h1 tag on the site, we are most likely going to have multiple paragraphs in different sections.

So before we make any style changes, let's go back to Figma and see if the different paragraphs in the website will all be the same size, or different sizes.

Generally, I'll use paragraph tags to contain regular text that isn't a header, because you want to use semantic tags like header, paragraph and so on when you can, instead of putting everything in div and span tags.

So in the hero, we have that text under the header. Let's see what font size it is, on the mobile design. This is 24px. Then, as we go down the website, in the next section, the regular text is 18px. So that's a little smaller. The magenta section after that has text that is 20px. So we have 3 sizes right now.

Below that I'm skipping the testimonial section because we'll be using a semantic tag, the blockquote tag, for that quote text, not a paragraph. After that towards the bottom in the blue CTA section, the text there is 24px.

So it looks like we have 3 font sizes of paragraphs: 18px, 20px, and 24px. And I'm going to assume that it will be the same on desktop-- it should have 3 sizes of paragraphs, probably bigger than the mobile sizes. We could add style rules for each paragraph in the section specific styles. So we'd set the font-size for the paragraph in the hero in our hero.scss file, and so on for each section after that.

But, there is a bit of shared font sizes, so for cases like this where there is some reuse of styles, it might be a good idea to set the paragraph styles globally in the typography.scss file, instead of specific to each section.

But if we have 3 different sizes of paragraph text, how can we differentiate them? One way we can do that is with helper or utility classes, which I mentioned back in the `Intro to Sass` section.

So far, we've created classes that follow the BEM approach by using the block, element, and modifier names which result in long class names. One benefit of using BEM is that it makes each class name very specific, to reduce the risk of accidentally using the same class and having your style rules conflict.

Helper or utility classes is in some ways almost the opposite approach. Helper class names are short, often just one word, and their names also describe what styles are associated with those class names.

Let me show you what I mean with these paragraph styles that we need to set up. In our typography.scss file, the paragraph tag selector has the font-size 16px. I'm going to set up our 3 different font sizes inside the paragraph tag.

We have 3 sizes: 18px, 20px, and 24px. I'm going to change the default size to 18px, since the 16px was just something from our demo website. Then, for the other 2 sizes, I'm going to create some helper classes. The first one I'll call `medium`, and in the paragraph tag, I'll create a nested selector with `ampersand dot medium`. And in this class I'll set the font-size to 20px, using our rem() function.

We need the ampersand so that the full selector will be `p dot medium` with no space between the p-tag and the `medium` class. This will then target a paragraph with a class of `medium`.

Now, if you want to try the next example, create another helper class in this paragraph tag with a class name of `large` and set the font-size to 24px using our rem() function.

Ok, to create our other class, I'm going to create a new selector and it will be `ampersand dot` to denote that it's a class, and then `large`. And in the curly brackets I'll set the font-size to `u.rem(24)`.

So now, we have 3 font-size options for paragraphs, and these can be used anywhere in the website that you use these classes. And to prevent unintentional conflicts, the `medium` and `large` class names must be used with a paragraph tag in order for these styles to get applied. So if we added a class of `medium` to an h1 tag, nothing would happen.

Now that we've created our helper classes, we can add the class name to our hero paragraph. Let's go back to the design and check what size we want the hero paragraph to be. On the mobile design, it is 24px. Going back to our paragraph styles, we want to add the `large` class to the paragraph in the hero.

In the index.html file, the hero paragraph is the one with the `hero__content` class. I'm going to add the `large` class name at the beginning, but it doesn't really matter if you add it before or after the `hero__content` class.

Now let's save, and check out the website. And the paragraph looks bigger now-- if we inspect it, we can see our `large` helper class, and in the `Rules` tab we see the `p.large` selector with the bigger font-size, overriding the initial font-size from just the paragraph tag.

Now that we know our helper classes are working, we also need to make each of the paragraph font sizes bigger for desktop, using the clamp() function that we've been using. So let's go over to Figma, and get those desktop font-sizes, starting with the `large` hero paragraph. This was 24px on mobile, and on desktop it is 28px.

We'll go to our trusty Fluid Typography Calculator, and if you want to try this yourself first, you can pause here.

If you don't have the calculator open, in a new tab, search for `Fluid Typography Calculator` and it should be the first result.

In the Min Font Size we'll put the mobile font-size, 24px, and the Max Font Size will be 28px. The Min Viewport will be our iPhone viewport width, 375px, and the Max Viewport will be 1200px which is what our wrapper div maxes out at.

We'll calculate that, and copy the resulting styles, and go back to VS Code. In the typography.scss file, this is for the hero paragraph which we gave a class of `large`. So we want to paste those styles in the `large` helper class selector, after the existing `font-size: u.rem(24)` style, because I want to keep that. And I'm going to round up the long decimals to 2 places.

I also want to change the `rem` values from the calculator to use our rem() function, so that when we eyeball these styles, we can immediately tell what the minimum and maximum font-sizes are in pixels. This is just my own preference-- you can keep everything as is from the calculator if you want.

I'm going to delete the `font-size: 1.5rem` which is the same as our `u.rem(24)` style. And I'm also going to replace the minimum value in the clamp() function with the same thing. And I'll replace the maximum value, 1.75rem, with `u.rem(28)`.

Now let's save, and make sure our styles are getting loaded and are working. In the website if we inspect the paragraph text, we can see our clamp() function, and in the `Computed` tab the font-size is a minimum of 24px for mobile viewports. Then as we increase the viewport it increases until it hits 28px. Nice!

Let's do the same for the other paragraph sizes. Going to the design, the next paragraph text is in the 3-column Features section, and on mobile it is 18px, which is the smallest size we had. Then on desktop that paragraph is also 18px. Since they're the same for both, we don't need to add any other styles for it.

After that, in the magenta full width Feature section the paragraph is 20px on mobile. And on desktop it's 24px. So let's go to the Fluid Typography Calculator and input those values in. I have it open from last time, so I'm going to change the Min Font size to 20px, and the Max Font Size to 24px. And copy the result, and in our styles this will be in the `medium` class selector.

So I'll paste it below the existing font-size, and round the decimals to 2 places, and I'm going to delete the `font-size: 1.24rem` since we have our `u.rem(20)` value. Then I'm going to copy the `u.rem(20` and paste it in the minimum value in the clamp() function, and also paste it for the maximum value and change the number to `24`.

Ok, so that should be it for the paragraph font sizes. Next up we should also make sure the line-height is correct for them.

First, for the hero paragraph, on mobile it's 24px font size and 31px line height, so 31 divided by 24 is 1.3, which is 130% of the font-size. On desktop it's 28px font-size and 36px line-height, which is also around 1.3. So in our styles for the `large` class paragraph, let's set `line-height` to 1.3.

The added benefit of using the ratio line-height instead of setting it to a static unit like px or rems is that as the font-size scales the line-height changes with it. So this way we don't need to calculate another clamp() function for the line-height.

And while we're here, let's check the line-heights for the other paragraph sizes. In Figma, let's go in the mobile design to the 3-column Features. The line-height is 23.4, so 23.4 divided by the font-size, which is 18, is 1.3. And this paragraph is the same size on desktop.

This is the same 1.3 line-height as our large paragraph style. Lastly, let's check the medium size paragraph line-height. In Figma, that will be paragraph in the magenta full width CTA section. It's 26px line-height, so 26 divided by the font-size, 20, is 1.3.

Since all three paragraph sizes have the same line-height, we can make that the default line-height. In VS Code, I'm going to select the `line-height: 1.3` rule from the `large` paragraph and move it up to the default paragraph styles. Now, both `medium` and `large` paragraphs will inherit the line-height from those default styles.

Cool, so I think we are good for our general paragraph styles. I know we got side-tracked slightly from just hero styles, but at the beginning of a website build I think it's worth it to spend a bit of extra time setting up global styles like these. That way, later on we can just use the paragraph classes, and won't have to write out the styles again.

The last thing we need to check for the hero section paragraph is the space under the paragraph. On the mobile design, from the paragraph bottom to the buttons is 40px. And let's see if it's the same for the desktop styles. On desktop, from the paragraph to the buttons is also 40px. So mobile and desktop have the same margin-bottom values.

In our styles, for the `large` class paragraph I'll add `margin-block-end: u.rem(40)`. And for this I am going to use rems so that the space between paragraphs will scale up as the browser base font size goes up, which will help with readability. And for now, we'll leave off setting the margin for the other paragraph styles-- we'll get to them as we go down the website.
