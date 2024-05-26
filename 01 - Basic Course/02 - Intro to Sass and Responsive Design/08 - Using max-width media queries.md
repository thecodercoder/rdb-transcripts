# Using max-width media queries

So our breakpoint is going to create the min-width media queries that we need. But there are some instances where I do want to use a max-width media query, if there are more mobile style rules than for desktop.

One example of this in our demo website could be if we wanted to have the sidebar text centered on mobile only, and not on desktop or tablet. We'd want a style rule saying `text-align: center;` for mobile, and we wouldn't want any text-align rule for tablet or desktop since they would use the default left-align.

If we used a min-width media query for this, we'd have to set `text-align: center` for our default styles, then add a media query to cancel it out with a `text-align: left` for tablet and desktop widths. So you'd be saving having to write that extra `text-align` rule with a max-width media query. This might seen very minor since it's only one line of code, but there could be cases where you'd have multiple style rules that you only want on mobile. So in those cases a max-width media query would save you time.k

Let's create a new mixin for that. Going back to VS Code in our `_breakpoints.scss` file, we need to create a new Sass map for the breakpoints. We need a slightly different set of widths so that there won't be any overlap in breakpoints which can cause weird behavior on websites.

Our breakpoints-up map used 700px, 900px, and 1440px. We'll make a new one called `$breakpoints-down` and in that we want to use the names `small` for 699.98px, `medium` for 899.98px, and `large` for 1439.98px. There's a 0.02 pixel difference between the values in `$breakpoints-up` and `$breakpoints-down` to avoid that overlap. And I got that 0.02px number from researching Bootstrap-- they use that difference as well.

Then we'll create a new mixin called `breakpoint-down` that will also have that `$size` parameter, and it will write a media query using `max-width`, and use `map-get` with the parameters `$breakpoints-down` and `$size`. And in the media query it will load `@content` to add in whatever style rules the mixin contains.

Now we can use our mixin in our styles for the sidebar, to make the text center aligned. In the `_grid.scss` file in the `.grid__sidebar` selector, I'll load the mixin with `@include` and the name of the mixin we just made, `u.breakpoint-down` with that `u` namespace for util. And we will set the parameter to `small` so that it will take effect for devices that are 699.98px and smaller.

Let's see if that works in the website. In our browser, if we slide the inspector panel over to make it a mobile width, we can see that the sidebar text is indeed center aligned. And if we test using the device emulator, it is center aligned for iPhone, and if we select iPad it will be back to the 2-column and left aligned style. And one thing to note is that in the inspector, the breakpoint width has been rounded a bit by the browser. We originally wrote `56.24875em` but Firefox has rounded it up to 56.2488em.

And, just to illustrate why we have that 0.02px difference in our `$breakpoints-down` map, let me change the `medium` value to `56.25em` to match the `$breakpoints-up` map. When we save and go back to the browser, if we slowly slide over the panel, you can see that there is a tiny viewport width where the layout is in 2-columns but the sidebar text is center aligned.

This is an edge case since it only exists at basically one pixel specific width, but you never know how large a user might be loading your website, so ideally you want it to look consistent at every single viewport width. Also, I used to do a 1px difference, but noticed that it caused the media query to trigger 1px too `late` when you're narrowing the viewport, which is a similar issue. It's not the biggest deal in the world, but having that 0.02px difference seems to be the best solution.
