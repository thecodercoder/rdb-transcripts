# Order of media queries matters due to the cascade

One more thing that I want to mention is that if you have multiple media queries for a selector, the order is very important. To illustrate this, let's experiment with giving the main content different background colors at different viewport widths.

We'll start with the blue color that we already have for mobile. Then let's create a new breakpoint for medium, and we'll set the medium to a green color. Then we'll add another media query for large or desktop, and make the background color orange.

Now in the browser we can see as we slide the inspector panel, that the background color does change from blue to green to orange.

This is working because in our styles the medium breakpoint is saying, at viewport widths of 700px and up, set the background color to green. And that style rule will override the default mobile style rules of blue. Then our second breakpoint says, at viewport widths of 900px and up, set the background color to orange.

And this is what we want to do for min-width media queries. The default styles are for mobile, then as the viewport width increases it will trigger the medium, large, and then xlarge breakpoints.

But, what happens if we put the media queries out of order, so that the large breakpoint is listed before the medium breakpoint? It's saying, default color is blue, then at widths of 900px and up set the background color to orange, but then on top of that, at widths of 700px and up set the background color to green. At desktop withs, do you think the background color will be orange or green? Let's find out.

If you thought green, you are correct! And if we look at all widths from desktop down to mobile, the background color is green except for mobile which is blue. Why did this happen? This is due to the `cascade` in our styles, which is how CSS determines which styles will ultimately be used on the website for a selector. And this is why CSS stands for "Cascading Style Sheets."

In CSS, if you have two rules that are the same level of specificity, the rule that occurs later on in the styles will override an earlier rule. So what's happening here is that the medium media query, which is 700px and up, is overriding the large media query for 900px and up, because it comes after the large media query in our code. Just for illustration purposes, what happens if we add another medium media query and set the background color to red?

If we look at the website, the background will be red. And again, this is because the style rule with the red background color is overriding the style rule before it, with the green color.

So putting the media queries back in the correct order, I'll delete that last red background color rule. And we'll have the default or mobile background color of blue, then for medium and up the background will be green, and for large and up the background will be orange.

And let's check that that's working in the website. And it looks like yes, the background is going from blue to green to orange as the viewport increases.

So, going back into our styles, when you're working with min-width media queries, you want to order them in increasing viewport widths. So starting with mobile and then going on up. And this is because the min-width media queries are saying, use these styles when the viewport width is at least this width, and on up. Then you can keep tacking on increasing viewport width media queries.

So our styles here are saying, use a blue background color, and then at viewports that are greater than 700px use a green background color, and then at viewports greater than 900px use the orange background color.

So then, what about max-width media queries like we have in the sidebar? For these, the default styles are desktop styles, and then you add media queries for viewports that are up to a certain width. So for our text-align center rule, we're adding that for viewports that are 899px and less. And that is for tablet widths. Then if we wanted to add another text-align rule for just mobile, we could add another breakpoint-down media query for "small" and set the text-align to say, text-align: right.

Our styles are now saying, use the default text-align: left, unless the viewport is 899px or less, then use text-align: center, and then if the viewport is 699px or less, use text-align: right.

You can see that this is a bit opposite of what we did with min-width media queries. When we're using max-width media queries, the default styles are for desktop widths, and then we keep tacking on decreasing viewport width media queries.

It can be kind of hard to wrap your head around min-width and max-width media queries and breakpoints when you're first starting out. Don't worry if it seems kind of confusing at the beginning.

But if you're noticing that your styles in media queries don't seem to be taking effect or are weirdly getting overwritten when you don't want that, try checking the order of media queries for that selector to see if maybe something is out of order. And try to play around with the order to see if it fixes your issue.
