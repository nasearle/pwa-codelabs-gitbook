# Lab: Scripting the Service Worker




## Contents




<a href="#overview"><strong>Overview</strong></a>

<a href="#setting-up"><strong>1. Get set up</strong></a>

<a href="#register-service-worker"><strong>2. Register the service worker</strong></a>

<a href="#listen-events"><strong>3. Listening for life cycle events</strong></a>

<a href="#intercept-requests"><strong>4. Intercept network requests</strong></a>

<a href="#explore-scope"><strong>5. Optional: Exploring service worker scope</strong></a>

<a href="#congratulations"><strong>Congratulations!</strong></a>

Concepts: <a href="https://google-developer-training.gitbooks.io/progressive-web-apps-ilt-concepts/content/docs/introduction_to_service_worker.html">Introduction to Service Worker</a>

<a id="overview"/>


## Overview




This lab walks you through creating a simple service worker. 

#### What you will learn

<em> Create a basic service worker script, install it, and do simple debugging

#### What you should know

</em> Basic JavaScript and HTML
<em> Concepts and basic syntax of ES2015 <a href="https://developers.google.com/web/fundamentals/getting-started/primers/promises">Promises</a> 
</em> Concept of an <a href="https://en.wikipedia.org/wiki/Immediately-invoked_function_expression">Immediately Invoked Function Expression</a> (IIFE)
<em> How to enable the developer console

#### What you need before you begin

</em> Computer with terminal/shell access
<em> Connection to the internet 
</em> A <a href="https://jakearchibald.github.io/isserviceworkerready/">browser that supports service workers</a>
<em> A text editor

<a id="setting-up"/>


## 1. Get set up




If you have not downloaded the repository, installed Node, and started a local server, follow the instructions in <a href="setting_up_the_labs.md">Setting up the labs</a>. 

Open your browser and navigate to <strong>localhost:8080/service-worker-lab/app</strong>.

<div class="note">
<strong>Note:</strong> <a href="tools_for_pwa_developers.md#unregister">Unregister</a> any service workers and <a href="tools_for_pwa_developers.md#clearcache">clear all service worker caches</a> for localhost so that they do not interfere with the lab.
</div>

If you have a text editor that lets you open a project, open the <strong>service-worker/app</strong> folder. This will make it easier to stay organized. Otherwise, open the folder in your computer's file system. The <strong>app</strong> folder is where you will be building the lab.

This folder contains:

</em> <strong>other.html</strong>, <strong>js/other.js</strong>, <strong>below/another.html</strong>, and <strong>js/another.js</strong> are sample resources that we use to experiment
<em> <strong>index.html</strong> is the main HTML page for our sample site/application
</em> <strong>index.css</strong> is the cascading stylesheet for <strong>index.html</strong>
<em> <strong>service-worker.js</strong> is the JavaScript file that is used to create our service worker
</em> <strong>styles</strong> folder contains the cascading stylesheets for this lab
<em> <strong>test</strong> folder contains files for testing your progress

<a id="register-service-worker" />


## 2. Register the service worker




Open <strong>service-worker.js</strong> in your text editor. Note that the file contains only an empty function. We have not added any code to run within the service worker yet. 

<div class="note">
<strong>Note:</strong> We are using an <a href="https://en.wikipedia.org/wiki/Immediately-invoked_function_expression">Immediately Invoked Function Expression</a> inside the service worker. This is just a best practice for avoiding namespace pollution; it is not related to the Service Worker API. 
</div>

Open <strong>index.html</strong> in your text editor. 

Replace TODO 2 with the following code:

#### index.html

```
if (!('serviceWorker' in navigator)) {
  console.log('Service worker not supported');
  return;
}
navigator.serviceWorker.register('service-worker.js')
.then(function() {
  console.log('Registered');
})
.catch(function(error) {
  console.log('Registration failed:', error);
});
```

Save the script and refresh the page. The <a href="tools_for_pwa_developers.md#console">console</a> should return a message indicating that the service worker was registered. 

