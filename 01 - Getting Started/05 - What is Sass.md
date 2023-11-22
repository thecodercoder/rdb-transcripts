# What is Sass?

Alright, so we've started setting up our project files and folders. Now let's talk about Sass. Obviously when making websites, we want them to look good, and the way we do that is by writing style rules in CSS, or Cascading Style Sheets. However, especially if you're building large and complex websites, your CSS files can get really long and convoluted. This is one reason why developers often write their styles in Sass!

So what is Sass? Sass stands for "Syntactically Awesome Style Sheets" and is a CSS preprocessor.

The Sass language has features that makes it easier and more efficient for developers to use. But since browsers can't read Sass directly, you need to compile or process your Sass files into CSS in order to work on websites.

There are two syntaxes that you can use when writing Sass. The original syntax, just called "Sass," is similar to CSS but doesn't use curly brackets or semicolons, instead simply relying on indentation and new lines to differentiate your style rules. Files using this syntax have the extension `.sass`.

SCSS is the more popular syntax and the one that we'll be using in this course. It is much more similar to pure CSS, and an added benefit is that any CSS style rules are valid in SCSS as well. This means you can copy and paste pure CSS into your SCSS files with no problem. SCSS files have the extension `.scss`.

In this course I might say both "Sass" and "SCSS" when talking about styles, but just know that I'm always referring to the SCSS syntax when I do.

So, what's so great about Sass? Well, here are some of the major features in Sass that, in my opinion, make it awesome.

First off, Sass lets you separate your styles out into multiple files called partials. With partials, instead of having to search through one giant long CSS file, you can store your styles in separate files. For example, you can keep all the styles for your website header in the `header.scss` file, the styles for your sidebar in `sidebar.scss`, and so on.

This helps a ton when you have to fix a bug in, say your footer. If you know that all your footer styles live in a file called `footer.scss`, you can locate it much more quickly and easily.

You can also store your Sass files in different subfolders for additional organizing, which is great when you have a lot of files.

Sass partials also make working on a team with other developers easier. Since the styles are all in separate files, it reduces the chances of someone else working in the same file at the same time as you are, and creating a potential code conflict.

One of my favorite Sass features is the ability to nest your style rules. This means that you can put a child style rule inside the style rule of its parent. This maintains the specificity of the child selector without having to keep typing the parent selector out. It may not be a big deal for one child element, but if you have dozens of child classes, this will save a lot of needless typing and repeating of the parent class!

There's also the ampersand symbol which is a shorthand that refers to the parent selector. The ampersand combined with nesting helps a lot to reduce the amount you have to type, and it's awesome when you're writing styles in the BEM or block-element-modifier system.

If you're not familiar with the BEM format, that's totally fine-- I'll be showing you how BEM works in the "Intro to Sass" section of this course.

Mixins are another great feature of Sass. You can use mixins to create sets of style rules that you want to reuse with the `@mixin` at-rule, and then reuse those rules anywhere else in your styles.

Before CSS custom properties came on the scene, Sass variables were a huge plus that let you store values for fonts, colors, and other properties. Nowadays, I've switched my Sass variables over to CSS custom properties for many cases, especially colors. But I'll still use Sass variables for a few things in this course. It may come in handy in case you have to work with a project or a framework that uses them.

Again, for each of these features that I've talked about we'll be going how to use them in more detail later in this section.

Alright, so we've talked about the great points of Sass and why I love it. But there is one main downside to using it. And that's that you need a tool of some kind to compile your Sass files to CSS. Whereas if you use pure CSS you can immediately load it in the browser and it works fine!

In my opinion, the benefits far outweigh the costs. And adding knowledge of Sass to your resume will always help you when you're searching for a job.

In the next section I'm going to cover two options that you have in this course for compiling Sass.

The first option is more beginner friendly, using the VS Code Live Sass Compiler and Live Server extensions with just a little bit of customization in the settings. These extensions are a great tool for when you're just working locally in your own projects and need to compile Sass with minimal setup involved. If you want to follow this beginner route, go ahead to the video on the Live Sass Compiler.

The other option is more advanced, using a Gulp workflow that will require you to install npm packages and run scripts on the command line. There is a lot more setup involved in this, but it's closer to what you would be doing in the real world for development and deployments. If you want to follow that more advanced route, go ahead to the videos on npm and Gulp.

Feel free to choose the option that feels most comfortable for you at this moment. If you go the beginner route first, you can always come back later on and try the more advanced route.

So let's get into the Sass compiling!
