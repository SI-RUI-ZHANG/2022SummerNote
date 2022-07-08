---
created: 09-03-2022
e: ⭐
tags: CS/javascript
---

# HTML Basics

HTML is a "markup language" that is used to describe to a client (web browser) what a web page should look like. HTML is considered an "interpreted" language - it needs an interpreter (your browser) to decode it and draw its contents to the screen.

Here's the basic structure of a HTML page.

And here's an overview of what all this means:

- HTML is a "tag based" language - tags are defined using open tags such as `<html>` and closing tags `</html>`.
- Tags are not printed - they are instead interpreted by the browser
- HTML ignores whitespace (you can hit enter a million times and you won't get a million line breaks on your website)
- The 'doctype' on the first line communicates to the browser that this document should be interpreted as a HTML5 document. This essentially tells the browser what "version" of HTML to expect in this document. This is the doctype for HTML5, the latest version of HTML.
- The opening 'html' tag signifies that everything from this point forward (until we reach the closing 'html' tag) should be treated as HTML. It also announces to the browser that the text being written on this page should be interpreted as US English. This is important for a number of reasons, none the least of which includes providing support for people with visual disabilities on your page (special software can be used to read a page using a computerized voice and the language declaration helps to make this process a lot easier)
- The opening 'head' tag signifies that we are in the document header. Anything that goes inside of the opening and closing 'head' tags is not supposed to be visually displayed as part of the web page -- instead this information is used by the browser (or search engines) get learn more about the page and how it should be used.
- The 'title' tag defines the title for the tab that this web page will open in your browser. Note how the text 'My Awesome Webpage' is situated between the two 'title' tags. We would say that this text is "affected" by these tags.
- The 'meta' tag is used to announce to the browser what character set we will be using on this page (standard ASCII vs. other characters sets)
- The 'body' tag indicates that we are working on the main body of the web page. Anything inside of the 'body' tags will be rendered visually as part of your website.
- The 'p' tag is a paragraph tag - it defines a new paragraph block. Paragraph blocks always have a line break after them.

## Heading Tags

HTML contains a series of heading tags which can be used to highlight important items on your website. Heading elements are organized into six levels – 'h1' through 'h6'. 'h1' is the largest heading, and 'h6' is the smallest. Each has its own corresponding tags which surround text that should be considered part of the heading. For example:

```html
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
<h3>This is heading 3</h3>
<h4>This is heading 4</h4>
<h5>This is heading 5</h5>
<h6>This is heading 6</h6>
```

## Block Level Elements

Heading elements are considered “block level” elements. This means that they will automatically occupy their own “line” on your HTML document – the browser will place a line break before and after your heading tags.

Another block level tag is the paragraph tag (`<p>`). This tag can be used to render text that should be structured as a single paragraph, like this:

```html
<p>It was the best of times, it was the worst of times ... </p>
```

You can also force a line break using the `<br>` tag. Note that in the previous version of HTML (XHTML) this was considered a “self contained” tag, so you will often see it used like this on the web: `<br />`. The  
tag is a block level tag as well. The browser will place it on its own line.

## Block Level vs. Inline Elements

As you can see, many elements in HTML are block-level elements (i.e. they will force a linebreak before and after the element). Some other elements are considered “inline” – they won’t force a linebreak by default. These elements affect the text they surround, like this:

```html
<p>
   <strong>This text is bold</strong> and 
   <em>This text is italicized</em>
</p>
```

We sometimes refer to these as "phrase" elements or "inline" elements. Here are a few examples:

- The 'strong' tag can be used to draw emphasis to some text (renders it in bold, and reads it in a loud voice to people with visual disabilities)
- The 'em' tag can also be used to draw emphasis to some text (renders it in italics)
- The 'sub' and 'sup' tags can be used to render subscript and superscript text (i.e. H2O or x2)
- The 'abbr' tag can be used to generate an abbreviation. For example:

```html
    <abbr title="Courant Institute">CIMS</abbr>
```

## Hyperlinks

The hyperlink is the primary navigation tool used to connect pages together in HTML. Hyperlinks (or "links") contain the following properties:

- A **resource** that is being linked to. This could be another web page, a PDF document, an image etc.
- An **anchor** that will serve as the visual representation for the link. This could be some text (i.e. [click here!](https://cs.nyu.edu/courses/spring22/CSCI-UA.0061-001/wrapup_01_static_web_development.php#)), an image, etc.
- An optional **target** that will tell the browser where to open the link. The default location to open a link is in the same tab (forcing the user to hit the "back" button if they want to return to the previous page) - you can also ask the browser to open the link in a different tab to override this behavior.
The basic structure of a link in HTML is as follows:

```html
<a href="resource">anchor text or image</a>
```

For example, if you wanted to create a link to the NYU homepage you could do so using the following code:

```html
<a href="http://www.nyu.edu">click here to go to NYU</a>
```

Note that the 'http://' part of the URL (called the "protocol") is required for links that are outside of your own website. We call these "absolute" links since they are directly pointing to a resource out of your control.

If you wanted to link to another one of your own pages you could use a "relative" hyperlink which does not require the 'http://' protocol. For example, say you had a page called 'pokemon.html' - you could link to it using the following:

```html
<a href="pokemon.html">click here for pokemon!</a>
```

To cause a hyperlink to open in a new tab you can use the optional "target" property, like this:

```html
<a href="pokemon.html" target="_blank">Pokemon in a new window!</a>
```

The "target" property tells the browser where the link should open. "_blank" is a special command that tells the browser to create a new tab and open the link there.

## Lists

List tags (`<ol> <ul>`) are used to define bulleted and ordered lists. The require both a beginning and an ending tag. The list item tag (`<li>`) is used inside of a list tag to render a line item in your list. This tag requires both an opening and a closing tag. Here’s an example:

```html
<ul>
 <li>First item</li>
 <li>Second item</li>
</ul>
```

Lists can also be "nested", meaning that you can have one inside of the other. Here’s an example:

```html
<ul>
 <li>First item
  <ol>
   <li>Sub-item 1</li>
   <li>Sub-item 2</li>
  </ol>
 </li>
 <li>Second item</li>
</ul>
```

## Tables

Tables can be created using the `<table>` tag. Once created, you can add in rows using the `<tr>` tag and individual “cells” using the `<td>` tag. For example:

```html
<table>
 <tr>
  <td>Student</td>
  <td>Grade</td>
 </tr>
 <tr>
  <td>John</td>
  <td>75</td>
 </tr>
</table>
```

Tables used to the primary way in which we visually laid out content for a web page, but this technique has fallen out of favor. Instead, web developers should be using CSS to lay out the content - we will discuss this more next week when we begin the CSS portion of the class.

## Images in HTML

Images can be incorporated onto a web page using the img tag. Here's the syntax:

```html
<img src="filename.jpg" />
```

Note that images are not "embedded" into an HTML document - instead, they are referenced as external assets that are loaded in by the browser when the page is displayed. This means that you will need to upload a copy of your image onto the i6 server in order for the image to display (otherwise you will see a "broken image" icon)

Note that you can put any hyperlink reference into the 'src' attribute to reference either a local file (relative hyperlink) or remote file (absolute hyperlink). It's generally considered bad practice to link to someone else's image on their own server though.

When the img tag is encountered the browser makes an independent network call for each image that you have on a page - the more images you have on a page, the more network calls, and the slower the page will generally load.

The browser only can support 4 file formats reliably - JPG, GIF, PNG and SVG (vector)

You can adjust the width and height of an image in HTML using the width and height properties, like this:

```html
<img src="filename.jpg" **width="500" height="200"**>
```

And if you omit one of these values the browser will automatically scale the image on your behalf. For example, if you wanted an image to occupy a width of 300 pixels you could use the following code - the browser will figure out how tall to make the image while keeping its scale in proportion:

```html
<img src="filename.jpg" **width="300"** />
```

Note that it is also possible to adjust the width of an image using CSS.

## HTML vs. CSS

HTML is a language that defines the structure of a document. Like a building, HTML defines the core elements of a page, such as the foundation, basement, first story, and roof. In the old days, HTML was also responsible for describing the presentation of content. For example, the following tag used to be used to change the color of text:

```html
<font color="yellow">Pikachu is yellow!</font>
```

However, this practice has Springen out of favor. For one, it's incredibly time consuming to do this - imagine that you are working on a 100 page website and your boss decides to change the heading color on each page from Yellow to Blue. You would have to manually search and replace content on 100 different pages!

Another reason why this technique isn't used anymore is due to the fact that we view web pages on many different types of devices (iPads, phones, browsers, etc) and we often have to adjust the presentation of our content for a particular screen width / height / orientation -- but not the content itself. CSS gives us this flexibility - it allows us the ability to completely separate the content of a page from its design.

So what is CSS? CSS stands for "Cascading Style Sheets" - it is a descriptive language that is used by a browser to "style" structural elements. For example, you could have the following HTML document:

```html
<h1>Welcome to my site!</h1>
```

And the browser will render it using in a default format. However, we can use CSS to tell the browser that the H1 tag should be styled in a different way using a series of "rules". The rest of today's lecture will focus on the mechanics of writing these rules as well as where these rules can be placed in your document.

## Style Placement

There are three ways in which you can attach styles to your documents:

- In-line styles
- Embedded in the `head` portion of your HTML document
- Loaded via an external style (called a stylesheet)

## In-line Styles

Let's start with exploring in-line styles. These styles are placed directly into an HTML tag, like in the following tag:

```html
<h1 style="color: yellow;">My h1 tag</h1>
```

This says "this h1 tag should be rendered using a yellow color".
In terms of color there are two CSS "rules" that we often use:

- `color` - foreground (text) color
- `background-color` - background color that will go behind all foreground content (text images, etc)
We can apply these rules to individual tags by using the "style" property, like this:

```html
<tag style="property: value;">
```

... and we can apply both style to a tag by including both rules inside of the "style" attribute. Note that the styles are separated by the ";" character.

```html
<tag style="property1: value1; property2: value2;">
```

## Embedded Styles

Styling an individual tag in this way is useful, but it's not practical to build an entire site this way as it can be difficult to read a document that has been created this way. Also the style is tightly coupled with the page content. This can cause problems later on when we need to change the style based on a variety of factors, such as a different screen resolution or device. In addition, if we wanted to apply a "blanket" style to all elements (say, all `p` tags should use the same foreground and background colors) we would have to duplicate a lot of code.

We can begin to address these issues by using "embedded" styles that we can place into the head of our HTML documents. Embedded styles are placed in the HEAD of the HTML document and inside a special tag called the "style" tag, like this:

```html
<head>
 <style type="text/css">
 </style>
</head>
```

Inside of the `style` tag we can then outline our "selectors". Selectors are the items on our page that we want to style. After we define a selector we place two brace characters ("{" and "}") to indicate that anything in between these braces is associated with the selector. Inside of these braces we then can articulate all of the "rules" that should be applied to the selector. Here's the syntax:

```html
<head>
 <style type="text/css">

  selector {
   property: value;
  }
 
 
 </style>
</head>
```

For example ....

```html
<head>
 <style type="text/css">
  /* this will make all h1 tags show up in blue text */
  h1 {
   color: blue;
  }
 </style>
</head>
```

Note that in CSS a "comment" can be applied using the "/*" character sequence followed by the "*/" character sequence. Anything in between these two "bookends" is ignored by the browser. This only works in CSS though - for HTML you have to use the standard HTML commenting method described during our HTML lectures.

## External Stylesheets

In our example above our styles are only applied to the current HTML document. This means that if we have two pages that we want to style in the same way we will have to "copy and paste" the styles to the desired page. We can do better than this!

Rather than storing styles on a particular page we can create a single external file called "styles.css" which will hold all of our styles. Here's what we can put inside of this document:

```css
/* my styles */
body {
  background-color: yellow; 
}
```

And then we can link it from our HTML pages, like this:

```html
<head>
  <link rel="stylesheet" type="text/css" href="styles.css" />
</head>
```

You can also override a style declaration on a specific page by putting a style in the head of that document. In this case the specificity of the style will override the style in the stylesheet.

## Conflicting Styles

Note that you can freely use all three CSS placement techniques on the same page. This can result in "style conflicts" -- for example, what do you think would happen in the following code?

```html
<html>
<head>
 <style type="text/css">

  h1 {
   background-color: grey;
   color: blue;
  }
 
 
 </style>
</head>
<body>
 <h1 style="color: green;">Welcome!</h1>
 <h1>What color is this h1?</h1>
</body>
```

In this case we have a conflicting style - the embedded style says to make all h1 tags blue, but the in-line style tag says to make this particular h1 tag green. To resolve the conflict the browser will use the style that is the most specific to the tag being affected (in this case green, which is the in-line style). Also note that the "background-color" property was also attached to the h1 selector. This property does not conflict with any properties attached to the two h1 tags on the page, so it is applied to both of the h1 tags as-is.

## IDs, classes and contextual selectors

Often you don't want to style all elements of the same type on a page. We can get around this by changing the selector that we use in CSS to target that element. Remember that the "selector" is the part of the CSS rule that defines the elements(s) on the page that will receive that rule. For example, the `h1` tag is the selector in the following CSS statement:

```css
h1 { 
  font-family: "Arial"; 
}
```

If you only want to target ONE element on the page you can give that element an "id". IDs can only affect one element, and there can only be one tag on the page with that ID. Here's an example:

```html
<h1 id="pikachu">Pika Pika!</h1>
```

Now we can write a CSS rule to target the id "pikachu", like this:

```css
#pikachu { 
  background-color: yellow; 
}
```

Sometimes you need to apply the same style to multiple elements. In that case you can create a "class" - any number of elements on a page can belong to the same class. Here's an example in HTML:

```html
<p class="charmander">This is paragraph 1</p>
<p>This is paragraph 2</p>
<p class="charmander">This is paragraph 3</p>
```

... and here's how to write a selector for the "charmander" class in CSS:

```css
.charmander { 
  background-color: red; 
}
```

Note that elements can have both IDs and classes. The following statement is valid in CSS:

```html
<p id="pikachu" class="charmander">What will show up here?</p>
```

Note that when a conflict between rules arises, IDs will win over classes. This is because IDs are more "specific" (they can only affect one element on the page)

A 'contextual selector' allows us to target tags on our page based on the relationship of a tag to its 'parent'. There are two may types of contextual selectors that we will be working with.

First, let's consider the following code:

```html
<div id="#example1">
    <p>paragraph 1</p>
    <div>
        <p>paragraph 2</p>
    </div>
    <p>paragraph 3</p>
</div>
```

If you wanted to style all of the "p" tags that are of the "foo" element (i.e. paragraphs 1, 2 3) you could write a rule that looks like the following:

```css
#example1 p {
 background-color: red;
 color: white;
}
```

However, if you only wanted to target the two **direct descendents** of the "div" tag you could do something like the following:

```css
#example1 > p {
 background-color: red;
 color: white;
}
```

Note the ">" character being used here - this is saying "find ONLY the 'p' tags that are direct descendants of the #example2 element"

For example, let's say that we want to style all "nested lists" - i.e. lists that appear inside of other lists. Here's the HTML code:

## The Box Model

All block level elements in CSS behave using the "box model" - this model describes how a block level elements should be rendered by the browser and includes the following elements:
![[Screen Shot 2022-03-09 at 9.37.11 PM.png|500]]
All block level elements can be given width and height attributes. if not specified, width will be 100% of the current container and height will adjust based on the content contained inside the container. For example, let's say we want this div to take up 50% of the browser's available width. We can do this by applying the "width" property to the tag, like this:

```html
<div style="width: 50%;">This is a div!</div>
```

... or if we want the tag to only take up 500 pixels of screen space we can do this:

```html
<div style="width: 500px;">This is a div!</div>
```

... and of course we can also apply height to block level tags, like this:

```html
<div style="width: 500px; height="250px;">This is a div!</div>
```

In addition, all block level elements contain a "border"" property as well as a width and height. By default a block level element has no border, but you adjust this using the following rules![[Screen Shot 2022-03-09 at 9.38.56 PM.png|300]]:

Note that you can also style just one border edge using the following rules:

```css
border-bottom: 5px solid black;
border-top: 5px solid black;
border-left: 5px solid black;
border-right: 5px solid black;
```

In addition, all block level elements can also have a property called "margin and padding". Margin is used to add space adds pixels outside the element, and padding adds space between the border of the element and the content within the element.
Margin and padding can be applied globally (i.e. to all 4 sides of your block level element) or to a single side. Here are the valid CSS rules that you can use to manipulate these values:

```css
margin: 100px; /* applies 100px of margin to ALL sides of your element */
margin-left: 10px; /* applies 10px of margin only to the LEFT side of your element */
margin-right: 10px; /* same as above, but applies the margin to the RIGHT of the element */
margin-top: 5px: /* top of the element */
margin-bottom: 5px; /* bottom of the element */

padding: 50px; /* applies 50px of padding to ALL sides of your element */
padding-right: 5px;
padding-left; 5px;
padding-top: 5px;
padding-bottom: 5px;
```

Here are some examples:
![[Screen Shot 2022-03-09 at 9.40.12 PM.png|300]]
You can center a div horizontally by applying margin: auto to the div - this will ask the browser to figure out what the margin should be on the left and right side of the div. Here's an example:
![[Screen Shot 2022-03-09 at 9.47.28 PM.png]]
Note that block level elements can be "nested" inside of one another. For example, here is a div that contains two other divs - notice how we only need to define the width on the "outer" div in this example. The "inner" divs will automatically grow to the correct size since, by default, a block element will extend across an entire line if not given a width value.

```html
<div style="width: 500px; border: 2px solid black;">
    
 <div style="height: 250px; background-color: yellow;">
 </div>
 
 <div style="height: 250px; background-color: red;">
 </div>

</div>
```

Alternately, you could ask the inner divs to have a width of 100%. In CSS a block level element will compute its size relative to its "parent" element. This means that the block level elements inside of the "outer" div will occupy 100% of the available width inside of that div.

```html
<div style="width: 500px; border: 2px solid black;">
    
 <div style="height: 250px; width: 100%; background-color: yellow;">
 </div>
 
 <div style="height: 250px; width: 100%; background-color: red;">
 </div>

</div>
```

Also notice that we can adjust the margin and padding on the "outer" div to control how the inner divs line up:

```html
<div style="width: 500px; border: 2px solid black; padding: 25px; margin: auto;">
    
 <div style="height: 250px; background-color: yellow;">
 </div>
 
 <div style="height: 250px; background-color: red;">
 </div>

</div>
```

![[Screen Shot 2022-03-09 at 9.48.55 PM.png]]

## Pseudoselectors

CSS and HTML are both "languages without verbs". In general, they can't be used to simulate interactivity. With that said, CSS does have some special attributes that let you change the design of the page based on basic user behavior states. For example, one thing that a user will often do is to hover over an element on your page. You can use a special CSS construct called a "pseudoselector" to listen for these events and respond accordingly. For example, consider the following code:

```css
h1 { 
 font-family: "Arial-Black"; 
}
h1:hover { 
    color:#FFCC00; 
}
```

The hover pseudo selector allows you to change the rule affecting an element only when the mouse is actively hovering over the element.

Any HTML element can be given a pseudoselector (div, p, h1, a, etc) but we often use them in conjunction with hyperlinks. There are a few other pseudoselectors in addition to :hover including:

```css
a:link    /* defines the look of the link when it is UNVISITED */
a:visited  /* defines the look of the link after it has been VISITED */
a:focus   /* defines the look of the link when it selected by the KEYBOARD (using the tab key) */
a:hover   /* defines the look of the link when the user is HOVERING over it */
a:active  /* defines the look of the link when the user is CLICKING on it */
```

## Some More on Fonts

In general, fonts are not embedded into an HTML document. They must exist on the user's computer in order for the browser to render them. We can articulate font choices by using a comma separated list, like this:

```css
h1 {
   font-family: "Harry Potter", "Hogwarts", fantasy;
}
```

There are a series of 'failsafe' fonts that you can always refer to:

- serif
- sans-serif
- monospace
- cursive
- fantasy

In addition, you can also use special "web-based fonts" in your site. The easiest way to get started is to use the Google Fonts repository: <http://www.google.com/fonts>#. These fonts are loaded in at the time your page loads from one of Google's servers, which means that the user does not need to have the font installed on their machine in order to see your page using that font.

CSS also allows you to create your own web-based fonts. This process involves having to create a special font file and then uploading that file to your server. Note that this is a "grey area" in terms of copyright, so you should probably stick to using one of the standard fonts on your computer or one of Google's web-based fonts. With that said, here's a link to a site that will walk you through the process: <http://www.fontsquirrel.com/tools/webfont-generator>

The 'float' Property
The float property in CSS lets you position a box without having to manipulate its position property. Boxes that are "floated" are temporarily removed from "normal flow" and move as far to the right or left as possible within their current container.

Note that you can float more than one element on a page. Other elements that are floated after the original element continue the process of floating - if there is room on the that holds the original floated element then subsequent elements will appear next to that element. If not the element will jump down to the next line and float as far left or right as possible. Here's a quick example - try resizing the browser to see how the floats "break" when the browser gets too small:
![[Screen Shot 2022-03-09 at 9.52.04 PM.png]]
The code for the above is as follows:

```css
.floater {
   float: left;
   width: 400px;
   height: 100px;
   border: 1px solid black;
   background-color: #ccc;
}
```html

<div class="floater">This box is floated left</div>
<div class="floater">This box is also floated left</div>

<!-- this line stops the floating and returns us to "normal flow" -->
<br style="clear: both;">
```

Valid values for the `float` property are "left" and "right", which cause the box in question to move as far left or right within their current container as possible. When you are finished floating and want to return to "normal flow" you need to create an element that uses the `clear` property - this property tells the browser to stop any floats that are active and move all future content so that it appears below the last floated element. We generally use `clear: both;` to stop both right and left floats, but you can use `clear: left;` or `clear: right;` too if you wanted to.

## Introduction to CSS Positioning

As you've seen, an HTML document has a normal "flow" to it. For example, block level elements that come after another element in code appear below those elements, and inline level elements appear next to one another.

You can adjust / interrupt the normal flow of a document to create new and interesting layouts for your content. In general, block level elements are positioned using what we call "static" positioning. They will appear where they should appear based on the normal flow. If you want to move a block level element somewhere else on the page you have to give it a specific position type. There are 4 that we use:

- `static`: default - the block appears where it should be. It can't be nudged.
- `relative`: the block appears where it is supposed to be, but nudged out of the way. it's moving relative to its normal flow position. You can nudge it by using the top, left, right, and bottom modifiers. **Relatively positioned elements retain their space on the document.** Things will continue to flow around where the element should have been.
- `fixed`: the block is removed from normal flow and stuck at an exact pixel spot in the browser. Items do not flow around the block.
- `absolute`: the block appears at the position that is specified relative to its nearest parent container. This means that top:0 left:0 for a div that is inside your tag would be the top left side of the screen. Absolute positioned blocks are removed from the normal flow.
In order to position a div we have to use the `position` rule, like this:

```css
position: absolute;
```

Next, we need to define where the div should be placed. We can do that using the `top`, `bottom`, `left` and `right` rules. These tell the browser where that part of the box should appear in relation to its parent container.

```css
position: absolute;
top: 0px;
right: 0px;
```

For a comprehensive demo and overview please view this file (and view its source to see comments on how things work): [02-position_and_document_flow.html](https://cs.nyu.edu/courses/spring22/CSCI-UA.0061-001/sourcecode/static_web_review/positioning_and_document_flow.html)

The z-index property
Boxes that are positioned using relative, absolute or fixed positioning have the ability to overlap one another. You can control how these boxes interact by supplying them with a z-index property - this property tells the boxes how to "stack" (think of it like a "layer" in Photoshop). A z-index value is always an integer, and lower values appear below higher values. For example:![[Screen Shot 2022-03-09 at 9.56.11 PM.png|400]]

## Media Queries

A media query is a way for you to ask the browser to load in a specific set of styles based upon the amount of space available to you in the browser's viewport. Media queries are generally designed to trigger rules stored in different CSS files based on the browser's width.

[This downloadable example (ZIP)](https://cs.nyu.edu/courses/spring22/CSCI-UA.0061-001/sourcecode/static_web_review/media_queries.zip) is designed to use one of three style sheets based on the width of the browser. The example uses three stylesheets named "small.css", "medium.css" and "large.css". These sheets are "conditionally attached" to this document using a media query, which basically asks the browser how big it is and then gives it the rules that are designed for that size. When displaying this page go ahead and resize the browser to see how the styles change based on the available width of the browser window.

Media queries go in the head of the HTML document. The basic syntax for a media query is as follows:

```html
<!-- Media query for narrow browser width -->
<link rel="stylesheet" media="only screen and (max-width: 480px)" href="mobile.css">

<!-- Media query for medium browser width -->
<link rel="stylesheet" media="only screen and (min-width: 481px) and (max-width: 960px)" href="tablet.css">

<!-- Media query for full browser width -->
<link rel="stylesheet" media="only screen and (min-width: 961px)" href="desktop.css">

```

Note that the media queries above will be dynamically evaluated as the browser is resized - as the browser size changes the queries will be re-evaluated and the correct rules will be put in place accordingly.
For mobile devices we need to add in another rule to help make things show up smoothly by preventing the mobile device from scaling the page to fit on the screen when it loads.

```html
<!-- Prevent smartphones from scaling pages down -->
<meta name="viewport" content="initial-scale=1"> 
```

## The "display" property

The display property in CSS allows you to change how an element is treated by the browser. Common values for this property include:

- none: hides the element and removes it from normal flow
- block: displays the element as a block element (line break after the element, obeys the box model - for example, a div and p are block-level tags)
- inline: displays the element as an inline element (no line break after the element, multiple inline elements can be placed in the same horizontal space, does not obey the box model - for example, a a and strong are inline tags)
- inline-block: displays the element as an inline-block element (no line break after the element, multiple inline-block elements can be placed in the same horizontal space, obeys the box model)
You can use the display property to change how any tag behaves in the "normal flow" of the document. For example:

```html
<p style="display: inline;">This is a 'p' tag, but it's on the same line as the hyperlink!</p>
<a href="#">link</a>
<strong style="display: block;">This is a 'strong' tag, but it being rendered as a block tag (line break at the end)</strong>
<a href="#">another link</a>
<div style="display: none">This div is totally invisible!</div>
```

## Flexible Box Module ("flexbox")

The "flexbox" specification is a display property that can be used to arrange elements so that they tile next / on top of one another. Using "flexbox" you can create layouts that were previously only do-able using the float property.

To start, note that "flexbox" layouts work along an orientation axis. The default axis is a horizontal row, though you can change the orientation axis to a column if you want.

To create a "flexbox" layout you need to begin by creating a container that has a display property of flex. You can then add child elements to this container that you want to manipulate. For example:

```html
<style>
 #flex-example-1 {
  display: flex;
 }
 #flex-example1 > div {
  border: 1px solid black;
  background-color: pink;
 }
</style>
<div id="flex-example-1">
 <div>One</div>
 <div>Two</div>
 <div>Three</div>
 <div>Four</div>
</div>
```

OUTPUT:
![[Screen Shot 2022-03-09 at 9.59.50 PM.png]]
Note how the div tags in this example are tiling next to one another from left to right in a row. Each of the child elements are set up so that they are just as wide as they need to be, but their height is equalized across all elements. For example, in the code below the last div is taller than the other elements, but all elements will adjust their height to match the tallest div.:

```html
<style>
 #flex-example-2 {
  display: flex;
 }
 #flex-example-2 > div {
  border: 1px solid black;
  background-color: pink;
 }