In your browser, navigate to <strong>test-registered.html</strong> (<strong>app/test/test-registered.html</strong>) to confirm that you have registered the service worker. This is a unit test. Passed tests are blue and failed tests are red. If you've done everything correctly so far, this test should be blue. Close the test page when you are done with it.

<div class="note">
<strong>Note:</strong> Be sure to open the test page using the localhost address so that it opens from the server and not directly from the file system.
</div>

<strong>Optional</strong>: Open the site on an <a href="https://jakearchibald.github.io/isserviceworkerready/">unsupported browser</a> and verify that the support check conditional works. 

#### Explanation

Service workers must be registered. Always begin by checking whether the browser supports service workers. The service worker is exposed on the window's <a href="https://developer.mozilla.org/en-US/docs/Web/API/Navigator"><code>Navigator</code></a> object and can be accessed with <code>window.navigator.serviceWorker</code>. 

In our code, if service workers aren't supported, the script logs a message and fails immediately. Calling <code>serviceworker.register(...)</code> registers the service worker, installing the service worker's script. This returns a promise that resolves once the service worker is successfully registered. If the registration fails, the promise will reject.

<a id="listen-events"/>


## 3. Listening for life cycle events




Changes in the service worker's status trigger events in the service worker.

### 3.1 Add event listeners

Open <strong>service-worker.js</strong> in your text editor. 

Replace TODO 3.1 with the following code:

#### service-worker.js

```
self.addEventListener('install', function(event) {
  console.log('Service worker installing...');
  // TODO 3.4: Skip waiting
});

self.addEventListener('activate', function(event) {
  console.log('Service worker activating...');
});
```

Save the file. Close <strong>app/test/test-registered.html</strong> page if you have not already. Manually <a href="tools_for_pwa_developers.md#unregister">unregister the service worker</a> and refresh the page to install and activate the updated service worker. The console log should indicate that the new service worker was registered, installed, and activated. 

<div class="note">
<strong>Note:</strong> All pages associated with the service worker must be closed before an updated service worker can take over.
</div>

<div class="note">
<strong>Note: </strong>The registration log may appear out of order with the other logs (installation and activation). The service worker runs concurrently with the page, so we can't guarantee the order of the logs (the registration log comes from the page, while the installation and activation logs come from the service worker). Installation, activation, and other service worker events occur in a defined order inside the service worker, however, and should always appear in the expected order.
</div>

#### Explanation

The service worker emits an <code>install</code> event at the end of registration. In this case we log a message, but this is a good place for caching static assets. 

When a service worker is registered, the browser detects if the service worker is new (either because it is different from the previously installed service worker or because there is no registered service worker for this site). If the service worker is new (as it is in this case) then the browser installs it. 

The service worker emits an <code>activate</code> event when it takes control of the page. We log a message here, but this event is often used to update caches. 

Only one service worker can be active at a time for a given scope (see <a href="#explore-scope">Exploring service worker scope</a>), so a newly installed service worker isn't activated until the existing service worker is no longer in use. This is why all pages controlled by a service worker must be closed before a new service worker can take over. Since we unregistered the existing service worker, the new service worker was activated immediately.

<div class="note">
<strong>Note: </strong>Simply refreshing the page is not sufficient to transfer control to a new service worker, because the new page will be requested before the the current page is unloaded, and there won't be a time when the old service worker is not in use.
</div>

<div class="note">
<strong>Note:</strong> You can also manually activate a new service worker using some browsers' <a href="tools_for_pwa_developers.md#accesssw">developer tools</a> and programmatically with <a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/skipWaiting"><code>skipWaiting()</code></a>, which we discuss in section 3.4. 
</div>

### 3.2 Re-register the existing service worker

Reload the page. Notice how the events change. 

Now close and reopen the page (remember to close all pages associated with the service worker). Observe the logged events. 

#### Explanation

