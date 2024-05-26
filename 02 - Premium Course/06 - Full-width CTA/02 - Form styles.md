## Form styles

Let's work on styling the form elements, starting with the button.

Style-wise, buttons, like other form elements, come with some browser specific styles like the gray color and border, and also the font family. So let's copy the classes from our fw-cta\_\_button, and see how things look. So I'm going to copy the whole "class" attribute and all the class names, and paste it in the button.

Now the button looks a lot closer. The font definitely looks different, and I can't tell if the sizes are different, so let's inspect the button and see what's going on.

With the button selected, I'm going to check the sizing in the "Layout" tab. It's 123.75 pixels wide by 41.333 pixels tall. Then if I click the anchor link button, it is also 41.333 pixels tall, which is good. And the width is different, I'm guessing because of the font family. And the other styles look good-- if I toggle between the two, they both have the same padding, and border.

Going back to the button, let's see what font-family is currently set. I'm going to click to the "Computed" tab, and filter for "font". And it says "MS Shell Dlg 2" -- I am using Firefox, so this will probably be different in different browsers.

But it is important to know that form elements will have their own default font family even if you've set a global font-family style in your body tag.

So staying on the "Computed" tab, if I click on the email textbox in the markup, it also has the same default font-family. If I click on the label, it doesn't have the default font, but it's using Source Sans, so we don't need to worry about that at least.

Let's set our form elements to have the same font-family as we have in the body tag. I'm going to create a new global style rule for this, since I'm pretty sure I want any and all forms to have the same font as the rest of the website and not the browser default.

I'm going to Quick Open with Ctrl+P and type in "boilerplate" and in the boilerplate.scss file, I'll create the new style right under the body tag. We want to affect form elements, and I'm going to use tag selectors.

So let's start with the "input", then a comma, and I'll add "button".

In this selector, I'm going to copy the "font-family" style from the body tag and paste it into the compound selector. And now, when we save, the first input button looks pretty much identical to the original anchor link button.

Let's inspect again just to check, and see if they're the same size. And it looks like they are the same width now since the font-family got changed. So I think we're good. I'm going to go back to VS Code and delete the anchor link since we just need the button.

We also need to set up the styles for the label and the textbox. So we should start by creating a Sass partial for the form styles. In the index.html file, we gave the form tag a class of "form", so I'm going to add some classes to the other elements, following our BEM approach.

The label I'll create a class and call it "form\_\_label". And then for our email input, I'll add a class called "form\_\_text". So that way in the hypothetical future, we can use this class name for other textboxes even if they are not email, like regular text, passwords, and so on.

Let's create our Sass partial, I'm going to open the left sidebar, and figure out where to put the form styles. I think maybe the "globals" folder, since we have the button styles there. So I'm going to right-click the "globals" folder and create a new file, and call it "\_form.scss". And we'll need to open the globals index.scss file and forward the "form" Sass module.

Let's close that, and also close the sidebar. And in the form.scss file, let's add our usual "@use '../util' as u" rule. And next we want to add the selectors for all the form elements. So I'm going to right-click the form.scss tab, select "Split down", and then in the top half load the index.html file.

Now we can add our class selectors, starting with the "form" class which is on the form tag. Then nested in it, we can add "&\_\_label" and then "&\_\_text". And that's all that we have at the moment.

Let's close the duplicate tab. And if we go to the desktop design and look at the "Email address" text, it is bold, and 18px. And on mobile, it is also 18px. So let's go into our styles and for the label I'll add "font-size: u.rem(18)" and "font-weight: 700".

We should also make sure the text box has the right font-size and padding. In the desktop design, the textbox text is 18px like the label, and it's regular weight, not bold. And it looks like on mobile, it's the same size.

In our styles, since both the label and textbox are the same size, 18px, I'm going to create a compound selector before the individual ones. And it'll be "&\_\_label comma &\_\_text". Then in that selector, I'll take the "font-size: u.rem(18)" style from the "label" and move it into the compound selector. And we want to leave the font-weight bold style since the textbox doesn't have that.

