# Lab 2: Using AMP Components




## Contents




<a href="#overview"><strong>Overview</strong></a> 

<a href="#get-set-up"><strong>1.  Get set up</strong></a> 

<a href="#learn-the-core-amp-components"><strong>2. Learn the core AMP components</strong></a> 

<a href="#expand-content-with-more-components"><strong>3. Expand content with more components</strong></a> 

<a href="#image-carousels"><strong>4. Image Carousels</strong></a> 

<a href="#adding-a-menu"><strong>5. Adding a menu</strong></a> 

<a href="#congratulations"><strong>Congratulations!</strong></a>

<a id="overview" />


## Overview




#### What you'll learn

* How to use AMP components

#### What you should know

* Have completed the <a href="lab-amp-basics.md">Lab 1: Creating a simple AMP webpage</a>

#### What you need

* Computer with terminal/shell access
* Connection to the internet
* Chrome
* A text editor

<a id="get-set-up" />


## 1.  Get set up




Follow the instructions provided by the session instructor to access the code repository for this lab. The repo should be available to you on a USB drive.

Open the <strong>amp-ilt/project</strong> folder in your preferred text editor. The <strong>project</strong> folder is where you will be building the lab.

If you have not completed <a href="lab-amp-basics.md">Lab 1: Creating a simple AMP webpage</a>, you can work inside the <strong>lab-1-solution</strong> folder.

<a id="learn-the-core-amp-components" />


## 2. Learn the core AMP components




AMP is a web components library. A web component is a new HTML tag that includes built-in functionality and perhaps even design. It's a way of extending HTML to do some of the more advanced things required for modern web pages. So, for example, HTML has tags like <code>&#x3C;div></code>, which is used to group page content.  Web components can be tags like <code>&#x3C;amp-youtube></code>, which embeds a YouTube video on your page.

AMP components provide the basic web functionality that shouldn't require writing your own JavaScript. In fact, in AMP, user generated scripts are not allowed except for in specific contexts.

AMP's component system allows us to quickly build efficient and responsive features into our pages with minimal effort. As of this writing, the main AMP JavaScript library (already included in the <code>&#x3C;head></code> of our page) includes three core components:

* <a href="https://www.ampproject.org/docs/reference/amp-img.html">amp-img</a> - A replacement for the HTML img tag
* <a href="https://www.ampproject.org/docs/reference/amp-pixel.html">amp-pixel</a> - Used as a tracking pixel to count page views
* <a href="https://www.ampproject.org/docs/reference/components/amp-layout">amp-layout</a> - Lets you apply aspect-ratio based responsive layouts to any element

For most AMP components, you need to include a JavaScript file that contains the logic for that specific component, but for the two built-in components, you don't. Let's explore the <code>amp-img</code> tag and how it relates to the AMP layout system. See the <a href="https://www.ampproject.org/docs/reference/components">AMP Components reference</a> for the full list of AMP components.

### The amp-img tag

