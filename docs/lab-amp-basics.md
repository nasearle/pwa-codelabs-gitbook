# Lab 1: Creating a simple AMP webpage




## Contents




<a href="#overview"><strong>Overview</strong></a> 

<a href="#get-set-up"><strong>1.  Get set up</strong></a> 

<a href="#start-a-local-server"><strong>2. Start a local server</strong></a> 

<a href="#write-an-html-page"><strong>3. Write an HTML page</strong></a> 

<a href="#style-the-page-with-css"><strong>4. Style the page with CSS</strong></a> 

<a href="#install-the-amp-library"><strong>5. Install the AMP library</strong></a> 

<a href="#install-the-amp-validator-chrome-extension"><strong>6. Install the AMP Validator Chrome extension</strong></a> 

<a href="#resolve-validation-errors"><strong>7. Resolve validation errors</strong></a> 

<a href="#congratulations"><strong>Congratulations!</strong></a>

<a id="overview" />


## Overview




#### What you'll learn

* Basic HTML and CSS review
* How to create a simple AMP page
* AMP restrictions and requirements
* How to validate an AMP page

#### What you need

* Computer with terminal/shell access
* Internet connection
* Chrome
* A text editor

In a mobile-first world, speed is really important. Websites must be fast to effectively reach and engage users. Users confirm this every day by not engaging with and even giving up on slow sites: 53% of mobile site visitors leave after 3 seconds of load time. This has become a real problem with the growth of average websites from 900KB in the early life of the web to over 3MB today, resulting in 75% of websites taking longer than 3 seconds to load on a 3G connection. In addition to being slow and unresponsive, websites often use obtrusive ads that block you from engaging with the site's actual content. The combination of slow load times and disruptive advertisements creates a bad experience that most users will leave behind.

We want to overcome these problems, but creating a fast, functional, and beautiful mobile site often takes a lot of effort and constant updates. That's why the AMP project was first started. AMP is meant to help developers create fast web experiences that are straightforward to create and to manage. By using the AMP format, your pages will be fast, and will avoid many of the big user experience pitfalls.

<a id="get-set-up" />


## 1.  Get set up




Follow the instructions provided by the session instructor to access the code repository for this lab. The repo should be available to you on a USB drive.

Open the <strong>amp-ilt/project</strong> folder in your preferred text editor. The <strong>project</strong> folder is where you will be building the lab.

<a id="start-a-local-server" />


## 2. Start a local server




We are going to build a website in this lab. We need to host the site on a local development server in order to test the code we write. If you already know how to run a local server, you can use your preferred method. Your instructor may also guide you to use an online test environment instead. Otherwise, you can use the Web Server for Chrome.

#### Web Server for Chrome

Install the <a href="https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en">Web Server for Chrome browser extension</a> from the Chrome Web Store. After installing the server, launch the app by clicking <strong>Launch App</strong> from the Web Store, or by navigating to <strong>chrome://apps/</strong> in your browser and clicking on the <strong>Web Server</strong> item. In the Web Server app interface, click <strong>Choose Folder</strong> and select the <strong>amp-ilt/project</strong> directory. Set the port to 8081 and make sure the "Automatically show index.html" option is checked. (If the server is already running, you must switch it off and then on again to pick up the changes.)
 <img class="center " style="max-width: 622.00px" src="/images/lab-1-creating-a-simple-amp-webpage/chrome_web_server.png" alt=" Chrome web server" title=" Chrome web server">

After you start a local server, open Chrome and navigate to <a href="http://localhost:8081/index.html">http://localhost:8081/index.html</a>. There should be an "entry not found" error on the page. This is because the <code>index.html</code> page doesn't exist yet. We'll create it in the next step.

<a id="write-an-html-page" />


## 3. Write an HTML page




<a href="https://html.spec.whatwg.org/multipage/">HyperText Markup Language</a> (HTML) is a document description language that lets us create content for the web. Let's make an HTML page now.

Inside the <strong>project</strong> folder, create a file called <code>index.html</code>.

Let's add some HTML code to the file. Copy and paste the following into <code>index.html</code>:

#### index.html
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Chico's Cheese Bicycles</title>
    <link rel="shortcut icon" href="icons/cheese-favicon.png">

  </head>
  <body>

  </body>
</html>
```
Save the file. Now, if you return to the browser and refresh the page, you should see a blank page instead of the error message. This is an improvement, but we'd like our page to actually show something to the user. Let's add some content to the page.

Add the following code to <code>index.html</code> between the opening <code>&#x3C;body></code> and closing <code>&#x3C;/body></code> tags:

#### index.html
```
    <header>
      <div class="site-name">Chico's Cheese Bicycles
