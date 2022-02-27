MeasureCamp San Francisco - Feb 26th 2022
====================================

Chrome DevTools snippets and overrides for increased productivity
-----------------------------------------------------------------

WARNING: If you report to a manager whose compensation depends on the size of the team they manage, do not use these scripts! It will ruin their plans to grow the team because you will be able to do so much more by yourself!

You might be familiar with the DevTools console and network tab. What about the Sources tab? This will contain 2 features that you might not know:

* Snippets
* Overrides

I used to have many tabs in Notepad++, a text editor, which all sorts of scripts in Javascript or Python ready for me to copy and paste. Then I explored DevTools more in depth as ever before to reasearch for an online course on the browser. That's how I stumbed upon the snippets and the overrides in DevTools Sources. Instead of copy and pasting code, I might have created a bookmarklet. Bookmarklets become quickly impractical after a few lines of Javascript because you need to remove all code indentation and line feed-carriage returns. That's not fun, therefore keeping code in a text editor came in handy. But now with DevTools Source snippets, I saved them all as separate snippets.

And then as an 11th hour experiment, I wanted to understand the difference between DevTools Source snippets and overrides. Chrome lets you edit the HTML of a given page just for you. But then the page will forget these changes as you return to that page later or refresh it. With overrides, you can make Chrome remember to reproduce these changes for you. I was able to use that to add an inline script tag in the head of one the pages I work with, before every other script loads on the page.

You might have experience with writing Chrome extensions. That's a lot of fun, but companies often lock down that feature. But DevTools snippets and overrides might still work for you. With these, I am able to circumvent these limitations, but also simplify the code that my code extension would need. I use overrides for code logic I want to apply at page load, and snippets for what I need to do after the page has loaded. By page, I mean both traditional web page and single-page application view.

<a id="Table-of-contents"></a>
### Table of contents:
----------------------
* [Flatten a CXDDL data layer (digitalData)](#)
* [Flatten an Adobe Analytics tracking request URL] (#)
* [Export a console table to CSV] (#)
* [Generate a unique, one-time only, last name] (#)
* [Step through pages and auto-fill forms] (#)
* [Override example]

<a id=""></a>
### Flatten a CXDDL data layer (digitalData)
This is not about the event-driven data layer. That sort of data layer is an array. The one I am dealing with here is a JSON object, and the code snippet below will flatten that JSON and return a console table.

(#Table-of-contents)
<a id=""></a>
### Flatten an Adobe Analytics tracking request URL

(#Table-of-contents)
<a id=""></a>
### Export a console table to CSV

(#Table-of-contents)
<a id=""></a>
### Generate a unique, one-time only, last name

(#Table-of-contents)
<a id=""></a>
### Step through pages and auto-fill forms

(#Table-of-contents)
<a id=""></a>
### Override example

(#Table-of-contents)

Alban Gérôme
27 Jul 2022

Follow me on Twitter: <a href="https://twitter.com/albangerome?lang=en-gb" title="Follow Alban Gérôme on  Twitter">@albangerome</a>