But we should also check the line-height for both. In the design, the label has a line-height of 18px, and the same for the textbox text. So let's add that to the compound selector, with "line-height: 1" to be equal to the font-size of 18px.

Let's save, and now on our website, we can see the textbox text is now bigger. Next we need to add padding to the textbox too. In our design, if I select the textbox text and hold down Alt, it looks like there's about 12px of space on top and bottom, and then 20px of space on left and I assume the right also.

So 12 and 20. In our styles for the ".form\_\_text" class, I'll add "padding" and set it to "u.rem(12)" for top and bottom, and then "u.rem(20)" for left and right.

And there was also a slight rounded corner on the textbox, so let's check that. And in our design if we select the rectangle, in the right the "Corner radius" is set at 5px. So let's add that too. In the "form\_\_text" selector I'll add "border-radius" and I'll use pixels for this since we don't care if it scales up or not, and just set it at "5px".

Let's save and take a look at the website. One thing I'm noticing is the textbox seems taller than what's in the design. And I can also see a slight border on the inside-- if I zoom in a bit, you might be able to see it better. There's a gray border around it, similar to the default button styles.

Let's get rid of that default border first. In our styles for the textbox, before the "border-radius" I'll add "border: none". And save, and now the border is gone.

I do want to mention that while it's ok to remove the border, we should not remove the "outline". That's what you see if you focus on the textbox, or if you tab through the form controls.

It's very important for usability and accessibility that the outline does change on focus, so that users know that they are highlighting the textbox.

But let's figure out what's going on with the textbox height. If I inspect it, and go to the Layout tab, we have our padding of 12 and 20 which is right. But in the blue content box itself, it should be 18px tall because we set line-height to 1, but instead it's 25.8333px tall. So that's kind of weird.

Let's check the label too, since we also set that to 18px. And that is also 25.8333px tall.

Since we explicitly set the font-size and line-height, the other thing that could affect the height on these elements would be if they were flex children.

Because flexbox will, by default, stretch the height of flex children unless you change the "align-items" property. But we don't have any flexbox, so it's not that.

The other thing that could affect the height is the default "display" value of these form elements. Let's check that on the "Computed" tab, I'll check the "Browser Styles" to show all default styles, and then filter for "display". So the label is by default "display: inline", and the textbox is by default "display: inline-block".

So let's try setting both to "display: block" to see if that fixes the height. I'll add it in the compound selector first. And when we save, this does kinda mess up the layout, but we'll figure that out later. The textbox looks the same-- if I inspect it, it's still 25.8333px.

The label does look like it's 18px tall now, which is good.

But let's figure out this textbox. Looking back at the "Layout" tab and the box model diagram, even though the font-size is set to 18px and the line-height is 1, the content height is still 25.8333. And the total height when we add the padding is 49.8333, so almost 50.

Let's compare this height with what have in the design. In the design, the textbox itself is 42 pixels tall. So on our website, we're about 8 pixels above that.

My guess is that the content height that we have is probably because of some default browser styles for the input textbox.

So while we could-- let me show you in the "Rules" tab-- control this by setting the height explicitly to 42px, in the "Layout" tab, this reduces the content height to 18px. And that works for the current design.

But if the font-size increased to bigger than 42px, let's add in "font-size: 50px", or even increase just to demonstrate this-- the text will start getting cut off because of that height limited to 42px.

So I know I've mentioned this before, but for elements that contain text, like this textbox or buttons, I think it's better to control the size with font-size plus padding, instead of setting a height or a width. That way it will scale more elegantly if the font-size changes.

Let's refresh to go back to our saved styles. And going back to our box model, we had said that with our current styles, the height of the textbox is 8px taller than what we have in the design.

Since the content height is getting controlled by some weird browser styles, what we can do as a workaround is to reduce the vertical padding by 8px total. So subtract 4px from the top and bottom padding.

Let's do that in our styles. In the "form\_\_text" styles, I'm going to change the vertical padding which is 12, and subtract 4 to get 8. Now let's save, and we can see the textbox is shorter. And if I inspect it, the total height with padding and everything is about 42px. It's slightly less but that's close enough for me.

Alright, so now we have the basic styles of the form all set. So we can work on the layout styles next.