</div>

    </header>
    <p>We sell the only ten-speed bicycles in the world made entirely of cheese.  They get you where you need to go, and you never arrive hungry.  Our bikes are 100% biodegradable.  And with our new rodent-repelling varnish they last longer than ever!</p>
```
Save the file and refresh the page in Chrome. Now the page has some content! This is great so far, but we could make the content look a bit nicer. We'll style the page with CSS in the next step.

#### Explanation

HTML is a language that describes what's on a webpage. HTML consists of a series of elements whose names start and end with angle-brackets, like <code>&#x3C;div></code>.  Such a name is called a  <em>tag</em> .  In most cases, each element consists of a start tag, like <code>&#x3C;div></code>, some other stuff, and an end tag like <code>&#x3C;/div></code>.

Inside a tag, there can be any amount of text and/or other tags.  So HTML describes a  <em>hierarchy</em>  of tags, sometimes thought of as a tree.  Inner tags are called "children" of the outer tags, and outer tags are called "parents" of their "children".

For example, here's a possible <code>&#x3C;div></code> tag:
```
<div>Chico's Cheese Bicycles
</div>

```
But here's an example in which the <code>&#x3C;div></code> has a <code>&#x3C;p></code> child tag:
```
<div>
  <p> Some other stuff </p>
</div>

```
If a tag contains no text or children, it can simply end with <code>/></code>.  The <code>&#x3C;img></code> tag is a good example:
```
 <img src="balloons.jpg" />
```
You can learn more about HTML from plenty of fine resources out there on the web.

<a id="style-the-page-with-css" />


## 4. Style the page with CSS




Cascading Style Sheets (CSS) let you customize the look of your webpage. Let's use CSS to style our <code>index.html</code> page now.

Copy and paste the following <code>&#x3C;style></code> element into the bottom of the <code>&#x3C;head></code> element in <code>index.html</code>:

#### index.html
```
<style>
  body {
    font-family: sans-serif;
    margin: 0;
    padding: 0;
    width: auto;
  }
  header {
    background: #e9924e;
    color: white;
    font-size: 2em;
    padding: 10px;
    text-align: center;
  }
  h1 {
    background: white;
    margin: 0;
    padding: 0.5em;
  }
  p {
    margin: 0.5em;
    padding: 0.5em;
  }
  .site-name {
    padding-top: 5px;
    padding-bottom: 5px;
  }