</style>
<div id="flex-example-2">
 <div>One</div>
 <div>Two</div>
 <div>Three</div>
 <div>Four<br>Four<br></div>
</div>
```

OUTPUT:
![[Screen Shot 2022-03-09 at 10.00.47 PM.png]]
You can change the default ordering by applying the `flex-direction` property to the container element. Valid values for this property are row (the default), row-reverse, column and `column-reverse`.

You can adjust the size of the elements inside of a "flexbox" layout by using the `flex` property. This property takes up to 3 values, which indicate the "grow" size, "shrink" size and "default" size of the elements. For example:

```html
<style>
 #flex-example-3 {
  display: flex;
 }
 #flex-example-3 > div {
  border: 1px solid black;
  background-color: pink;
  flex: 1 1 auto;
 }
</style>
<div id="flex-example-3">
 <div>One</div>
 <div>Two</div>
 <div>Three</div>
 <div>Four<br>Four<br></div>
</div>
```

![[Screen Shot 2022-03-09 at 10.02.02 PM.png]]

You can cause a "flexbox" layout to break into multiple lines by adjusting the size of each element and applying the flex-wrap property to the container. For example:

```html
<style>
 #flex-example-4 {
  display: flex;
 }
 #flex-example-4 > div {
  border: 1px solid black;
  background-color: pink;
  flex: 1 1 50%;
 }
</style>
<div id="flex-example-4">
 <div>One</div>
 <div>Two</div>
 <div>Three</div>
 <div>Four<br>Four<br></div>
</div>
```
