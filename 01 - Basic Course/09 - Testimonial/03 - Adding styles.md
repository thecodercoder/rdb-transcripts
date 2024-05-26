# Adding Styles

First up in our styles, let's create our Sass partial for the Testimonial styles. Since we're using `testimonial` as our BEM block name, we'll want to create a Sass file with that file name. In our scss folder, this should go in the `components` subfolder since the Testimonial section will include styles that we only want to use in that section.

In the scss/components folder I'll create a new file and call it `_testimonial.scss`. And since we're creating a new partial, we need to open the components index.scss file and @forward the `testimonial` partial.

And let's go back to the testimonial.scss file, and up at the top, we want to load our utilities by writing `@use` and then the path to the util folder, `../util` and we're loading it as the namespace `u`.

Next up, I want to add selectors in our Sass file that correspond with all the classes that we have in our index.html file. I'm going to right-click the testimonial.scss file, select `Split down`, and then in the top half go to index.html. So now we can see the HTML and the classes in the top half, and our styles in the bottom half.

The first selector will be our block name class, `testimonial`. And then we'll add curly brackets, and in them we'll add the next element, `testimonial__wrapper` with the ampersand, double underscore and `wrapper`. After that will be `testimonial__icon`, and then `quote`, then `author dash wrapper`, `author dash image`, and `author dash description`.

And that should be it for the Sass selectors. I'm going to close that bottom testimonial.scss file, and let's see what we should work on first in the website.

In our website we have all the content there. I do want to inspect the different semantic tags that we added, like `figure`, `blockquote`, and `figcaption`, just to check what default browser styles they have that we might need to cancel out.

If I inspect and hover over the `figure` tag, it looks like we have some margins added-- margins are highlighted in yellow. Then the `blockquote` tag also has some default margins. And the `figcaption` looks like it doesn't have any default styles added.

I do want to zero out the margins for the figure and blockquote. I think I'll add those styles in our boilerplate styles as opposed to the testimonial styles. This is because if I need to use any of those tags again in the future, I'd like to only have to zero out the margins once instead of having to do it in each section.

In VS Code, let's go to `scss/globals/boilerplate.scss`. And I'll put this rule after the image tag. For our selector we'll do a compound one with `figure, blockquote` separated by commas. And then in the curly brackets I'll set `margin` to zero.

Now, going back to the website, and when I inspect the figure and blockquote tags, they no longer have the default browser margins. So we should be good to start adding our Testimonial styles. I'm going to start with colors, text styles, and spacing. And then once we get all those set we'll work on the layout styles.
