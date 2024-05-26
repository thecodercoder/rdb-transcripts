# Sharing styles

I mentioned earlier that this Full-width style has some similarities to the Full-width Feature section earlier in the website. So let's go up and take a look at that to see if there's any shared styles that we could use here.

The Full-width Feature section is similar in that everything is centered, and the text color is white due to the magenta background. I'm going to inspect the styles to see where we set them. In the `fw-feature` section tag, we set the background-color, the text color, and set `text-align: center` which, if we uncheck that box, is controlling the headline and paragraph text alignment.

The wrapper div doesn't seem to have anything section-specific, and neither does the h2 tag. The paragraph tag has a `margin-inline: auto` rule to center it within the section tag, because we set a `max-width` of 70 ch or characters. If I uncheck the `margin-inline` rule, you can see the paragraph tag is limited to that 70ch width and is aligned to the left. And we want the `max-width` so that it doesn't go all the way across the section, for better readability.

We don't have an image tag in the Full-width CTA section, so I don't think we need to worry about that too much. But the other style rules for centering, text color, and the paragraph styles are ones that we would also need for the Full-width CTA section.

And while we could simply write the same style rules, it would be more efficient if we could figure out a way to share styles. Fortunately, there are multiple ways that we can share styles.

One option is to use a Sass at-rule called `@extend`, which lets you use the rules from a different selector in your current one. And related to that, we can use a Sass feature called `placeholders` that work with the `@extend` at-rule so that you can use the placeholder styles in multiple places.

Another approach is to use Sass mixins to generate a set of style rules anywhere that the mixin is included. And lastly, we can create a helper or utility class for these shared styles, and then add the class to both the Full-width Feature and Full-width CTA sections.

As is often the case, I don't think there's 1 single approach that's the best. A lot of it depends on your own preferences when writing styles, or your company's existing approach. But I do think that it's useful to know all of these approaches, in case you encounter them in the future. And then you can compare and decide which one you like the best.
