## Aligning grid children

Alright, so let's take a look at the grid that we have currently.

So, we can see that the textbox and the button are taking up the full width of the container. And actually, if we hover over the "label" we can see that it's also full-width, even if the text isn't as long.

The reason that the elements are going full-width is because of the default values of the "justify-content" and "justify-items" properties.

I want to take some time to explain these two properties, as well as another one, "justify-self" to you-- we touched on them briefly in the Hero section.

All the "justify" properties control the alignment of the grid children along the inline axis of a grid, which in our case means horizontally. But they do so in slightly different ways.

And I do think it's important to understand what they actually do in practice, as well as what some of their default values do, because it can help explain some confusing behaviors that you might run into.

So, let's start with "justify-content" and "justify-items", which are properties that you set on the grid parent. Both of them default to "normal", which ends up meaning "stretch" in most cases.

And that's what's happening here. We can change this full-width effect by changing the value of either "justify-content" or "justify-items" properties.

Let's first look at justify-content. In our styles, for the form, I'll add "justify-content: center".

Now what's happening is that the children within the grid are no longer stretching to the full width of the container. We can see the extra space in the grid with that shaded space on the left.

And it's hard to see, but there are vertical dotted lines on the left and right of the grid column. If we toggle the "justify-content" back to the default stretch, the lines go all the way out to the container.

However, even if we toggle back the "justify-content: center", the button still is stretched out.

This is because "justify-content: center" does get rid of the full-width stretching, but the grid children each have a default value of "justify-self" of "auto", which ends up meaning "stretch".

[ Layout tab, go to grid diagram ]

I know this sounds kind of confusing. Even though we set the grid children to be centered so that they won't stretch full-width, what's happening is that the width of the grid column that's currently containing all the grid children is being controlled according to whatever is the grid child with the greatest width.

[ hover over each row ]

Then, with each grid child individually stretching by default, what happens is that the children with smaller widths stretch to fit the same width as the largest width.

Now, what determines the greatest width? This could be due to the amount of text, like if you had a really long line of text, or if an element has a width explicitly set.

In our case, the textbox input element has a width controlled by the browser. This is again, one of those tricky behaviors that browsers have for form elements that you can't always see even if you look through all the styles.

If I go to the Box Model panel, then in the Markup View select each of the grid child elements, it tells us that each one is [XXX] pixels wide.

And it looks like the biggest width is coming from the textbox, since the "Email address" text is smaller, and the button looks like it is stretched out.

So what will happen if I explicitly set the textbox input to have a super small width like "width: 10px"? It gets super narrow, and the button shrinks down. And now, the label and the button are both [XXX] pixels wide.

It's hard to tell if the largest width is coming from the "Email address" text or the button-- if I edit the label to just say "Email", then it stays at that width, which tells me that it's stretching to the width of the button.

Then if I make the label really wide by adding a bunch of text, it gets longer and the button now stretches to match the width.

So that's part of how justifying the grid children will behave. It can get weird with the default stretching, but just know that one way you can fix that is by setting "justify-content" to something.

Let's reload the website to go back to our saved styles, with "justify-content: center". And if we go to the grid inspector and the diagram, hovering over each row shows us that the grid content as a whole is not full-width, but shrunk down to the widest grid child, the textbox.

Keep that in mind, and now let's look at "justify-items" and see how it compares.

I'm going to go back to the form styles just in the browser, and instead of "justify-content", I'm going to change it to "justify-items: center". Going back to the grid diagram, the grid content is back to being full-width of its container.

But in the Markup View, if we hover over each grid child, you can see that instead of stretching to the widest grid child, each one now is only the width of their own content.

This is why button is no longer stretching out. This is the difference between "justify-content" and "justify-items".

"Justify-content" aligns all the grid children as a whole within the container, and "justify-items" aligns each grid child within its available space.

However, we actually want each grid child to have a different alignment. We want the label to be aligned to the left, the textbox to stretch to the full width of the container, and the button to be centered and not stretched.

We can align each child individually with the "justify-self" property, which is set on the grid child elements, instead of the grid parent like "justify-items" or "justify-content".

This is useful if the children need to be aligned differently from one another, instead of setting them all to the same value with "justify-items".

Let's go into VS Code, and remove the "justify-content: center" rule that we added before. And on the website everything is stretched out full-width again.

Now, for the first grid child, the form\_\_label, we want it to be aligned to the left. In grid terms, this equates to "start". So I'm going to add "justify-self: start". And when we save, the label is aligned to the left.

For the "form\_\_text" element, we don't have to add anything since it's stretching by default.

For the last child, the "form\_\_button", if you want to try this yourself, pause the video here, and then see if you can figure out what to set "justify-self" to.

[ pause ]

Okay, so the button we want to be centered and not stretched. We can do this by setting "justify-self" to "center". And now the button is the width that we want it to be.

So I think our alignment is all set for mobile. Now as you can probably see, we need to add space between the grid children. Let's go to the design to see what we want to set these at.

On mobile, if I select the textbox and hold down Alt, there is 12px of space under the label, and then 20px of space under the textbox. Usually I would add space in a grid with the gap property, but unfortunately you can't set different gap sizes. So I'm going to add all the spacing using margin instead.

In our styles, in the "form\_\_label" selector, I'll add "margin-block-end: 12px". And then in "form\_\_text" I'll add "margin-block-end: 20px". And now the layout looks pretty good!

Let's put the design up and compare them. I'll try to put the mobile up on the left side, and let's have the website on the right. And they look pretty identical to me. So I think we're good for the mobile styles.

Now, let's get to the desktop layout styles. It is slightly more complicated than the mobile version, because the button is next to the textbox, and the textbox and button are on the second row, under the label.