After initial installation and activation, re-registering an existing worker does not re-install or re-activate the service worker. Service workers also persist across browsing sessions.

### 3.3 Update the service worker

Replace TODO 3.3 in <strong>service-worker.js </strong>with the following comment:

#### service-worker.js

```
// I'm a new service worker
```

Save the file and refresh the page. Notice that the new service worker installs but does not activate. 

Navigate to <strong>test-waiting.html</strong> (<strong>app/test/test-waiting.html</strong>) to confirm that the new service worker is installed but not activated. The test should be passing (blue).

Close all pages associated with the service worker (including the <strong>app/test/test-waiting.html</strong> page). Reopen the <strong>app/</strong> page. The console log should indicate that the new service worker has now activated. 

<div class="note">
<strong>Note:</strong> If you are getting unexpected results, make sure your <a href="tools_for_pwa_developers.md#disablehttpcache">HTTP cache is disabled</a> in developer tools.
</div>

#### Explanation

The browser detects a byte difference between the new and existing service worker file (because of the added comment), so the new service worker is installed. Since only one service worker can be active at a time (for a given scope), even though the new service worker is installed, it isn't activated until the existing service worker is no longer in use. By closing all pages under the old service worker's control, we are able to activate the new service worker.

### 3.4 Skipping the waiting phase

It is possible for a new service worker to activate immediately, even if an existing service worker is present, by skipping the waiting phase. 

Replace TODO 3.4 in <strong>service-worker.js</strong> with the following code:

#### service-worker.js

```
self.skipWaiting();
```

Save the file and refresh the page. Notice that the new service worker installs and activates immediately, even though a previous service worker was in control. 

#### Explanation

The <code>skipWaiting()</code> method allows a service worker to activate as soon as it finishes installation. The install event listener is a common place to put the <code>skipWaiting()</code> call, but it can be called anywhere during or before the waiting phase. See <a href="https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/lifecycle#skip_the_waiting_phase">this documentation</a> for more on when and how to use <code>skipWaiting()</code>. For the rest of the lab, we can now test new service worker code without manually unregistering the service worker.

#### For more information

</em> <a href="https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/lifecycle">Service worker lifecycle</a>

<a id="intercept-requests"/>


## 4. Intercept network requests




Service Workers can act as a proxy between your web app and the network. 

Replace TODO 4 in <strong>service-worker.js</strong> with:

#### service-worker.js

```
self.addEventListener('fetch', function(event) {
  console.log('Fetching:', event.request.url);
});
```

Save the script and refresh the page to install and activate the updated service worker. 

Check the console and observe that no fetch events were logged. Refresh the page and check the console again. You should see fetch events this time for the page and its assets (like CSS).

Click the links to <strong>Other page</strong>, <strong>Another page</strong>, and <strong>Back</strong>.

You'll see fetch events in the console for each of the pages and their assets. Do all the logs make sense? 

<div class="note">
<strong>Note:</strong> If you visit a page and do not have the HTTP cache disabled, CSS and JavaScript assets may be cached locally. If this occurs you will not see fetch events for these resources.
</div>

#### Explanation

The service worker receives a fetch event for every HTTP request made by the browser. The <a href="https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent">fetch event</a> object contains the request. Listening for fetch events in the service worker is similar to listening to click events in the DOM. In our code, when a fetch event occurs, we log the requested URL to the console (in practice we could also create and return our own custom response with arbitrary resources).

Why didn't any fetch events log on the first refresh? By default, fetch events from a page won't go through a service worker unless the page request itself went through a service worker. This ensures consistency in your site; if a page loads without the service worker, so do its subresources.

#### For more information

<em> <a href="https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent">Fetch Event - MDN</a>
</em> <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch">Using Fetch - MDN</a>
<em> <a href="https://developers.google.com/web/updates/2015/03/introduction-to-fetch">Introduction to Fetch - Google Developer</a>

#### Solution code

To get a copy of the working code, navigate to the <strong>04-intercepting-network-requests</strong> folder.

