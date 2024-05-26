## Tablet/desktop grid layout

Alright, so now we're going to work on the tablet and desktop styles.

In the "fw-cta\_\_form" selector, I'm going to add a breakpoint since we don't want this to affect mobile styles, with "@include u.breakpoint".

And I'm going to set this to "medium" since I think tablets are wide enough to handle the button being next to the form textbox. So these styles will be applied for tablet and desktop.

So I'll set "medium" as the parameter, and then in our media query I'll add "grid-template-areas" and in the value, we need to kind of diagram the layout that we want for tablet and desktop.

Going back to the design for a little refresher, we want to have 2 columns and 2 rows. The label will be in the first row, taking up both columns. And then in the second row, the textbox input will be in the first column, and the button will be in the second column.

If you want to try this yourself first, you can pause the video, and then test out what the "grid-template-areas" should be for this.

[ pause ]

Alright, so, I'm going to add the "grid-template-areas", and in the value, we'll add quotation marks, and then write the areas for the first row. Since it's only the label there, I'll write "label label".

Then, below that, we'll write the areas for the second row. I'll add another quote, and write "text button".

Note that we haven't added any sizing with grid-template-columns or rows, so the size of the columns and rows in our grid will be based on the size of the content in them, which I think should work, but we can tweak if necessary.

Now, let's save, and see what happens. And in our website, I'm going to load the iPad view.

So, we're kinda there-- we have the 2 columns and 2 rows, but things look slightly wonky. Let's inspect, and I'll make the grid highlighting a little easier to see, maybe light green?

The first thing is that the grid is super wide-- it's stretching taking up the full width of the container. So the first thing we'll do is to make the grid content centered and not stretch out.

In the parent selector, in the breakpoint, I'll add "justify-content: center". And when we save, just like I showed you earlier, now the grid content as a whole isn't stretching out all the way.

The second thing I'm noticing is that the "Contact" button is stretching to be taller than it should be. This is probably because of the margin we added under the input, which we needed for mobile. But we don't want it when they're side by side.

Let's go back to our styles and in the "form\_\_text", I want to only add the "margin-block-end" for mobile, or small breakpoints.

Okay, so while we could add a breakpoint for "medium" and in it reset "margin-block-end" to zero for medium and large widths, in this case it would be more efficient to use the "breakpoint-down" mixin and set the parameter to "small".

If you need a quick refresher, you can check out the breakpoints.scss file-- press Ctrl+P for the Quick Open menu, type in "breakpoints" and we'll see our Sass maps and the mixins.

We want to use the "breakpoint-down" mixin that's at the bottom to create a "max-width" media query, which reads from the "breakpoints-down" map.

And I'm going to use the "small" size which is 699px. For our other styles in the form, we're changing the layout with a min-width media query which uses the "breakpoints-up" map and the "medium" size, which is 700px. So I want to match that breakpoint.

Okay, going back to our Full-width CTA styles, in the "form\_\_text" class selector, I'll load our mixin with "@include u.breakpoint-down" and in the parentheses set it to "small". Then I'll move the "margin-block-end" style inside the mixin.

And now, when we save, on the website the input textbox doesn't have the space under it. And to check, if I switch to iPhone view, the space is under the textbox. Which is what we want.

Let's go back to an iPad view. And the other thing I'm noticing is that we need to add horizontal space between the input and the button. If we go back to the design to check, it looks like we have 20px of space between them.

Going back to our styles, I'm going to add the space by adding margin to the "form\_\_text" element. And after our small breakpoint, I'm going to create a new min-width breakpoint for medium and up by writing "@include u.breakpoint(medium)" and in it add "margin-inline-end: 20px".

Let's save, and I want to double-check that the space isn't there on mobile, so let's go to the iPhone view, and yes, the space on the right of the input isn't there, but the space under it is. And if we go back to iPad, the space under disappears, and the space to the right is visible.

I think the spacing is good now. Let's go back to the design and kind of eyeball the design, and then compare it to the website. And they are slightly different in size just because of the zoom. But, it does look like the textbox in the design is a lot longer than on the website, so let's check that out.

On desktop, the textbox is 300px wide. And let's also check mobile while we're here-- on mobile the textbox is 327px, which is happening because it's taking up 100% of the available width minus the 24px of space on either side of the mobile wrapper.

