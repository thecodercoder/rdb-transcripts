## Alternating styles

To start off, let's refer back to the design to see how it should look. On mobile, the image is first, and then the text stacked underneath it. Then just on desktop, the first row has the order flipped, with the text first on the left and then the image second on the right. The second row matches the mobile order, and then the third row is again flipped.

So what we need to do is to figure out a way to change the order of image and text on every other row, starting with the first row. Let's first focus on how to target every other row in CSS, and then figure out how to change the order of the items.

Thankfully, CSS has some really handy pseudo-classes that we can use to accomplish this. Earlier, I mentioned that we could use the "last-child" pseudo-class to target the last "alt-feature\_\_row" div. There's also a "first-child" pseudo-class that will target the first element in a group of sibling elements.

And if you need to target a specific child in the group, the "nth-child()" class lets you use a number to target whichever child you need.

Let me show you what I mean in the browser. I'm going to select of the "alt-feature\_\_row" divs, then click the "plus" icon to add a new selector based on the class name. Then I'll add a rule, "outline: 2px solid blue", which will then add a blue outline to all elements that have the class "alt-feature\_\_row".

If I change that selector to be "alt-feature\_\_row:first-child", it will target only the first row. And I can use "last-child" to target just the last row.

Then, if I change it to "nth-child(1)", it will target the first row. Changing it to "nth-child(2)" will target the second row. And as you might imagine, "nth-child(3)" will target the third row.

However, some of how these pseudo-classes work isn't super intuitive. Let me show you what I mean.

First, let's add this selector to our code so it will stay there even if we reload. In the alt-feature.scss file, I'm going to go to the "alt-feature\_\_row" selector and add one targeting the third row with "&:nth-child(3)" and then adding the style rule "outline: 2px solid blue".

Now let's save and reload, and on the website we have the third row with the blue outline.

Here's where things get tricky. In the index.html file, let's fold up all the "alt-feature\_\_row" divs.

nd I'm going to add a blank div to the group, after the second "alt-feature\_\_row" div. And I'll add some "test" text to it. Now, if I save, the third "alt-feature\_\_row" div loses the outline.

Which seems weird, right? Because you might think that the selector "alt-feature\_\_row:nth-child(3)" will find all the divs that has the "alt-feature\_\_row" class and target the third one out of those.

But it's not. It's looking for the third element in a group of sibling elements, then if that third element has the class "alt-feature\_\_row", it will target it. In our case, the third element in this group is the test div with no class name, and so it doesn't meet those requirements.

And if I add the "alt-feature\_\_row" class to the test div, it will have the blue outline since it is the third child, and it has the class "alt-feature\_\_row".

Let's delete the test div, and now the third child is the last "alt-feature\_\_row" div, and it's getting targeted.

So that's one tricky part about using these "nth-child" and other "child" related pseudo-classes. Because they are looking through groups of sibling elements, meaning all on the same level, then finding the element that has the order number you're looking for, and then if that element matches the class or other selector, only then will it apply the style.

This is a pretty unintuitive way of working, but unfortunately that's how it is for now-- so I wanted to explain to you how it works so hopefully you won't get tripped up as badly as I've been with these types of selectors.

Now, let's get back to how to target every other row. Another parameter you can use with the "nth-child" pseudo-class is "odd" or "even", which is very helpful for our situation! I'm going to edit what we have and change it to "nth-child(odd)". Then when I save, the odd number children have been targeted-- meaning the first and third rows.

One other thing I wanted to mention is that if we inspect the first "alt-feature\_\_row", in the "Rules", Firefox has changed "odd" to "2n+1". This is to denote odd numbers, starting with n = 0. So if n equals zero, 2n + 1 becomes zero plus 1 which is 1. Then if n is 1, 2n + 1 results in 2 + 1 = 3, which is the next odd number. And so on.

And in the same way, if just in the browser, we change the selector to "nth-child(even)", it will get rewritten to "2n" which will target all even numbers.

Going back to our styles, we only want to change the alternating styles for desktop viewports. So in the alt-feature.scss file, I'm going to take that "nth-child(odd)" pseudo-class and move it into the large breakpoint of the "alt-feature\_\_row" selector.

And when we save and load the website, if we change the viewport to a mobile width, we can see that the outline only will happen on desktop.

Now, how do we want to change the order of the children in this selector? If you want to try to figure this out yourself, pause the video here, and then play it when you're ready.

[ pause ]

Alright, so with flexbox, we can change the order of the children using the "flex-direction" property. Right now it's set to "row" which is ordering from left to right. We can flip that in the nth-child(odd) selector, by setting "flex-direction" to "row-reverse". And if we save, the first and third rows are indeed switched!

And just to check, let's load iPhone view, and all the images are first, with the text underneath. Cool!

[ close Responsive Design Mode ]

Now I think we can remove that blue outline from our styles, since everything seems to be working. And let's do a test starting with mobile view, and increasing the viewport width until we hit that 2-column desktop layout.

Alright, things are looking good! Looking back at Figma, the design seems to match what we have on the website. So I think we can consider this section complete.

Let's commit our code changes in GitHub. In GitHub Desktop, in the Changes tab, let's just eyeball all the changes and make sure that there aren't any files selected that we don't want to commit. But everything looks good, so I'm going to in the bottom left write a commit message, "Alternating Features" and then click the "Commit to main" button, and then "Push to origin."

So, that's it for the Alternating Content section! Next up, we'll be tackling the Premium version of the Testimonial section.