<a id="explore-scope"/>


## 5. Optional: Exploring service worker scope




Service workers have scope. The scope of the service worker determines from which paths the service worker intercepts requests. 

### 5.1 Find the scope

Update the registration code in <strong>index.html</strong> with:

#### index.html

```
if (!('serviceWorker' in navigator)) {
  console.log('Service worker not supported');
  return;
}
navigator.serviceWorker.register('service-worker.js')
.then(function(registration) {
  console.log('Registered at scope:', registration.scope);
})
.catch(function(error) {
  console.log('Registration failed:', error);
});
```

Refresh the browser. Notice that the console shows the scope of the service worker (for example <strong>http://localhost:8080/service-worker-lab/app/</strong>). 

#### Explanation

The promise returned by <code>register()</code> resolves to the <a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration">registration object</a>, which contains the service worker's scope.

The default scope is the path to the service worker file, and extends to all lower directories. So a service worker in the root directory of an app controls requests from all files in the app.

### 5.2 Move the service worker 

Move <strong>service-worker.js</strong> into the <strong>app/below</strong> directory and update the service worker URL in the registration code. <a href="tools_for_pwa_developers.md#unregister">Unregister the service worker</a> and refresh the page. 

The console shows that the scope of the service worker is now <strong>localhost:8080/service-worker-lab/app/below/</strong>. 

Navigate to <strong>test-scoped.html</strong> (<strong>app/test/test-scoped.html</strong>) to confirm that that service worker is registered in <strong>app/below/</strong>. If you've done everything correctly, you shouldn't see any red errors. Close the test page when you are done with it.

Back on the main page, click <strong>Other page</strong>,  <strong>Another page</strong> and  <strong>Back</strong>. Which fetch requests are being logged? Which aren't?

#### Explanation

The service worker's default scope is the path to the service worker file. Since the service worker file is now in <strong>app/below/</strong>, that is its scope. The console is now only logging fetch events for <strong>another.html</strong>, <strong>another.css</strong>, and <strong>another.js</strong>, because these are the only resources within the service worker's scope (<strong>app/below/</strong>).

### 5.3 Set an arbitrary scope

Move the service worker back out into the project root directory (<strong>app</strong>) and update the service worker URL in the registration code.

Use the <a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerContainer/register">reference on MDN</a> to set the scope of the service worker to the <strong>app/below/</strong> directory using the optional parameter in <code>register()</code>. <a href="tools_for_pwa_developers.md#unregister">Unregister the service worker</a> and refresh the page. Click <strong>Other page</strong>, <strong>Another page</strong> and <strong>Back</strong>.

Again the console shows that the scope of the service worker is now <strong>localhost:8080/service-worker-lab/app/below</strong>, and logs fetch events only for <strong>another.html</strong>, <strong>another.css</strong>, and <strong>another.js</strong>. 

Navigate to <strong>test-scoped.html</strong> again to confirm that the service worker is registered in <strong>app/below/</strong>. 

#### Explanation

It is possible to set an arbitrary scope by passing in an additional parameter when registering, for example:

#### index.html

```
navigator.serviceWorker.register('/service-worker.js', {
  scope: '/kitten/'
});
```

In the above example the scope of the service worker is set to <strong>/kitten/</strong>. The service worker intercepts requests from pages in <strong>/kitten/</strong> and <strong>/kitten/lower/</strong> but not from pages like <strong>/kitten</strong> or <strong>/</strong>. 

<div class="note">
<strong>Note:</strong> You cannot set an arbitrary scope that is above the service worker's actual location.
</div>

#### For more information

</em> <a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration">Service worker registration object</a>
<em> <a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerContainer/register">The register() method</a>
</em> <a href="https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration/scope">Service worker scope</a>

#### Solution code

To get a copy of the working code, navigate to the <strong>solution</strong> folder.

<a id="congratulations"/>


## Congratulations!




You now have a simple service worker up and running.