</style>
```
Save the file and refresh the page in the browser. The page should now contain a title bar!

#### Explanation

CSS is a set of rules that control how elements on a webpage look.  Each rule consists of a  <em>selector</em>  and a list of  <em>properties</em> .  The selector determines which elements on your page the rule applies to, and the properties define how that element will look.

Take this rule above:
```
.site-name {
    padding-top: 5px;
    padding-bottom: 5px;
}
```
The selector starts with a period.  This is how you select all the elements with a given  <em>class</em> .  This rule would apply to any element which contained <code>class="site-name"</code> - like <code>&#x3C;div class="site-name"></code>.

The properties above give any such element a top and bottom padding of 5 pixels - which instructors the browser to leave 5 pixels of blank space above and below the element.

As with HTML, the web is full of lots of excellent documentation and tutorials about CSS.  One such resource is the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS">CSS documentation on MDN</a>.

<a id="install-the-amp-library" />


## 5. Install the AMP library




AMP is a strong move in favor of a faster, more user-friendly web. Modern web pages often load much too slowly, especially on mobile, and components like ads can be disruptive to the user experience if done incorrectly.

AMP runs on standard HTML, JS, and CSS. It's simply a specific use of standard web technologies, and it works in all modern browsers.

AMP has a set of requirements to ensure that AMP pages load quickly, and features like ads run smoothly. For example, AMP does not allow any custom JavaScript; you can only write your own JavaScript in very limited contexts. However, the AMP library is JavaScript that provides all the logic that most sites need. AMP also restricts a small number of HTML tags and CSS rules from use (we'll explore these in the next section).

For an HTML page to be an AMP page, it must include the AMP library. This library implements all of AMP's best performance practices and manages resource loading to ensure a fast rendering of your page. It also contains a validator that tests if your page meets the requirements of AMP.

Let's convert our HTML page to an AMP. To begin, we will add the AMP JavaScript library file and view what errors appear when the AMP validator is turned on.

To include the AMP library, add this line just before the closing <code>&#x3C;/head></code> tag in <code>index.html</code>:

#### index.html
```
<script async src="https://cdn.ampproject.org/v0.js"></script>
```
Save the file and refresh the page in the browser. Open Chrome DevTools (<code>Command+Option+I</code> on Mac or <code>Control+Shift+I</code> on Windows) and select the <strong>Console</strong> tab. You should see this message in the console:
```
Powered by AMP ⚡ HTML
```
<strong>Optional:</strong> While AMP can be used on desktop as well as mobile, it is a good idea to simulate a mobile device experience in the Chrome Developer Tools to see how a user would experience your site on mobile. Click the mobile phone device icon here:
 <img class="center " style="max-width: 409.00px" src="/images/lab-1-creating-a-simple-amp-webpage/devtools_mobile_preview.png" alt=" Mobile preview in DevTools" title=" Mobile preview in DevTools">

Now select a mobile device (for example a "Nexus 5X") from this menu:
 <img class="center " style="max-width: 624.00px" src="/images/lab-1-creating-a-simple-amp-webpage/select_device.png" alt=" Select mobile device" title=" Select mobile device">

You should see a mobile simulated resolution in your browser such as this:
 <img class="center " style="max-width: 388.50px" src="/images/lab-1-creating-a-simple-amp-webpage/first_app_preview.png" alt=" First app preview" title=" First app preview">

<a id="install-the-amp-validator-chrome-extension" />


## 6. Install the AMP Validator Chrome extension




Each AMP page starts with a <a href="https://www.ampproject.org/docs/tutorials/create/basic_markup">standard bit of HTML</a>. This <a href="https://www.ampproject.org/docs/tutorials/create/basic_markup#required-mark-up">required markup</a> is sometimes called the "AMP Boilerplate".

The AMP HTML document must:
<table>
<tr>
<td><strong>Rule</strong>
</td>
<td><strong>Description</strong>
</td>
</tr>
<tr>
<td>Start with the <code><!DOCTYPE html></code> doctype.
</td>
<td>Standard for HTML.
</td>
</tr>
<tr>
<td>Contain a top-level <code>&#x3C;html �</code>�> tag (<code><html amp></code> is accepted as well).
</td>
<td>Identifies the page as AMP content.
</td>
</tr>
<tr>
<td>Contain <code>&#x3C;head></code> and <code><body></code> tags.
</td>
<td>Optional in HTML but not in AMP.
</td>
</tr>
<tr>
<td>Contain a <code>&#x3C;meta charset="utf-8"></code> tag as the first child of the <code><head></code> tag.
</td>
<td>Identifies the encoding for the page.
</td>
</tr>
<tr>
<td>Contain a <code>&#x3C;script async src="https://cdn.ampproject.org/v0.js">&#x3C;/script></code> tag as the second child of the <code><head></code> tag.
</td>
<td>Includes and loads the AMP JS library.
</td>
</tr>
<tr>
<td>Contain a <code>&#x3C;link rel="canonical" href="$SOME_URL"></code> tag inside the <code><head></code>.
</td>
<td>Points to the regular HTML version of the AMP HTML document or to itself if no such HTML version exists. Learn more in <a href="https://www.ampproject.org/docs/guides/discovery">Make Your Page Discoverable</a>.
</td>
</tr>
<tr>
<td>Contain a <code>&#x3C;meta name="viewport" content="width=device-width,minimum-scale=1"></code> tag inside the <code>&#x3C;head></code> tag. It's also recommended to include <code>initial-scale=1</code> in the content attribute.
</td>
<td>Specifies a responsive viewport. Learn more in <a href="https://www.ampproject.org/docs/guides/responsive/responsive_design">Create Responsive AMP Pages</a>.
</td>
</tr>
<tr>
<td>Contain the <a href="https://www.ampproject.org/docs/reference/spec/amp-boilerplate"><code>amp-boilerplate</code> code</a> in their <code><head></code> tag.
</td>
<td>CSS boilerplate to initially hide the content until AMP JS is loaded.
</td>
</tr>
</table>

Our current page is missing some of the required markup, but not to worry! We have a tool, called the AMP validator, that tests our page and tells us exactly what we need to change to make our page a valid AMP. We will make these changes in the next step and gain some insight into the way AMP works as we do. 

For future projects, you can use the <a href="https://www.ampproject.org/docs/tutorials/create/basic_markup">AMP Boilerplate</a> as a starting point for your site. The boilerplate code contains all of the markup required for validation.

Now, let's install the AMP validator and see what happens. 

Install the <a href="https://chrome.google.com/webstore/detail/amp-validator/nmoffdblmcmgeicmolmhobpoocbbmknc?hl=en">AMP Validator Chrome extension</a>.

Once installed, the extension should appear as a little AMP symbol in the navigation bar:
 <img class="center " style="max-width: 624.00px" src="/images/lab-1-creating-a-simple-amp-webpage/amp_validator_extension.png" alt=" AMP Validator extension" title=" AMP Validator extension">

One of the requirements for a page to be considered valid AMP is for the <code>&#x3C;html></code> tag to contain a <code>�</code>�� symbol or the word <code>amp</code>. After this requirement has been met, the AMP Validator Chrome extension will give us a detailed list of the rest of the validation errors in our page.

Add the ⚡ attribute to the <code>&#x3C;html></code> tag like so:

#### index.html
```
<html ⚡ lang="en">
```
Save the file and reload the page.

The AMP symbol should turn red and display a number corresponding to the number of errors in our page.

Click on the icon to see the list of validation errors.
 <img class="center " style="max-width: 624.00px" src="/images/lab-1-creating-a-simple-amp-webpage/amp_validator_errors.png" alt=" AMP Validator errors" title=" AMP Validator errors">

<div class="note">
<strong>Note:</strong> You can also enable the built-in AMP validator by adding <code>#development=1</code> to the end of the AMP URL in the browser. For example, <code>http://localhost:8081/index.html#development=1</code>. Validation errors will appear in red in the console. You may need to manually refresh the page in your browser to see the errors.
</div>

Now we're ready to turn this into a proper AMP page! Let's step through the validation errors one by one and address how they relate to AMP.

<a id="resolve-validation-errors" />


## 7. Resolve validation errors




For your AMP page to be hosted in an <a href="https://www.ampproject.org/docs/guides/how_cached">AMP Cache</a>, it must pass validation. 

An AMP Cache is a <a href="https://en.wikipedia.org/wiki/Content_delivery_network">content delivery network</a> (CDN) for delivering valid AMP documents. When serving AMP documents, the AMP Cache picks the server closest to the user, so that the page is delivered very quickly. Additionally, valid AMP pages in Google Search results get precached and prerendered. That way, when the user clicks on a result, the page appears in less than a second.

Web crawlers are constantly searching the web for valid AMP pages, and when they're found the content gets saved in an AMP Cache. So all you must do to get your page into an AMP Cache is make it valid AMP. 

<div class="note">
<strong>Note:</strong> If you don't want your page served by AMP caches, you can simply insert something small that makes the AMP invalid.
</div>

All of the <a href="https://www.ampproject.org/docs/tutorials/create/basic_markup#required-mark-up">required markup</a> validation errors can be easily fixed by adding a few lines of <a href="https://www.ampproject.org/docs/tutorials/create/basic_markup">AMP boilerplate</a> code to the <code>&#x3C;head></code> of your document. Let's look at the validation errors one by one and add the corresponding piece of the AMP boilerplate to fix them.

### Charset required

We will begin by fixing the following error:
```
The mandatory tag 'meta charset=utf-8' is missing or incorrect.
```
AMP requires that the charset for the page be set so that the text displays correctly. It also must be the first child of the <code>&#x3C;head></code> tag.

Add the following code to <code>index.html</code> as <strong>the first line of the </strong><code>&#x3C;head></code><strong> tag</strong>:

#### index.html
```
<meta charset="utf-8" />
```
Save the file, reload the page, and check the validator to see the error is not showing anymore.

### AMP pages are required to have a <code>&#x3C;link rel=canonical></code> tag.​​​

Next, we will look at the following error:
```
The mandatory tag 'link rel=canonical' is missing or incorrect.
```
When AMP began, it was standard practice to use it only on mobile. A webpage would have an AMP version that was served to mobile devices, and a version written in regular HTML for desktops. It was required to link the two versions together using a <code>&#x3C;link></code> tag so that search engines would know that both docs represented the same webpage. The non-AMP version was called the "canonical" version.

So, the non-AMP document contained a link to the AMP document, like this:
```
<link rel="amphtml" href="https://www.site.com/amp/document.html">
```
And the AMP document contained a link to the non-AMP document, like this:
```
<link rel="canonical" href="https://www.site.com/document.html">
```
Now, AMP has become more full-featured, and unless you require additional features on your desktop page, it may be easiest to simply use AMP for both mobile and desktop. That way, you're maintaining one page instead of two! Nonetheless, the <code>&#x3C;link></code> is still required. In this case, you simply link the page to itself, like this:
```
<link rel="canonical" href="https://www.site.com/amp/document.html">
```
Using a single AMP page for all devices is called "canonical AMP". That's what we're doing for our cheese bike shop!

Let's add this canonical link to our AMP page.

Add the following code to <code>index.html</code> below the <code>&#x3C;title></code> tag in the <code>&#x3C;head></code>:

#### index.html
```
<link rel="canonical" href="/index.html">
```
Return to the browser and reload the page. The canonical link error is no longer in the validator.

### Viewport required

Next we will tackle the following error:
```
The mandatory tag 'meta name=viewport' is missing or incorrect.
```
To fix this error, add the following HTML snippet under the <code>&#x3C;link rel="canonical" href="/index.html"></code> tag in the <code>&#x3C;head></code>:

#### index.html
```
<meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
```
The <a href="https://developers.google.com/speed/docs/insights/ConfigureViewport?hl=en">meta viewport tag</a> configures how your page will appear on mobile devices. 

As before, reload the page and check if the error has disappeared.

### The style element

The following warning is related to the <code>&#x3C;style></code> tag:
```
The mandatory text (CDATA) inside tag 'head > style[amp-boilerplate] - old variant' is missing or incorrect.
```
The <code>&#x3C;style></code> element containing your custom styles must have the <code>amp-custom</code> attribute.

Add the <code>amp-custom</code> attribute to the opening <code>&#x3C;style></code> tag:

#### index.html
```
<style amp-custom>
```
Note that there is a 50 kilobyte file-size limit for all styling information, and that you can only have one <code>&#x3C;style amp-custom></code> tag in your entire AMP document. You can read more about AMP CSS rules <a href="https://www.ampproject.org/docs/guides/responsive/style_pages">here</a>.

Once again, reload the page and check if the stylesheets warning has disappeared.

### The AMP CSS boilerplate

The next errors refer to two missing tags in the <code>&#x3C;head></code> tag:
```
The mandatory tag 'noscript enclosure for boilerplate' is missing or incorrect.
The mandatory tag 'head > style[amp-boilerplate]' is missing or incorrect.
The mandatory tag 'noscript > style[amp-boilerplate]' is missing or incorrect.
```
Add the following code to the <code>&#x3C;head></code>, just above the <code>&#x3C;style amp-custom></code> element: 

#### index.html
```
<style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
```
This is some CSS boilerplate to initially hide the content until AMP JS is loaded.

### Success!

Now your AMP document should look something like this:

#### index.html
```
<!doctype html>
<html ⚡ lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="canonical" href="/index.html">
    <title>Chico's Cheese Bicycles</title>
    <link rel="shortcut icon" href="icons/cheese-favicon.png">
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
    <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
    <style amp-custom>
      body {
        font-family: sans-serif;
        margin: 0;
        padding: 0;
        width: auto;
      }
      header {
        background: #e9924e;
        color: white;
        font-size: 2em;
        padding: 10px;
        text-align: center;
      }
      h1 {
        background: white;
        margin: 0;
        padding: 0.5em;
      }
      p {
        margin: 0.5em;
        padding: 0.5em;
      }
      .site-name {
        padding-top: 5px;
        padding-bottom: 5px;
      }
    </style>
    <script async src="https://cdn.ampproject.org/v0.js"></script>
  </head>
  <body>
    <header>
      <div class="site-name">Chico's Cheese Bicycles
</div>

    </header>
    <p>We sell the only ten-speed bicycles in the world made entirely of cheese.  They get you where you need to go, and you never arrive hungry.  Our bikes are 100% biodegradable.  And with our new rodent-repelling varnish they last longer than ever!</p>
  </body>
</html>
```
Refresh the page and check the validator. The symbol should appear green indicating that all validation checks have passed!

<a id="congratulations" />


## Congratulations!




You've started your AMP journey and successfully created your first valid AMP. 

<strong>Frequently Asked Questions</strong>

* <a href="http://stackoverflow.com/a/27637245">What is DOM reflow?</a>
* <a href="https://www.ampproject.org/docs/guides/responsive/control_layout.html#what-if-the-layout-attribute-isnt-defined">What if the layout attribute isn't defined?</a>
* <a href="https://www.ampproject.org/docs/guides/responsive/control_layout.html#what-if-width-and-height-are-undefined">What if width and height are undefined?</a>


