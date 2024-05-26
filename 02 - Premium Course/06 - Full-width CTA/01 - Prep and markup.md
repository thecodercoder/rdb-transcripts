## Prep and markup

Alright, in this section we're going to be making some changes to the Full-width CTA section. To start, let's look at what the section looks like now, and what we'll be building in our design.

[ Show current website, desktop view ]

Here's our website and the CTA section. It has the gradient background, then a title, paragraph text, and a white call-to-action button that says "Free Trial." And all the content is centered.

And if we turn on Responsive Design Mode and load it in iPhone view, it's pretty much the same, except that the gradient is a bit different.

Okay, let's now go to Figma to see what changes we'll be making. First, in the desktop design, the headline is the same, but the description text is a bit different-- it says "Contact us to find the next undiscovered unicorn." Then under that, instead of just a CTA button, we now have a simple form with an email address field, and the button now says "Contact".

And on mobile, the copy and the form are similar, except that in the form the email textbox looks a bit wider, like it's taking up 100% of the width of the wrapper. And then the button is under it and centered.

I do want to mention that we're not going to add any actual functionality to this form-- I'm just going to show you how to write the HTML and the styles for it.

Let's start updating the website, starting with the easy part, putting in the new copy for the description. I'm going to copy the text, then go to VS Code, and in the index.html file we want to go down to the "fw-cta" section. And in the paragraph tag I'm going to paste in the new copy.

And while we're here we can update the button text too, to say "Contact". We'll be making more changes to the button when we build the form out, but for now let's leave everything else.

Alright, now the website has the updated description and button text. Let's start building the form in our markup.

Forms are an interactive part of websites, where you input information and then submit it to the website by pressing the submit button. And in order to make sure the form elements are accessible and functional, we should use the correct markup.

First of all, forms need to live inside an HTML form tag. So I'm going to create a form tag after the paragraph and before the button. In Emmet, you can see there are options for a "GET" and "POST" version. I'll just select "POST" but it doesn't matter which one you choose because we're not doing anything functional.

Very briefly, the "GET" and "POST" methods in the form dictate how the information in the form gets sent to the web server. There's a lot of overlap in GET and POST, but you can think of GET as retrieving data from the server-- one example might be submitting a search form and then "getting" the data in the form of search results. For POST, you can think of something like what we're building-- a contact form that when you submit, will save the email address in a database.

The "action" attribute will be the URL that the form data gets sent to. These functionalities of the form will need back-end code to communicate with the web server, or you might use an API-- these concepts are beyond the scope of this course, so I'm going to delete the attributes from the form tag. But I wanted to give you a very brief overview of them so you have a little context.

Also, I want to add a class to the form tag, so we can target it for our styles. I'm going to set it to "form", and we'll be creating a Sass partial for these form styles a bit later on.

Alright. So, in the form we have the form elements-- they could be things like textboxes, dropdown menus, radio buttons, and checkboxes. Most of them are created using the "input" HTML element. So to get a better idea about what form inputs are, I'm going to search for "mdn form input" and then go to the first result, "The Input (Form Input) element".

In the example, we can see that we have a textbox, and then a label that says "Name (4 to 8 characters)". And under it, is the input element, with several attributes. The "type text" attribute means that it will be a textbox. Then we have an ID which is used to target this specific element in JavaScript or other programming language. And the "name" attribute which will be submitted to the database along with the value that is put into the textbox. So if I type in "Coder", then if we submitted the form, our entry would contain "Name equals Coder".

The "required" attribute means that the form will not submit if this field is left empty. Then the min and max length attributes are optional, but they let you control character length, and the size is the visual size of the textbox.

If we scroll down a bit more, we can see that there are different "types" that you can set the input to be other than "text". We have button, checkbox, color picker, date picker, and email-- which we will be using in our website. The email field will look just like a regular textbox, but has some additional validation and other features more than just text.

Let's get back to our code and start adding our form elements. We're just adding a textbox for the email address, so let's create one by typing "input" and then I'm going to select "email" to set the "type" to "email".

Then in the input element, I'm going to set "name" to "email" and set "id" to "txtEmail", just to follow what we might need to set in a fully functional form. I'm also going to add the "required" attribute since we would want to enforce that. But just to note, in a real form you would also want some server-side form validation to be safest-- you shouldn't only depend on the native HTML validation when it comes to submitting data.

Now, the other thing we need to add for this Email field is a label. This is included in the design, it says "Email address" above the textbox. I know a lot of people don't include a label, and instead just use the placeholder text to put the field name in.

But the original purpose of placeholder text is to give an example of the type of information you can put in the field. So for our email field, I'll add the "placeholder" attribute, and then "[test@test.com](mailto:test@test.com)".

Then when I save you can see that we have the textbox and in it our placeholder text. Putting the name of the field here has a few different problems-- one is that it's by nature a light gray so that you know it's not the actual text. So the contrast is too light to be considered readable.

Also, the placeholder text is not accessible to be read by screen readers. So we shouldn't use placeholder to keep any important information that users need to know. I think it's okay to use placeholders as an extra feature, and as long as users are not dependent on having to read them to know how to fill out the form.

We do need to label our textbox, and the way to do that is to add a label element. So in our code, before the email input, I'm going to add a "label" tag. And VS Code automatically adds the "for" attribute-- this is how you can tell the browser what input element the label is labeling.

In the label, we want to set the "for" attribute to the ID of the corresponding input. So I'm going to copy the "txtEmail" ID and paste it in for the label. Then in the label tag, I'm going to type in what I want to show the user-- I'll write "Email address".

And in our markup, we should also move our "Contact" button inside the form. So I'll do that.

Now, because this button is in a form, we need to change it to be an actual HTML button element, and not just an anchor link. Because you need it to be an actual button in order for it to submit the form data properly. So I'm going to create a button with Emmet, and I'll select the "submit" type, so when we generate it, it has the "type" set to "submit". And let's copy the "Contact" text and paste it in the button.

Now when we save, we have our new button element, and then our original button which is the anchor tag. I do want to mention that you can also create a button with the input element. Let me show you really quick-- before the buttons I'll add "input" and make it a submit button with "colon submit".

The main difference is that input tags are what's called "void" elements, meaning they don't have an opening and closing tag like most other HTML tags-- they just have one tag and then the forward slash before the closing angle bracket indicates that it's self-closing. So for the submit input, you can put the button text in the "value" attribute. So if I write "Contact" for the value, then we can see the button.

I'm still going to use the button element because I think it's more intuitive to use the button tag, and it's a bit easier to style, so I'm going to delete that input. But I just wanted to mention it to you so you know it exists, because you might run into it.