So in the design, the textbox is 100% of the width for small, mobile widths. Then it is 300px for tablet and desktop.

Now, going to the website, on mobile it is taking up 100% of the width, which works for mobile. Then on tablet it is [XXX] pixels wide, which is smaller than it needs to be.

For sizing the textbox, we haven't done anything to set the size of the textbox in our styles, so this width is coming from the browser default size. Maybe we'll try setting the width for medium and up to 300px.

In our styles, in the medium breakpoint, I'll add "width" and set it to "u.rem(300)", using rems because it's containing text, and we do want this to scale up if the browser base font size increases.

And now, the form looks a lot closer to the design, and if we inspect it, it is indeed 300px.

Now let's check how the form looks on all viewport widths. I'm going to turn off the grid highlighting so it's not so distracting. Then, in Responsive Design Mode, I'm going to select "Laptop" and then also go full screen on the website so we can see everything.

And that looks good. Let's reduce the viewport width to see how things change as we go down to mobile.

And this is around tablet widths, and it still looks good.

When we hit that breakpoint to below tablet, where the width of the textbox isn't set at 300px, it gets kinda wide, then as we get closer to mobile widths it's fine.

So, going back to right after hitting the breakpoint, it's pretty wide. If I inspect it, it is [XXX] pixels wide. So let's fix this by setting a max-width on the textbox.

[ Move website back to R, VS Code on L ]

In our styles, just in the default styles, I'm going to add "max-width" and then try maybe 400px, in rems, so "u.rem(400)".

And when we save it's a lot narrower. Maybe we'll decrease it a little more, like 350. Okay, I think that's good.

Now, there are some alignment issues again. If I inspect the form grid, and get the highlighting to show up, we can see that since the textbox has that max-width of 350px, it doesn't extend all the way across like previously.

But, if we try centering it by adding "justify-self: center", while it does center, the width goes back to that weird default browser width of the input element.

This is because we haven't set the actual "width" property, so the width was getting set based on either grid stuff or the default browser width.

If I uncheck the "justify-self" rule, the width gets set because it's stretching to fill the container due to the default "justify" behavior. So by adding "justify-self: center", we're removing the stretch, and with no actual "width" property, it reverts back to the default browser width.

We could try adding "width: 100%", so that it will stretch out and then get limited by the max-width to 350px. And that looks good. But, for those wider viewport widths just under the tablet width, you can see that the label, which is justified to the start, or left side, now that is off.

What we actually want in this situation is to limit the actual grid content itself to 350px, not just the textbox. This will make sure that all the grid children will not be greater than 350px.

Going into our styles, I'm going to select that "max-width" of 350 from our "form\_\_text" element, cut it, and paste it in the "form" grid parent. And when we save, the whole grid is limited to 350px, so the label is aligned correctly now.

But, we now need to center the grid within the larger CTA wrapper div. Right now, the headline and subheadline are centered with the "text-align: center" style, but that won't center block level elements like the form grid.

What we could do, is to center the entire grid by adding "margin-inline: auto", which is the same way that we've been centering all the wrapper divs. That looks good-- let's add that to our styles.

Now when we save, the entire form does look centered. You might notice that because we've set the max-width of the overall grid to be 350px, at the larger viewport widths we have some overflow because at those larger widths, we had set the textbox's width to 300px.

But even with the overflow it does look okay and centered, so you can leave it.

If that does bother you, you could go back to the styles, and in the medium breakpoint, cancel it out by adding "max-width: none" for those larger widths. And now if we save, on the website the overflow is gone.

Things look pretty good! Let's do one more check and start from iPhone-- things look good. And as we increase, the form goes to 2 columns, and up to desktop widths, the sizing and spacing and alignment still look good.

Ok, great! I think we can consider the Full-width CTA form now complete. We could have built this using grid lines like we have in previous parts of the website, but grid areas are a pretty cool way to set your grid template layout without having to use the actual line numbers.

Alright, let's do our usual thing and commit our changes in GitHub. In GitHub Desktop, in the Changes tab, I'll eyeball the files, and those all look good. So I'll add a message, I'll write "Full-width CTA add form" and press "Commit to main" and then push to origin.
