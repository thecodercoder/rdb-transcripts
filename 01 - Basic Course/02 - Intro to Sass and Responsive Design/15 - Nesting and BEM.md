# Nesting and BEM

So far, we've used BEM to create the classes for `grid` which is the block, then `grid__main` and `grid__sidebar` where `main` and `sidebar` are elements of the `grid` block. Now I'm going to add some more elements to the sidebar, specifically we'll add some sidebar widgets, which will be blocks of content within the sidebar itself.

First I'll start by adding to the markup in the index.html file. I'm going to move the content that we have in the sidebar currently into a new div. Let's create the new div that will have a class of `grid__widget`. Then I'll move the h2 tag and the paragraph tag into it.

And let's have multiple widgets in the sidebar. If I select the first widget and then hit Ctrl-D it will duplicate it. And I'll make the headline in the second widget say something a little different, like "Check out this cool thing!" And also, in order to make it look different from the first widget let's delete some of the text so the paragraph here will be shorter.

We have two widgets-- now let's make one more by duplicating the second widget and changing the headline and paragraph text.

When you're working from a design a lot of times the designer will put in placeholder copy, since the final copy is usually not ready until later on in the development process. So one thing I try to do is stress test what happens when there are different lengths of copy in the different elements. For example if you're building a series of cards, you need to know how it's going to behave if one title takes up 2 or 3 lines instead of just 1, and if the text in one card is a lot longer or shorter. So that's why I'm trying to make these cards look different, because we never know exactly what the final copy will be.

If we look at the website now, we can see each of the widgets in the sidebar! What I want to do is add some themes to the sidebar widget, and each of those themes will have a different background color. Let's start writing our styles in the `_grid.scss` file. After the `&__sidebar` block selector, I'm going to add a new block selector, `&__widget`. And, I'm going to move the background-color property from the `&__sidebar` selector into the `&__widget` selector. So now when we look at the website we can see each individual widget.
