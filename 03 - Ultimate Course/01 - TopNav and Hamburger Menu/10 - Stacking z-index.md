## Sticky nav and z-index

Let's also make the top navigation sticky, so that if you scroll down it will remain visible for both mobile and desktop. We can do this by setting the position to "sticky", but let's see which element we want to add it on.

If I inspect the top navigation on the website, I think we'll want it to be set on the "topnav" class header tag since that contains all the Top Navigation content.

In our topnav styles, we can add this in the main "topnav" class selector. So I'll add "position: sticky" and we also need to say where we want it to stick. I want it at the top, so we'll add "top: 0" meaning zero pixels down from the top.

Let's save and test this out. And the mobile site looks good, and on desktop, the sticky nav is working!

[ stay on desktop ]

Okay, one thing I'm noticing is that when we scroll down, it looks like the Testimonial content is overlapping the Top Nav, which we definitely don't want to happen.

And if I switch to mobile again, and scroll to the Testimonial section, and open the menu, the Testimonial content is on top of the menu. And it also looks like it's on top of the overlay too.

When you're working with different types of positioned properties, like sticky or absolute, it's almost a guarantee that at some point you're going to run into stacking issues. Meaning, you'll have elements that are on top of other elements that you don't necessarily want to happen.

And if you've worked with stacking before, you may have also used the z-index property. And while on a basic level it makes sense, that giving an element a higher z-index number will put it on top of the stack, it doesn't always work out that way.

Which is why you might see other people or yourself trying to put z-index at like 99999, but it still may not do what you want.

So, how exactly does stacking work in the browser, and why is it so tricky sometimes?

What the browser is doing is seeing elements on the page in terms of what's called a "stacking context". I didn't make up this term, and if you think this sounds confusing, I completely agree with you.

However, this is what it's called, so I'm going to try to explain it to you the best way I can.

So stacking contexts are basically groups of elements on the page which can get stacked above or below each other.

The entire document of the site, meaning everything in the &lt;html> tag, is by default, one stacking context. And all the elements on the page are on the same level, which is sometimes referred to as "Layer 0".

However, things start to change if any of the elements get styled with certain properties that will enable them to get positioned on top of the other elements.

This is what's called a "stacking context", and you can have multiple stacks in one website.

In our case, when we added "position: fixed" to the "topnav\_\_menu" and "topnav\_\_overlay" elements, that put each of them in a new stacking context.

Because when you set the "position" property to something other than the default value of "static", this will create a new stacking context.

This enabled them to be displayed on top of the other elements on the page, which is why when we scrolled down, the menu was on top of the rest of the website.

Also, by default, elements that are on the same level will get stacked in order of their appearance in the markup, with latter elements being on top of earlier elements.

This is why the "topnav\_\_overlay", which comes first in the markup, gets put under the "topnav\_\_menu". Because the menu comes after the overlay in the markup, so gets stacked on top of the overlay.

This is also why the Testimonial content is getting stacked on top of both the menu and the overlay.

If we look at the Testimonial section code, the figure tag has its position set to "relative". This also created a new stacking context, which raised the Testimonial content above Layer 0.

And, since the Testimonial content comes after the Top Nav in the HTML markup, that put the Testimonial content above it in the stack. Which is why the Testimonial content is displayed on top of the menu.

And at this point, we hadn't added z-index to anything. But just by having that position property set, it began creating these different stacks.

So what happens if we start trying to add z-index to make the menu be on top of the Testimonial content?

In our styles, for the ".topnav\_\_menu", I'll add "z-index" and set it to 10. Theoretically, this should put the menu on top of the Testimonial, since the Testimonial only has "position: relative" and doesn't have a z-index.

But when we save and go back to the website, if I open the menu, the Testimonial is still on top of the menu! What's going on here?

Unfortunately, there is another part of z-index and stacking that can throw a wrench into things. This involves parent elements.

Remember that we made the header tag sticky with "position: sticky"? Well, as I mentioned earlier, setting "position" to anything other than the default "static" will create a new stacking context.

So the header tag being position: sticky creates a new stacking context. And because the menu and overlay are children of the header, they are forced to conform to the stacking order of the parent.

Since the header has no z-index, it and all its children, will still be below the Testimonial content since that comes later in the markup order.

And the z-index of 10 that we set on the menu will only take effect inside the header. So it could put the menu on top of other elements within the header's stacking context, but it has no effect outside the parent.

I think this is the part of z-index that trips up people the most, including myself. So how can we fix this?

What we want is for the entire header to be on top of the Testimonial. So we need to add a z-index so that it will be higher in the stack.

In our styles, I'm going to take remove the z-index: 10 from the menu since it's not doing anything, and instead put it in the topnav header styles.

This will move the Top Nav header tag, along with all its children, above the Testimonial content.

And we can see that now the sticky header and the mobile menu are on top of the Testimonial content!

That seems to have fixed all of our stacking issues. And one more thing-- you know how I mentioned that setting position to something other than the default "static" value will create a new stacking context?

There are other CSS properties that will also create a new stacking context. If we search for "mdn stacking context" we'll go to the MDN page, and if we scroll down a bit, they list out all the ways you can create new stacking contexts.

It is a lot, but just to highlight some of the more common ways-- flex or grid children, setting opacity to less than 1, using mix-blend-mode, as well as other properties.

And, if you for whatever reason need to create a stacking context but don't want to add one of these properties, you can create one without any "side effects" by setting "isolation: isolate". And this will let you place the element on top of other elements without having to set position: relative or any of these other properties.

So if you're ever working on a website and you can't figure out why an element is layered on top of another element, you can come back to this page and see if any of these properties are causing the weird issues.