The AMP library, a.k.a. the AMP "runtime", does many things to ensure pages are rendered more efficiently and to create a superior user experience. For example, AMP prevents elements from shifting around as the page loads (an unfortunately common occurrence known as "<a href="https://sites.google.com/site/getsnippet/javascript/dom/repaints-and-reflows-manipulating-the-dom-responsibly">reflow</a>"), which drastically improves page load speed.

To prevent reflow, AMP requires that some HTML tags be replaced with AMP components, and that these elements must declare their size in advance.

AMP has a web component specifically designed to replace the HTML <code>img</code> tag, called <code>amp-img</code>. Let's add an <code>amp-img</code> element to the page without defining the height and see what happens.

Add the following code to <code>index.html</code> under the paragraph inside the <code>&#x3C;body></code> element:

#### index.html
```
<amp-img src="images/ricotta-racer.jpg"></amp-img>
<p>Our newest model: the Ricotta Racer</p>
```
Save the file, return to the browser, and refresh the page. Notice the image does not display on the page.

Click on the validator and you should see one new error:
```
The implied layout 'CONTAINER' is not supported by tag 'amp-img'.
```
Let's explore what this error means before we fix it by defining the height for the element.

### Layout System

AMP includes a <a href="https://ampbyexample.com/advanced/layout_system/">layout system</a> for ensuring the layout of the page is as rigid as possible before the browser renders the page. This system gives us a <a href="https://www.ampproject.org/docs/guides/responsive/control_layout#supported-values-for-the-layout-attribute"><code>layout</code></a> attribute that lets us position and scale elements in a variety of ways -- fixed dimensions, responsive design, fixed height, and more.

The layout system is responsible for enforcing size declarations of certain elements like <code>amp-img</code>. In the layout system, containers (elements that contain other elements) do not need a defined height, because the height of a container is determined by the dimensions of its contents. If an element does not have a defined height, AMP assumes the <code>layout</code> type is <code>container</code> by default. However, the <code>amp-img</code> element can't be a  <code>container</code> (because it cannot contain other elements), so AMP throws the error.

Let's fix the error now.

Set the <code>height</code> and <code>width</code> of the <code>amp-img</code> element as follows. It is recommended to set the width as well as the height so that AMP knows the aspect ratio of the element.

#### index.html
```
<amp-img src="images/ricotta-racer.jpg" width="640" height="480"></amp-img>
```
Refresh the page and check the validator - you should no longer see any errors! However, the image doesn't look so great as it is awkwardly positioned on the page. It would be great if we could scale the image to <strong>responsively</strong> stretch and fit the page no matter the screen size.
 <img class="center " style="max-width: 356.50px" src="/images/lab-2-using-amp-components/app_preview_bicycle.png" alt=" Preview of app with bicycle image" title=" Preview of app with bicycle image">

The <code>layout</code> attribute has a <code>responsive</code> type that automatically scales the image as the window is resized. This layout type requires both the <code>width</code> and <code>height</code> be defined so that AMP can preserve the aspect ratio as the image scales.

Set the <a href="https://www.ampproject.org/docs/guides/responsive/control_layout#supported-values-for-the-layout-attribute"><code>layout</code></a> attribute to <code>responsive</code> to have AMP responsively scale the image:

#### index.html
```
<amp-img src="images/ricotta-racer.jpg" layout="responsive" width="640" height="480"></amp-img>
```
Voila! Our image has the correct aspect ratio and responsively fills the width of the screen.
 <img class="center " style="max-width: 400.50px" src="/images/lab-2-using-amp-components/app_preview_responsive_image.png" alt=" Preview of app with responsive image" title=" Preview of app with responsive image">

<a id="expand-content-with-more-components" />


## 3. Expand content with more components




By now you have a basic AMP document with text and an image. However, modern websites often include more functionality than simply pictures and text.

So let's take our AMP document to the next level and explore what components are available beyond the core components mentioned earlier.

In this chapter we'll try adding more advanced web functionality:

* YouTube videos
* Tweets
* Image Carousels
* Sidebar

### Embed a YouTube video

Let's try embedding a YouTube video into the document.

Add the following code beneath the <code>&#x3C;amp-img></code> and <code>&#x3C;p></code> elements inside the <code>&#x3C;body></code> element:

#### index.html
```
<amp-youtube
  data-videoid="BlpMQ7fMCzA"
  layout="responsive"
  width="480"
  height="270">
  <div fallback>
    <p>The video could not be loaded.</p>
  
</div>

</amp-youtube>
<p>Mixer making the raw material for the new Parmesan Pacer!</p>
```
Save the file. Return to the browser and refresh the page. Notice the video does not appear on the page and we get this error in the AMP validator:
```
The tag 'amp-youtube' requires including the 'amp-youtube' extension JavaScript.
```
Remember, not all components are included in the core AMP JavaScript library. We need to include an additional JavaScript library for the YouTube component. All components except for a core set will require these additional JavaScript references.

Add the following request to the bottom of the <code>&#x3C;head></code> element:

#### index.html
```
<script async custom-element="amp-youtube" src="https://cdn.ampproject.org/v0/amp-youtube-0.1.js"></script>
```
Refresh the page and you should see the YouTube video:
 <img class="center " style="max-width: 414.12px" src="/images/lab-2-using-amp-components/app_preview_video.png" alt=" Preview of app with YouTube video" title=" Preview of app with YouTube video">

Once again we have specified the width and height of the video so that the page is rendered more quickly and elements don't move around as they load. Remember, the height is required for all externally fetched AMP resources.  Furthermore, the layout type has been set to <code>responsive</code>, meaning this video will fill the width of its parent element. This layout type requires us to define the width as well as the height so that AMP can preserve the aspect ratio of the video as it scales.

Learn more about the <a href="https://www.ampproject.org/docs/reference/extended/amp-youtube.html">YouTube component</a>.

<div class="note">
<strong>Note</strong>: In addition to the YouTube component AMP includes a generic HTML5 video component aptly named <a href="https://www.ampproject.org/docs/reference/amp-video.html">amp-video</a> and an AMP component dedicated to the Brightcove Video Cloud or Perform player named <a href="https://www.ampproject.org/docs/reference/extended/amp-brightcove.html">amp-brightcove</a>. Check out "<a href="https://ampbyexample.com/advanced/integrating_videos_in_amp_an_overview/">AMP By Example</a>" for more video playback examples including Facebook videos, Instagram, Vine, Twitter & Dailymotion.
</div>

<div class="note">
<strong>Note</strong>: AMP works across all browsers, but the <a href="https://www.ampproject.org/docs/guides/responsive/control_layout.html#fallback">fallback attribute</a> ensures that some content will be displayed to the user on the off-chance that something happens - like the user loses their connection to the internet.
</div>

### Display a Tweet

Embedding preformatted tweets from Twitter is a common feature of many sites. The AMP Twitter component can provide this functionality with ease.

Start by adding the following JavaScript request to the bottom of the <code>&#x3C;head></code> tag of your document:

#### index.html
```
<script async custom-element="amp-twitter" src="https://cdn.ampproject.org/v0/amp-twitter-0.1.js"></script>
```
Now, add this code beneath the <code>&#x3C;amp-youtube></code> and <code>&#x3C;p></code> elements we added in the previous step:

#### index.html
```
<amp-twitter
  width="486"
  height="657"
  layout="responsive"
  data-tweetid="944269037327892481">
</amp-twitter>
```
The <code>data-tweetid</code> attribute is another example of a custom attribute being required by a particular platform vendor. In this case, Twitter recognises the <code>data-tweetid</code> attribute as corresponding to a particular tweet to be embedded in the page.

Save the code and refresh the page in your browser. You should see the tweet appear:
 <img class="center " style="max-width: 394.37px" src="/images/lab-2-using-amp-components/app_preview_twitter.png" alt=" Preview of app with Twitter post" title=" Preview of app with Twitter post">

Learn more about the <a href="https://www.ampproject.org/docs/reference/extended/amp-twitter.html">Twitter component</a>.

<div class="note">
<strong>Note</strong>: AMP includes even more components for embedding content from social networks. Check out the <a href="https://www.ampproject.org/docs/reference/extended/amp-instagram.html">Instagram component</a> and the <a href="https://www.ampproject.org/docs/reference/extended/amp-vine.html">Vine component</a>.
</div>

<a id="image-carousels" />


## 4. Image Carousels




Another common feature in web development is a carousel, also known as a "slider". A carousel is an element containing a set of images that can be scrolled through horizontally.

There are a host of JavaScript libraries for creating carousels, but they are often non-performant. In fact, carousels full of large images are one of the most common causes of slow page load. 

AMP includes a carousel component, <a href="https://www.ampproject.org/docs/reference/components/amp-carousel"><code>amp-carousel</code></a>, that is designed to be performant; it lazy-loads images that won't be visible for a while.

Let's start with a simple example such as a carousel of images.

Remember to include the carousel component library by adding the following JavaScript request to the bottom of the <code>&#x3C;head></code> tag of your document:

#### index.html
```
<script async custom-element="amp-carousel" src="https://cdn.ampproject.org/v0/amp-carousel-0.1.js"></script>
```
Next we'll embed a simple carousel in the page. 

Add the following code to your page beneath the <code>amp-twitter</code> element:

#### index.html
```
<amp-carousel layout="fixed-height" height="309" type="carousel" >
  <amp-img src="images/cheddar-chaser.jpg" width="412" height="309"></amp-img>
  <amp-img src="images/cheese.jpg" width="412" height="309"></amp-img>
  <amp-img src="images/mouse.jpg" width="412" height="309"></amp-img>
</amp-carousel>
```
Notice we've set the element <code>type</code> attribute to <code>"carousel"</code> and the <code>layout</code> attribute to <code>"fixed-height"</code>. The <code>carousel</code> display type shows all images at once, and they can be scrolled through horizontally. This display type requires a <code>fixed-height</code> layout so that its width can vary, showing more or less of the images in the carousel, but the height does not change. For <code>fixed-height</code> to work, the <code>height</code> attribute must be defined, while the <code>width</code> attribute should not be present or should be set to <code>auto</code>.

Refresh the page and you should see a carousel:
 <img class="center " style="max-width: 411.16px" src="/images/lab-2-using-amp-components/app_preview_carousel.png" alt=" Preview of app with carousel" title=" Preview of app with carousel">

Next, try changing the type to <code>slides</code> instead and look at the result. Be sure to change the <code>layout</code> attribute of the <code>amp-carousel</code> and the images inside it to be <code>responsive</code> as well:

#### index.html
```
<amp-carousel layout="responsive" width="412" height="309" type="slides">
  <amp-img src="images/cheddar-chaser.jpg" width="412" height="309" layout="responsive"></amp-img>
  <amp-img src="images/cheese.jpg" width="412" height="309" layout="responsive"></amp-img>
  <amp-img src="images/mouse.jpg" width="412" height="309" layout="responsive"></amp-img>
</amp-carousel>
```
Now instead of a scrolling list of elements you'll see one element at a time. Try swiping horizontally to move through the elements. If you swipe to the third element you won't be able to swipe any further.

Next, add the <code>loop</code> attribute. Refresh the page and try swiping to the left immediately. The carousel loops endlessly.

Lastly, let's make this carousel autoplay at a rate of every 2 seconds. Add the <code>autoplay</code> attribute to the page and the delay attribute with a value of <code>2000</code> like so: <code>delay="2000"</code>.

Your final result should look something like this:

#### index.html
```
<amp-carousel layout="responsive" width="412" height="309" type="slides" autoplay delay="2000" loop>
  <amp-img src="images/cheddar-chaser.jpg" width="412" height="309" layout="responsive"></amp-img>
  <amp-img src="images/cheese.jpg" width="412" height="309" layout="responsive"></amp-img>
  <amp-img src="images/mouse.jpg" width="412" height="309" layout="responsive"></amp-img>
</amp-carousel>
```
Refresh the page and give it a spin!

Learn more about the <a href="https://www.ampproject.org/docs/reference/extended/amp-carousel.html">Carousel component</a>.

<a id="adding-a-menu" />


## 5. Adding a menu




A common requirement of mobile websites is a site navigation menu. These menus can take many different forms, but a good solution is the <a href="https://www.ampproject.org/docs/reference/components/amp-sidebar"><code>amp-sidebar</code></a> component. This component provides a hidden menu that can contain links to other parts of your site and can be toggled by the tap of a button.

Let's include the <code>amp-sidebar</code> component library at the bottom of the <code>&#x3C;head></code>:

#### index.html
```
<script async custom-element="amp-sidebar" src="https://cdn.ampproject.org/v0/amp-sidebar-0.1.js"></script>
```
Now we're ready to use <code>amp-sidebar</code>.

Add the following snippet to the top of the <code>&#x3C;body></code> element:

#### index.html
```
<amp-sidebar id="sidebar"
  layout="nodisplay"
  side="left">
  <ul>
    <li>
      <a href="#">Our Story</a>
    </li>
    <li>
      <a href="#">Our Bikes</a>
    </li>
    <li>
      <a href="#">Latest Models</a>
    </li>
    <li>
      <a href="#">Contact</a>
    </li>
  </ul>
</amp-sidebar>
```
Now we need a button to open and close the sidebar.

Inside the <code>&#x3C;header></code> in the page's <code>&#x3C;body></code>, add the following button above the site name. The whole <code>&#x3C;header></code> should look like this:

#### index.html
```
<header>
  <div role="button" on="tap:sidebar.toggle" tabindex="0" class="hamburger-menu">☰
</div>

  <div class="site-name">Chico's Cheese Bicycles
</div>

</header>
```
This new <code>&#x3C;div></code> contains a hamburger menu that toggles the sidebar when clicked.

Finally, let's add some CSS to position the icon at the top left of the page and remove bullets from the unordered list in the sidebar.

Add the following rules to the CSS in the <code>&#x3C;head></code>:

#### index.html
```
ul {
  list-style: none;
  margin: 10px;
  padding: 0;
}
li {
  padding: 10px;
}
a {
  color: #000;
  text-decoration: none;
  font-weight: bold;
}
.hamburger-menu {
  float: left;
}
```
Save the file and refresh the page in the browser. Try clicking on the icon to bring up the sidebar menu. You can click on the page to close the sidebar.

Learn more about the <a href="https://www.ampproject.org/docs/reference/components/amp-sidebar"><code>amp-sidebar</code> component</a>.

<a id="congratulations" />


## Congratulations!




You've finished the AMP course and successfully explored many key components of AMP!  Be sure to explore the full list of AMP components <a href="https://www.ampproject.org/docs/reference/extended.html">available</a>.

The following are some additional topics and links you might want to explore to <strong> <em>amplify </em> </strong>your skills even further!

* <a href="https://ampbyexample.com/">AMP By Example</a> - An extensive catalog of examples for AMP components and component patterns.
* <a href="https://dfp-amp-testing-1185.appspot.com/">Double Click Ad Examples</a> - An extensive catalog of amp-ad examples.
* <a href="https://www.ampproject.org/docs/guides/discovery.html">All about Page Discovery</a>
* <a href="https://www.ampproject.org/docs/reference/spec.html">Disallowed HTML Tags</a>
* <a href="https://www.ampproject.org/docs/guides/responsive/style_pages.html#disallowed-styles">Restricted CSS Rules & Animations</a>
* <a href="https://www.ampproject.org/docs/guides/iframes">More on iFrames</a>
* <a href="https://www.ampproject.org/docs/get_started/about-amp.html#amp-cdn">The AMP CDN</a>
* <a href="https://www.ampproject.org/docs/reference/extended.html">List of available AMP Components</a>


