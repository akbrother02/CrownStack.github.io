---
title:  "Tips to improve the performance of your Website"
date: 2017-11-30
author: Ajay Upreti
categories:
- blog
tags:
- frontend
---


In this blog, I'm going to highlight ways in which you can improve the performance of your Websites.


# Page Speed
* **Keep page weight under 2MB**. Use tools.pingdom.com to check the page weight for your primary landing pages. Anything more than 2MB is too heavy.
* **Keep page requests under 50**. Every file and image on any given page is a HTTP request. The fewer the number of requests, the faster it’ll load. The average webpage has 70 requests. Use GTmetrix to see your requests.
* **Design page elements with CSS instead of background images.** Never use an image to show a button, form, or other common component on your site. CSS loads faster and is more flexible in responsive layouts.
* **Optimize images** before uploading them to your site. Tools like TinyPNG can reduce your image file sizes by 80–95% without losing resolution or image quality.
* **Set up a Content Delivery Network** to host your images and other larger files in several locations around the world. CDNs store and deliver your files from strategically located servers to maximize loading speed depending on your visitor’s physical location.
* **Minify JavaScript, HTML, and CSS** by using compiling and compression tools prior to uploading files to your website. For JavaScript, use Closure Compiler. For HTML, use HTML Minifier. For CSS, use YUI Compressor.
* **Move render-blocking JavaScript to the footer.** The only scripts that should be placed in the header are the scripts that immediately affect the design of the page.
* **Avoid landing page redirects.** Redirects trigger an additional HTTP request which delays page rendering.
* **Leverage browser caching** by setting expiry dates for pages and page types that aren’t updated often. Browser caching instructs the browser to load previously downloaded pages from the local disk rather than through the network.
* **Enable gzip compression** in your server configuration. Compression can reduce the transferred response time by 90% which improves the time to first render for your pages.

# Head
* **Doctype:** The Doctype is HTML5 and is at the top of all your HTML pages.
* **Charset:** The charset declared (UTF-8) is declared correctly.
* **X-UA-Compatible:** The X-UA-Compatible Meta tag is present.
* **Viewport:** The viewport is declared correctly.
* **Title:** A title is used on all pages
* **Description:** A meta description is provided, it is unique and doesn't possess more than 150 characters.
* **Favicons:** Each favicon has been created and displays correctly.
* **Apple Touch Icon:** Apple touch favicon apple-mobile-web-app-capable are present
* **Windows Tiles:** Windows tiles are present and linked.
* **Canonical:** Use rel="canonical" to avoid duplicate content.
* **Language attribute:** The <code>lang</code> attribute of your website is specified and related to the language of the current page.
* **Inline critical CSS:** The inline critical CSS is correctly injected into the HEAD.
* **CSS order:** All CSS files are loaded before any JavaScript files in the HEAD.

# HTML
* **Webfont format:** WOFF, WOFF2 and TTF are supported by all modern browsers.
* **Webfont size:** Webfont sizes don't exceed 2 MB (all variants included).
* **HTML5 Semantic Elements:** HTML5 Semantic Elements are used appropriately (header, section, footer, main...).
* **Error pages:** Error 404 page and 5xx exist
* **Noopener:** In case you are using external links with target="_blank", your link should have a rel="noopener" attribute to prevent tab nabbing. If you need to support older versions of Firefox, use rel="noopener noreferrer"
* **W3C compliant:** All pages need to be tested with the W3C validator to identify possible issues in the HTML code.
* **HTML Lint:** I use tools to help me analyze any issues I could have with my HTML code.
* **link checker:** There are no broken links on my page, verify that you don't have any 404 error.
* **Adblockers test:** Your website shows your content correctly with adblockers enabled

# Images
* **Optimization:** All images are optimized to be rendered in the browser. WebP format could be used for critical pages (like Homepage)
* **Picture/Srcset:** You use picture/srcset to provide the most appropriate image for the current viewport of the user.
* **Sprite:** Small images are in a sprite file (in the case of icons, they can be in an SVG sprite image).
* **Width and Height:** Set width and height attributes on <img> if the final rendered image size is known (can be omitted for CSS sizing).
* **Alternative text:** All <img> have an alternative text which describes the image visually.

# SEO
* **Google Analytics:** Google Analytics is installed and correctly configured.
* **Headings logic:** Heading text helps to understand the content on the current page.
* **sitemap.xml:** A sitemap.xml exists and was submitted to Google Search Console.
* **Sitemap HTML:** An HTML sitemap is provided and is accessible via a link in the footer of your website.

# Accessibility
* **H1:** High All pages have an H1 which is not the title of the website.
* **Headings:** High Headings should be used properly and in the right order (H1 to H6).
