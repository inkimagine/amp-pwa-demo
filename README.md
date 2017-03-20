# AMP+PWA Demo for Blog and News Sites

A simple, dependency-free blog that uses a
[Progressive Web App](https://developers.google.com/web/progressive-web-apps/)
(PWA) to show [Accellerated Mobile Pages](https://www.ampproject.org/) (AMP).
__This is not an official Google product.__


## Setup

This project requires `node` and `npm` which can be installed
[here](https://nodejs.org/en/download/).

In the root of this repo, run `npm install` to download all dependencies, and
then `npm start` to start the server. You can visit the site at
[localhost:8080](localhost:8080).

Note that this is just a _demo site_. Some features (e.g. push notifications)
require a more complex backend that is not implemented here.


## Implementation Details

Our site uses AMP and PWA to create a site that loads as fast as possible, while
still allowing users to take advantage of some of the most recent web platform
features like push notifications and offline browsing.

The front end consists of three main components:

- __AMP templates__: All pages are valid AMP pages. We'll only have to maintain
  a single set of templates (rather than a conventional version and a separate
  AMP version).
- __App Shell__: This is an empty HTML page that contains some scripts to
  download content.
- __Service Worker__

The first pageview will always be an AMP page. If visitors are coming from
Google search results, this page will be loaded directly from the Google AMP
cache. In the background, the AMP page will install the service worker, which in
turn will cache the app shell page and some other resources.

Any further pageview will be intercepted by the service worker. It returns the
app shell, rather than the requested page, and the app shell will then load the
actual content using AJAX.

While the content shown inside the app shell is still valid AMP, we can now use
custom JavaScript to add functionality that is not (yet) supported by AMP. Note
however that this functionality will not be available on the first pageview, or
in browsers that don't support service workers. The App Shell can also intercept
link clicks and use the web history API to create a "single page app".


## TODO List

- [ ] P1 Add Articles, images and core CSS
- [ ] P2 Get article title and thumbnail for offline page and notifications.
- [ ] P2 Automatically refresh offline page when back online
- [ ] P3 Notifications server
- [ ] P3 Run the demo site on GitHub pages
- [ ] P3 404 Error pages
- [ ] P4 Better analytics
