# जावास्क्रिप्ट की परिचय

चलिए हम देखते हैं कि जावास्क्रिप् इतना खास क्यों है, हम इस से क्या प्राप्त कर सकते हैं और कौन से अन्य टेक्नोलॉजी इसके साथ अच्छे से काम करते हैं

## जावास्क्रिप्ट क्या है?

*जावास्क्रिप्ट* को पहली बार *वेब पेजेस चलाने* के लिए बनाया गया था

इस भाषा में प्रोग्राम को *स्क्रिप्ट्स* कहा जाता है. वे एचटीएमएल में डायरेक्टली लिखे जा सकते हैं और पेज लोड होते ही ऑटोमेटिकली रन होते हैं.

स्क्रिप्ट्स को सामान्य टेक्स्ट के रूप में पर्याप्त और एक्सीक्यूट किया जाता है. उन्हें रन करने के लिए स्पेशल प्रिपरेशन या कंपाइलेशन की जरुरत नहीं पड़ती.

इस मामले में, जावास्क्रिप्ट [जावा](https://hi.wikipedia.org/wiki/%E0%A4%9C%E0%A4%BE%E0%A4%B5%E0%A4%BE_(%E0%A4%AA%E0%A5%8D%E0%A4%B0%E0%A5%8B%E0%A4%97%E0%A5%8D%E0%A4%B0%E0%A4%BE%E0%A4%AE%E0%A4%BF%E0%A4%82%E0%A4%97_%E0%A4%AD%E0%A4%BE%E0%A4%B7%E0%A4%BE)) कही जानेवाली दूसरी भाषा से एकदम अलग है.

```smart header="इसे जावास्क्रिप्ट क्यों केहते है?"
जब जावास्क्रिप्ट को बनाया गया था, पेहले उसका दूसरा नाम था: "लाइवस्क्रिप्ट". लेकिन उस वक्त जावा जावा बहोत पोपुलर था, इसलिए यह निर्णय लिया गया की अगर इस नई भाषा को जावा के "छोटे भैया" के रूप में पेश किया जायेगा तो मदद मिलेगी.

मगर जैसे जैसे यह विकसित हुई, जावास्क्रिप्ट उसके अपने इसीऍमअएस्क्रिप्ट कहे जानेवाले स्पेसिफिकेशन के साथ पूरी तरह से एक स्वतंत्र भाषा बन गई, और अब उसका जावा के साथ किसी भी तरह से कोई नाता नहीं है.
```

आज, जावास्क्रिप्ट न सिर्फ ब्राउज़र में एक्सीक्यूट हो सकती है, पर सर्वर पर भी, या वास्तव में कोई भी डिवाइस पर जिसके पास जावास्क्रिप्ट इंजन कहा जानेवाला स्पेशल प्रोग्राम है.


The browser has an embedded engine sometimes called a "JavaScript virtual machine".

Different engines have different "codenames". For example:

- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- in Chrome and Opera.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- in Firefox.
- ...There are other codenames like "Trident" and "Chakra" for different versions of IE, "ChakraCore" for Microsoft Edge, "Nitro" and "SquirrelFish" for Safari, etc.

The terms above are good to remember because they are used in developer articles on the internet. We'll use them too. For instance, if "a feature X is supported by V8", then it probably works in Chrome and Opera.

```smart header="How do engines work?"

Engines are complicated. But the basics are easy.

1. The engine (embedded if it's a browser) reads ("parses") the script.
2. Then it converts ("compiles") the script to the machine language.
3. And then the machine code runs, pretty fast.

The engine applies optimizations at each step of the process. It even watches the compiled script as it runs, analyzes the data that flows through it, and further optimizes the machine code based on that knowledge.
```

## What can in-browser JavaScript do?

Modern JavaScript is a "safe" programming language. It does not provide low-level access to memory or CPU, because it was initially created for browsers which do not require it.

JavaScript's capabilities greatly depend on the environment it's running in. For instance, [Node.js](https://wikipedia.org/wiki/Node.js) supports functions that allow JavaScript to read/write arbitrary files, perform network requests, etc.

In-browser JavaScript can do everything related to webpage manipulation, interaction with the user, and the webserver.

For instance, in-browser JavaScript is able to:

- Add new HTML to the page, change the existing content, modify styles.
- React to user actions, run on mouse clicks, pointer movements, key presses.
- Send requests over the network to remote servers, download and upload files (so-called [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) and [COMET](https://en.wikipedia.org/wiki/Comet_(programming)) technologies).
- Get and set cookies, ask questions to the visitor, show messages.
- Remember the data on the client-side ("local storage").

## What CAN'T in-browser JavaScript do?

JavaScript's abilities in the browser are limited for the sake of the user's safety. The aim is to prevent an evil webpage from accessing private information or harming the user's data.

Examples of such restrictions include:

- JavaScript on a webpage may not read/write arbitrary files on the hard disk, copy them or execute programs. It has no direct access to OS system functions.

    Modern browsers allow it to work with files, but the access is limited and only provided if the user does certain actions, like "dropping" a file into a browser window or selecting it via an `<input>` tag.

    There are ways to interact with camera/microphone and other devices, but they require a user's explicit permission. So a JavaScript-enabled page may not sneakily enable a web-camera, observe the surroundings and send the information to the [NSA](https://en.wikipedia.org/wiki/National_Security_Agency).
- Different tabs/windows generally do not know about each other. Sometimes they do, for example when one window uses JavaScript to open the other one. But even in this case, JavaScript from one page may not access the other if they come from different sites (from a different domain, protocol or port).

    This is called the "Same Origin Policy". To work around that, *both pages* must agree for data exchange and contain a special JavaScript code that handles it. We'll cover that in the tutorial.

    This limitation is, again, for the user's safety. A page from `http://anysite.com` which a user has opened must not be able to access another browser tab with the URL `http://gmail.com` and steal information from there.
- JavaScript can easily communicate over the net to the server where the current page came from. But its ability to receive data from other sites/domains is crippled. Though possible, it requires explicit agreement (expressed in HTTP headers) from the remote side. Once again, that's a safety limitation.

![](limitations.svg)

Such limits do not exist if JavaScript is used outside of the browser, for example on a server. Modern browsers also allow plugin/extensions which may ask for extended permissions.

## What makes JavaScript unique?

There are at least *three* great things about JavaScript:

```compare
+ Full integration with HTML/CSS.
+ Simple things are done simply.
+ Support by all major browsers and enabled by default.
```
JavaScript is the only browser technology that combines these three things.

That's what makes JavaScript unique. That's why it's the most widespread tool for creating browser interfaces.

That said, JavaScript also allows to create servers, mobile applications, etc.

## Languages "over" JavaScript

The syntax of JavaScript does not suit everyone's needs. Different people want different features.

That's to be expected, because projects and requirements are different for everyone.

So recently a plethora of new languages appeared, which are *transpiled* (converted) to JavaScript before they run in the browser.

Modern tools make the transpilation very fast and transparent, actually allowing developers to code in another language and auto-converting it "under the hood".

Examples of such languages:

- [CoffeeScript](http://coffeescript.org/) is a "syntactic sugar" for JavaScript. It introduces shorter syntax, allowing us to write clearer and more precise code. Usually, Ruby devs like it.
- [TypeScript](http://www.typescriptlang.org/) is concentrated on adding "strict data typing" to simplify the development and support of complex systems. It is developed by Microsoft.
- [Flow](http://flow.org/) also adds data typing, but in a different way. Developed by Facebook.
- [Dart](https://www.dartlang.org/) is a standalone language that has its own engine that runs in non-browser environments (like mobile apps), but also can be transpiled to JavaScript. Developed by Google.

There are more. Of course, even if we use one of transpiled languages, we should also know JavaScript to really understand what we're doing.

## Summary

- JavaScript was initially created as a browser-only language, but is now used in many other environments as well.
- Today, JavaScript has a unique position as the most widely-adopted browser language with full integration with HTML/CSS.
- There are many languages that get "transpiled" to JavaScript and provide certain features. It is recommended to take a look at them, at least briefly, after mastering JavaScript.
