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
* [Flatten a CXDDL data layer (digitalData)](#DL)
* [Flatten an Adobe Analytics tracking request URL](#AA)
* [Export a console table to CSV](#CSV)
* [Generate a unique, one-time only, last name](#Unique)
* [Step through pages and auto-fill forms](#Next)
* [Override example](#Over)

To create a new snippet:

1. Open DevTools
2. Locate the Sources tab
3. Locate the Snippets tab under Sources
4. Click on "+ New snippet"
5. Name your new snippet
6. Add Javascript code
7. Save your snippet - if there's a * next to the snippet name, it's not saved!
8. Right-click on your snippet and select "Run" - you could use a Chrome extension to link your snippet to a keyboard shortcut, but your company might not let you install that extension

<a id="DL"></a>
### Flatten a CXDDL data layer (digitalData)

This is not about the event-driven data layer. That sort of data layer is an array. The one I am dealing with here is a JSON object, and the code snippet below will flatten that JSON and return a console table. You can create the snippet with the code provided with this link or run it if you have already done so:

https://github.com/alban-gerome/javascript/blob/main/datalayer

[](#Table-of-contents)

<a id="AA"></a>
### Flatten an Adobe Analytics tracking request URL

This will only work with Adobe Anaytics tracking requests, not Google Analytics.

1. Open DevTools
2. Go to the network tab
3. Search for requests containing "/b/ss/"
4. Right-click and copy the URL you need to decode
5. Open the console and paste this code below
6. Go to the Sources tab, select Snippets
7. Create the snippet with the code below or run it

```js:
localStorage.setItem("aa","[paste your Adobe Analytics tracking requests here]");
```

https://github.com/alban-gerome/javascript/blob/main/adobeanalytics

Please notice the small JSON at the bottom of the file, and the "ignore" key. You can add or remove keys that are not relevant for your analysis, remove all the noise and keep only what matters. It's a pipe-separated list (|).

[Back to Table of Contents](#Table-of-contents)

<a id="CSV"></a>
### Export a console table to CSV

Create a snippet and feel free to edit the file name as needed. Please note that the snippet can only generate a CSV file, no other Excel file type. The snippet will drop the CSV files into your downloads folder. This can't be changed, it's always going to be the downloads folder. Here's the link to the code below:

https://github.com/alban-gerome/javascript/blob/main/generateCSV

[](#Table-of-contents)
<a id="Unique"></a>
### Generate a unique, one-time only, last name

We used to use the same first name, last name, date of birth details for all our testing. That caused a database constraint error so we were told to use a random combination. Random, gotcha, no problem. How do you keep track of them? All it takes is one of these 3 items to change to have a unique combination. As it turns out, Javascript can return the date down to the second and you can convert that to the number of seconds elapsed since Jan, 1st 1970 with this line of code:

```js:
new Date() - 0 // -0 will convert the date to a number
```

Then you could replace any zeroes to the letter "a", ones to "b", twos to "c" etc. Finally, capitalise the first letter. But then, the code below will:

* Print the name into the console
* Give you 3 seconds to click into any text field of your choice on a web page and ready to paste there

[Back to Table of Contents](#Table-of-contents)

<a id="Next"></a>
### Step through pages and auto-fill forms

The code for this snippet comes into 2 parts. At the very bottom you will need to provide a JSON that will be specific to your web journeys. When you do, this snippet will fill all forms fields on your web page and take you to the next page. All you do is go, next page, next page, next page. The snippet requires the CXDDL (digitalData) data layer and expects the page name to be under digitalData.page.pageName. But you could make it work with another type of data layer.

The JSON is 2-levels deep:

1. Page names as found under digitalData.page.pageName
2. A CSS selector for the element to be interacted with as the key, and the value for that element

For best results the elements need to have an id attribute value. But there is none, use the default "+" key with the following value:

```js:
(o, s, ac) => s(".myLifeUWPaddingleft label", 3, null)
```

With the code above, the "s" function takes 3 parameters:

1. CSS selector that returns several elements
2. Which one of the many items the selector above returns, which one is the snippet needs to interact with
3. Same as the value you pass for when your key is a CSS selector for a unique DOM element - null means "no value no enter, just click on it"

Here's another example for several elements that have no id attributes on a given page

```js:
(o, s, ac) => [11, 13, 15, 16, 21, 25].map(aj => s(".myLifeUWPaddingleft label", aj, null))
```

The code above means that you have a collection of DOM elements for the ".myLifeUWPaddingleft label" CSS selector rather than just one, and you need item #11, #13, #15, #16, #21 and #25. Since the value is null, the snippet will click on all 6 DOM elements.

If you need to wait before interacting with a specific field, here's an example:

```js:
"+"                                        : (o, s, ac) => o(1000).then(() => ac({
  "#monthlypremium"                        : null,
  "#getQuote"                              : null
}))
```
Notice the number 1000 above. That's the number of milliseconds you need the snippet to wait. 1000 milliseconds means 1 second, 3000 means 3 seconds.

Here are below examples of 4 full top-level sections in your JSON:

```js:
"Page 1" : {
   "+"                            : () => {
      if(typeof _satellite == "undefined")          return null;
      if(typeof _satellite.setDebug == "undefined") return null;
      _satellite.setDebug(true);
    },
    "#onetrust-accept-btn-handler"             : null,
    "#dobDay1"                                 : 10,
    "#dobMonth1"                               : 10,
    "#dobYear1"                                : 1970,
    "#manualAddress"                           : null,
    "#addressline1"                            : "5th Floor",
    "#addressline2"                            : "My street",
    "#addressline4"                            : "Some town",
    "#postcode"                                : "Some postcode",
    "#UseAddress"                              : null, //click on that
    "#email"                                   : "mail@mail.com",
    "#getQuote"                                : null
  },
  "Quote Start" : {
    "#coverTypeLevelLabel"                     : null,
    "#policyTypeSingleLabel"                   : null,
    "#monthlypremium"                          : "20",
    "#coverLength"                             : "20",
    "#noneLabel1"                              : null,
    "+"                                        : (o, s, ac) => o(1000).then(() => ac({ // wait 1 second
      "#monthlypremium"                        : null,
      "#getQuote"                              : null
    }))
  },
  "Work and Travel" : {
    "+"                                        : (o, s, ac) => [0, 8, 10, 12, 14].map(ai => s(".myLifeUWPaddingleft label", ai, null)), //click on 5 radio buttons
    "#acceptButton"                            : null
  }, 
  "Leisure Activities" : {
    "+"                                        : (o, s, ac) => s(".myLifeUWPaddingleft label", 7, null), //find that single element and click on it
    "#acceptButton"                            : null
  }
```
Remember that the JSON above is for you to figure out. You can find the CSS selectors of an element by right-clicking on it, inspect the element, right click on it and on the DevTools element tab, right-click on the element there and copy the selector. But if the selector is too long, or does not return a unique element create a "+" key.

[Back to Table of Contents](#Table-of-contents)

<a id="Over"></a>
### Override example

That one is only a 11th hour discovery the day before MeasureCamp. I was aware of DevTools Sources overrides but unsure of how they differ from snippets. Imagine you want to do a prank to your manager. You could take your production website home page, inspect elements on the screen and edit the entire HTML. But your boss was not born yesterday and will hit refresh and your prank falls flat. But what if you could save the changes so that when your boss refreshes the screen, oh shock and horror, it's still there! You can do that with overrides. Chrome will do a lookup for saved changes for that page and apply them. Here are the stesp to do that, you won't be able to say I didn't give you enough time before April Fools' day:

1. Open DevTools
2. Locate the Sources tab
3. Locate the Overrides tab under Sources
4. Click the "Enable Local Overrides" checkbox
5. Provide a folder name, all Overrides for a given domain will be stored in that folder
6. The pane on the right will show you the page source code. That's where you want to modify the page HTML. Do your worst!
7. Save your override

In the example I demoed at MeasureCamp San Francisco I added an inline script block that will print to the console the full URL for all image requests that fired on the page. That's most of your marketing pixels, Adobe Analytics etc, but not the base tags because they are based on script tags rather than images. So, only images and the script is straight off an old post by O'Reilly books writer Stoyan Stefanov (https://www.phpied.com/intercepting-new-image-src-requests/).

```html:
<script>
  const NativeImage = Image;  
  class FakeImage {
    constructor(w, h) {
      const nativeImage = new NativeImage(w, h);
      const handler = {
        set: (obj, prop, value) => {
          if(prop === "src") {
            console.log('gotcha ' + value);
          }
          return nativeImage[prop] = value;
        },
        get: (target, prop) =>  target[prop];
      };
      return new Proxy(nativeImage, handler);
    };
  };  
  Image = FakeImage;
</script>
```
I have found a shorter more modern version that achieves the same thing:
```html:
const a = Object.getOwnPropertyDescriptor(HTMLImageElement.prototype, "src");
Object.defineProperty(HTMLImageElement.prototype, "src", { 
  set: function(b){
    console.log(b);
    a.set.call(this, b);
  }
});
```
I just need to get the snippet above to work with script elements with a src attribute and possibly iframes, Ajax requests, fetch requests. That's so fetch! That would expose all network requests the tags we work with fire and then we can isole all Adobe Analytics requests from that trove of information, decode them and generate the CSVs on the fly!

Another use is to inject the Adobe Launch monitoring hooks as per this article by Aaron Hardy: https://medium.com/adobetech/launch-library-monitoring-hooks-c674d16deae3. Please note that the article misses a 4th hook called "ruleConditionFailed".

[Back to Table of Contents](#Table-of-contents)

All these can work together in sequence. For example use the snippet that will automatically fill your pages, flatten the data layer, export to CSV, find the Adobe Analytics request with the override, pass the URL to localStorage, flatten it, export it, next page. Now, you are a true Snippet Jockey!

Alban Gérôme
27 Jul 2022

Follow me on Twitter: <a href="https://twitter.com/albangerome?lang=en-gb" title="Follow Alban Gérôme on  Twitter">@albangerome</a>
