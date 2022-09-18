# cypress-playwright-webkit

## Cypress supports Playwright-Webkit

As you can read in the official blog post, Cypress 10.8.0 has a new experimental feature named [experimentalWebKitSupport](https://www.cypress.io/blog/2022/09/13/cypress-10-8-experimental-run-tests-in-webkit/), so Cypress users can test their web applications using WebKit, the same browser engine used in Safari. By running your existing Cypress tests in WebKit, you can feel confident that your web application is bug-free and works as intended for Safari users.

But, what is WebKit?

## Webkit

[WebKit](https://webkit.org/) is the web browser engine used by Safari, Mail, App Store, and many other apps on macOS, iOS, and Linux.

WebKit is the **open source** web platform implementation used by Apple Safari and Epiphany

## Playwright-Webkit

[Playwright](https://playwright.dev/docs/browsers#webkit) provides a WebKit build that can be download as a node package. Playwright WebKit works across all platforms (macOS, Linux, Windows), in both headless and headful modes.

Playwright's WebKit version matches the recent WebKit trunk build, before it is used in Apple Safari and other WebKit-based browsers. This gives a lot of lead time to react on the potential browser update issues.

You can dowload it here: [Playwright-Webkit](https://www.npmjs.com/package/playwright-webkit)

## What is the difference between testing on Safari vs Webkit?

Answer extracted from this interesting post at [https://exchangetuts.com/](https://exchangetuts.com/what-is-the-difference-between-testing-on-safari-vs-webkit-1639870147015690)

Stock browsers like Google Chrome, Apple Safari embed rendering engines (Chromium, WebKit) and add stuff on top of them. In particular, they add proprietary media codecs, inject browser extensions, etc. They also add surrounding interfaces such as bookmarks sync. But they reuse the underlying web platform implementation.

#### Chromium

Chromium is the open source web platform implementation used by Google Chrome, Opera, Microsoft Edge and other browsers. It implements web specs, renders content, works with network, etc. Playwright uses a stock Chromium build that can be automated with the Playwright API for e2e testing.

For Google Chrome things are simple: Chromium is a safe target to test, modulo proprietary media codecs and DRM. You can point Playwright against stock Chrome Canary or Edge Canary to use proprietary media codecs.

#### WebKit

When WebKit runs on macOS, it is a safe target to test Safari. WebKit on Linux and Windows differs from Apple Safari in the following ways:

- it uses a non-macOS network stack
- uses non-Core Animation to composite scene and produce image raster. This means that screenshots on Linux and Windows will not perfectly match screenshots from macOS.

In terms of the web platform, the same WebKit code will layout the page and run JavaScript—it will match how WebKit works in Safari.

To conclude, we consider the browsers provided by Playwright to be the best of what you can get for e2e testing.

## How to implement this new experimental feature in your framework?

1. Open your cypress.config.js/ts and add the following property:
   ```bash
       experimentalWebKitSupport: true,
   ```
2. Install the playwright-webkit in your project
   ```bash
       npm install --save-dev playwright-webkit
   ```
3. You can specify the browser you need as a cli flag, as well:
   ```bash
       --browser webkit
   ```

#### Known issues:

You can find the known issues in the official documentation: [known-issues](https://docs.cypress.io/guides/guides/launching-browsers#Known-Issues-with-experimentalWebKitSupport)
