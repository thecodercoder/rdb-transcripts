## Mobile grid layout

Let's look at our design and see what layouts we have for mobile and desktop. Starting on mobile, we have the label aligned to the left, the textbox taking up 100% of the available wrapper width, and the button is centered.

Then on desktop, we have the whole form centered in the wrapper, but the form itself has the label on its own row and again left-aligned. Then below the label we have the textbox and the button next to each other.

I think this layout is a great opportunity to use grid-template-areas in CSS grid. So far, when using grid, we've created an explicit grid template with a number and size of columns and/or rows. Then we use the grid lines to place the grid children where they need to go.

However, with grid-template-areas, we create our grid template by writing almost a diagram of the grid in our actual styles, with names for each area. It's a very different approach from using grid lines, and it may seem weird at first, but once you get used to it, it will make a lot more sense.

Looking at the desktop design, in our grid I'm going to have 3 grid children-- the "Email address" label, the email textbox, and the "Contact" button. The textbox and button are next to each other, which means we'll put them in the same row, in 2 separate columns. Then the label is above both of them, so we'll put the label in the first row, extending across both columns.

Then on mobile, we have a 1-column grid, with each grid child in its own row.

Let's now go into our styles and start creating our grid template. Previously, we were adding form styles in the form.scss file, because we wanted those styles to potentially be reusable if there are other forms on the website in the future.

However, these layout styles shouldn't be global form styles, because this layout is specific to the Full-width CTA section, and other hypothetical forms may have a different design and layout. So I think the best place to put these styles will be in the Full-width CTA Sass partial, which is "fw-cta.scss".

Let's use the Quick Open menu with Ctrl or Command P, then type in "fw-cta". Currently it looks like we only have the gradient background styles, and none of the other section-specific classes are getting used. To keep things simple, I'm going to delete the empty selectors to start off.

And, we should check on the HTML elements that we have for our form, because I think we'll need to add some section-specific classes to them. I'm going to right-click the fw-cta.scss file tab, select "Split down" and then in the top half load the index.html file.

Alright, so in the Full-width CTA section, we'll want to give the form elements class names so we can target them in our styles. Starting with the form tag itself, I'll add a new class called "fw-cta\_\_form". Again, I'm using the "fw-cta" BEM block name since we only want these layout styles to get applied in the Full-width CTA section.

In the form, for the label, I'll add the class name "fw-cta\_\_label". Then the input email textbox I'll add the class "fw-cta\_\_text". Then the button already has the class name "fw-cta\_\_button".

Now, down in the fw-cta.scss file, I'll add the selectors for the form elements. After the gradient styles, I'll add "&\_\_form", then "&\_\_label", "&\_\_text", and "&\_\_button". And let's save our styles and the index.html file, and I'll close the bottom duplicated Sass file.

[ index.html on L and website on R ]

In our website, I'm going to load the iPhone display in Responsive Design Mode, so we can start with the mobile styles. In the markup, our form element is the parent of the label, input, and button elements. So in our styles, the "fw-cta\_\_form" will be our grid parent.

In the form styles, I'll add "display: grid". And we can see that now by default, we've created an intrinsic grid where each grid child is put on its own row. And there are some default styles that is causing them to stretch out to full width.

We will fix the width and alignment a little bit later, but right now I'm going to start setting up the grid areas.

This is where we're going to use grid areas instead of grid lines to place the children inside the grid. To start, we need to give each grid child a unique name.

Let's start with the label, and I'll add "grid-area" as the first property before the other grid styles, and set it to the name I want to use, "label".

Note that here, we just write the name without any quotation marks. Next, the "form\_\_text" I'll add "grid-area" and set it to "text". Then for the button, I'll add "grid-area" and set it to "button".

If we save, we can see on the website that they're all overlapping each other. This is because we haven't placed the grid children, so by default they will all be placed in the first cell, causing them to overlap.

To get the layout to work, we need to position them using the grid area names. This is done in the parent, which in our case is the "fw-cta\_\_form" class element, using the "grid-template-areas" property.

This is the part that is going to be really different if you haven't used grid areas before.

So in the form selector, I'm going to add "grid-template-areas" and I'm going to start writing the grid-area names.

I'm going to add the "label" name first, and note that it needs to be in quotes here, even though it didn't need quotes when we named them in the "grid-area" properties down below.

I think the quotes thing is so that we can keep the rows separate from each other. I'll show you what I mean. So after the "label", I'm actually going to press Enter and below that I'll write "text", again in quotes.

And then below that on another new line I'll add "button". Then we'll have the closing semicolon.

Now when we save, we have each element in its own row. And one cool thing you can do is inspect the grid, and in the "Layout" tab, "Grid" panel, I'll make sure we have the "fw-cta\_\_form" grid highlighted.

Then down in the "Grid Display Settings" if I check the "Display area names" checkbox, on the website we now have the names of the grid areas that we created!

Pretty cool, right? Also, I'm doing this in Firefox, but you can do the same thing in Chrome to show the area names.

Right now the layout is a bit more simple, since everything is just in 1 column. But we'll see how things change with desktop later on.

Okay, I'm going to turn off the grid area names for now, and maybe also the grid line numbers since we're not using them. And next up, we're going to look at how to align the grid children.
