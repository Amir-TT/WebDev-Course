<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e982871b8388c59c22a41b73b5fca70f",
  "translation_date": "2025-08-24T13:54:16+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "hi"
}
-->
# इवेंट्स का उपयोग करके गेम बनाना

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/21)

## इवेंट-ड्रिवन प्रोग्रामिंग

जब हम एक ब्राउज़र आधारित एप्लिकेशन बनाते हैं, तो हम उपयोगकर्ता के लिए एक ग्राफिकल यूजर इंटरफेस (GUI) प्रदान करते हैं, जिससे वे हमारे द्वारा बनाए गए एप्लिकेशन के साथ इंटरैक्ट कर सकें। ब्राउज़र के साथ इंटरैक्ट करने का सबसे सामान्य तरीका विभिन्न तत्वों पर क्लिक करना और टाइप करना है। एक डेवलपर के रूप में हमारी चुनौती यह है कि हमें यह नहीं पता होता कि उपयोगकर्ता ये ऑपरेशन कब करेंगे!

[इवेंट-ड्रिवन प्रोग्रामिंग](https://en.wikipedia.org/wiki/Event-driven_programming) वह प्रकार की प्रोग्रामिंग है जो हमें अपने GUI को बनाने के लिए करनी होती है। यदि हम इस वाक्यांश को थोड़ा तोड़ें, तो हम देखेंगे कि इसका मुख्य शब्द **इवेंट** है। Merriam-Webster के अनुसार, [इवेंट](https://www.merriam-webster.com/dictionary/event) का अर्थ है "कुछ जो होता है"। यह हमारी स्थिति को पूरी तरह से वर्णित करता है। हमें पता है कि कुछ ऐसा होगा जिसके लिए हमें प्रतिक्रिया स्वरूप कोड निष्पादित करना है, लेकिन हमें यह नहीं पता कि यह कब होगा।

जिस तरह से हम उस कोड के हिस्से को चिह्नित करते हैं जिसे हम निष्पादित करना चाहते हैं, वह है एक फ़ंक्शन बनाकर। जब हम [प्रोसीजरल प्रोग्रामिंग](https://en.wikipedia.org/wiki/Procedural_programming) के बारे में सोचते हैं, तो फ़ंक्शन्स को एक विशिष्ट क्रम में कॉल किया जाता है। इवेंट-ड्रिवन प्रोग्रामिंग के साथ भी यही बात सच होगी। फर्क सिर्फ इतना है कि **कैसे** फ़ंक्शन्स को कॉल किया जाएगा।

इवेंट्स (जैसे बटन क्लिक करना, टाइप करना आदि) को संभालने के लिए, हम **इवेंट लिसनर्स** रजिस्टर करते हैं। एक इवेंट लिसनर एक फ़ंक्शन होता है जो किसी इवेंट के होने का इंतजार करता है और प्रतिक्रिया स्वरूप निष्पादित होता है। इवेंट लिसनर्स UI को अपडेट कर सकते हैं, सर्वर को कॉल कर सकते हैं, या उपयोगकर्ता की क्रिया के जवाब में जो भी करना हो, वह कर सकते हैं। हम [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) का उपयोग करके और एक फ़ंक्शन प्रदान करके एक इवेंट लिसनर जोड़ते हैं।

> **NOTE:** यह ध्यान देने योग्य है कि इवेंट लिसनर्स बनाने के कई तरीके हैं। आप गुमनाम फ़ंक्शन्स का उपयोग कर सकते हैं, या नामित फ़ंक्शन्स बना सकते हैं। आप `click` प्रॉपर्टी सेट करने जैसे शॉर्टकट्स का उपयोग कर सकते हैं, या `addEventListener` का उपयोग कर सकते हैं। हमारे अभ्यास में, हम `addEventListener` और गुमनाम फ़ंक्शन्स पर ध्यान केंद्रित करेंगे, क्योंकि यह शायद वेब डेवलपर्स द्वारा उपयोग की जाने वाली सबसे सामान्य तकनीक है। यह सबसे लचीला भी है, क्योंकि `addEventListener` सभी इवेंट्स के लिए काम करता है, और इवेंट का नाम एक पैरामीटर के रूप में प्रदान किया जा सकता है।

### सामान्य इवेंट्स

ऐप्लिकेशन बनाते समय आपके लिए [कई दर्जन इवेंट्स](https://developer.mozilla.org/docs/Web/Events) उपलब्ध हैं। मूल रूप से, उपयोगकर्ता द्वारा पेज पर की गई लगभग हर क्रिया एक इवेंट को ट्रिगर करती है, जो आपको यह सुनिश्चित करने की शक्ति देती है कि उन्हें वह अनुभव मिले जो आप चाहते हैं। सौभाग्य से, आमतौर पर आपको केवल कुछ ही इवेंट्स की आवश्यकता होती है। यहां कुछ सामान्य इवेंट्स दिए गए हैं (उनमें से दो का उपयोग हम अपने गेम में करेंगे):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): उपयोगकर्ता ने किसी चीज़ पर क्लिक किया, आमतौर पर एक बटन या हाइपरलिंक
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): उपयोगकर्ता ने राइट माउस बटन क्लिक किया
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): उपयोगकर्ता ने कुछ टेक्स्ट को हाइलाइट किया
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): उपयोगकर्ता ने कुछ टेक्स्ट इनपुट किया

## गेम बनाना

हम इवेंट्स के साथ काम करने के तरीके को समझने के लिए एक गेम बनाएंगे। हमारा गेम एक खिलाड़ी की टाइपिंग स्किल का परीक्षण करेगा, जो कि सभी डेवलपर्स के लिए एक बहुत ही महत्वपूर्ण कौशल है। हमें अपनी टाइपिंग का अभ्यास करते रहना चाहिए! गेम का सामान्य प्रवाह इस प्रकार होगा:

- खिलाड़ी **स्टार्ट** बटन पर क्लिक करता है और उसे टाइप करने के लिए एक कोट दिया जाता है
- खिलाड़ी जितनी जल्दी हो सके टेक्स्टबॉक्स में कोट टाइप करता है
  - जैसे ही प्रत्येक शब्द पूरा होता है, अगला शब्द हाइलाइट हो जाता है
  - यदि खिलाड़ी कोई टाइपो करता है, तो टेक्स्टबॉक्स लाल हो जाता है
  - जब खिलाड़ी कोट पूरा करता है, तो एक सफलता संदेश और समय दिखाया जाता है

आइए अपना गेम बनाएं और इवेंट्स के बारे में जानें!

### फाइल संरचना

हमें कुल तीन फाइलों की आवश्यकता होगी: **index.html**, **script.js** और **style.css**। चलिए इन्हें सेटअप करते हैं ताकि हमारा काम आसान हो जाए।

- एक नया फोल्डर बनाएं और उसमें काम शुरू करने के लिए कंसोल या टर्मिनल में निम्नलिखित कमांड चलाएं:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Visual Studio Code खोलें

```bash
code .
```

- Visual Studio Code में फोल्डर में तीन फाइलें जोड़ें:
  - index.html
  - script.js
  - style.css

## यूजर इंटरफेस बनाएं

यदि हम आवश्यकताओं का विश्लेषण करें, तो हमें अपने HTML पेज पर कुछ तत्वों की आवश्यकता होगी। यह एक रेसिपी की तरह है, जहां हमें कुछ सामग्री चाहिए:

- उपयोगकर्ता के लिए टाइप करने के लिए कोट दिखाने की जगह
- संदेश दिखाने की जगह, जैसे सफलता संदेश
- टाइपिंग के लिए एक टेक्स्टबॉक्स
- एक स्टार्ट बटन

इनमें से प्रत्येक को IDs की आवश्यकता होगी ताकि हम उन्हें अपने JavaScript में उपयोग कर सकें। हम CSS और JavaScript फाइलों के संदर्भ भी जोड़ेंगे जिन्हें हम बनाने जा रहे हैं।

**index.html** नामक एक नई फाइल बनाएं। निम्नलिखित HTML जोड़ें:

```html
<!-- inside index.html -->
<html>
<head>
  <title>Typing game</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Typing game!</h1>
  <p>Practice your typing skills with a quote from Sherlock Holmes. Click **start** to begin!</p>
  <p id="quote"></p> <!-- This will display our quote -->
  <p id="message"></p> <!-- This will display any status messages -->
  <div>
    <input type="text" aria-label="current word" id="typed-value" /> <!-- The textbox for typing -->
    <button type="button" id="start">Start</button> <!-- To start the game -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

### एप्लिकेशन लॉन्च करें

हमेशा यह बेहतर होता है कि हम चीजों को धीरे-धीरे विकसित करें और देखें कि वे कैसी दिखती हैं। चलिए अपना एप्लिकेशन लॉन्च करते हैं। Visual Studio Code के लिए [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) नामक एक शानदार एक्सटेंशन है, जो आपके एप्लिकेशन को लोकली होस्ट करेगा और हर बार जब आप सेव करेंगे, ब्राउज़र को रिफ्रेश करेगा।

- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) इंस्टॉल करें। लिंक पर क्लिक करें और **Install** पर क्लिक करें।
  - ब्राउज़र आपको Visual Studio Code खोलने के लिए कहेगा, और फिर Visual Studio Code इंस्टॉलेशन करने के लिए कहेगा।
  - यदि Visual Studio Code आपको रीस्टार्ट करने के लिए कहे, तो इसे रीस्टार्ट करें।
- इंस्टॉल होने के बाद, Visual Studio Code में Ctrl-Shift-P (या Cmd-Shift-P) दबाएं और कमांड पैलेट खोलें।
- **Live Server: Open with Live Server** टाइप करें।
  - Live Server आपके एप्लिकेशन को होस्ट करना शुरू कर देगा।
- ब्राउज़र खोलें और **https://localhost:5500** पर जाएं।
- अब आपको वह पेज दिखना चाहिए जो आपने बनाया है!

चलो अब कुछ फंक्शनलिटी जोड़ते हैं।

## CSS जोड़ें

हमारे HTML के तैयार होने के बाद, चलिए कोर स्टाइलिंग के लिए CSS जोड़ते हैं। हमें उस शब्द को हाइलाइट करना होगा जिसे खिलाड़ी को टाइप करना चाहिए, और यदि उन्होंने गलत टाइप किया है तो टेक्स्टबॉक्स को रंगीन करना होगा। हम यह दो क्लासेस के साथ करेंगे।

**style.css** नामक एक नई फाइल बनाएं और निम्नलिखित सिंटैक्स जोड़ें:

```css
/* inside style.css */
.highlight {
  background-color: yellow;
}

.error {
  background-color: lightcoral;
  border: red;
}
```

✅ CSS के मामले में आप अपने पेज को अपनी पसंद के अनुसार डिज़ाइन कर सकते हैं। थोड़ा समय लें और पेज को और आकर्षक बनाएं:

- एक अलग फॉन्ट चुनें
- हेडर्स को रंगीन करें
- आइटम्स का आकार बदलें

## JavaScript

हमारे UI के तैयार होने के बाद, अब हम JavaScript पर ध्यान केंद्रित करेंगे, जो लॉजिक प्रदान करेगा। हम इसे कुछ चरणों में तोड़ेंगे:

- [Constants बनाएं](../../../../4-typing-game/typing-game)
- [गेम शुरू करने के लिए इवेंट लिसनर](../../../../4-typing-game/typing-game)
- [टाइपिंग के लिए इवेंट लिसनर](../../../../4-typing-game/typing-game)

लेकिन पहले, **script.js** नामक एक नई फाइल बनाएं।

### Constants जोड़ें

हमें प्रोग्रामिंग को आसान बनाने के लिए कुछ चीजों की आवश्यकता होगी। यह भी एक रेसिपी की तरह है, जहां हमें कुछ सामग्री चाहिए:

- सभी कोट्स की सूची के साथ एक ऐरे
- वर्तमान कोट के सभी शब्दों को स्टोर करने के लिए एक खाली ऐरे
- खिलाड़ी जिस शब्द को टाइप कर रहा है, उसका इंडेक्स स्टोर करने की जगह
- वह समय जब खिलाड़ी ने स्टार्ट पर क्लिक किया

हमें UI तत्वों के संदर्भ भी चाहिए:

- टेक्स्टबॉक्स (**typed-value**)
- कोट डिस्प्ले (**quote**)
- संदेश (**message**)

```javascript
// inside script.js
// all of our quotes
const quotes = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// store the list of words and the index of the word the player is currently typing
let words = [];
let wordIndex = 0;
// the starting time
let startTime = Date.now();
// page elements
const quoteElement = document.getElementById('quote');
const messageElement = document.getElementById('message');
const typedValueElement = document.getElementById('typed-value');
```

✅ अपने गेम में और कोट्स जोड़ें

> **NOTE:** हम `document.getElementById` का उपयोग करके कोड में जब चाहें तत्वों को पुनः प्राप्त कर सकते हैं। चूंकि हम इन तत्वों का नियमित रूप से संदर्भ लेंगे, हम स्ट्रिंग लिटेरल्स के साथ टाइपो से बचने के लिए Constants का उपयोग करेंगे। [Vue.js](https://vuejs.org/) या [React](https://reactjs.org/) जैसे फ्रेमवर्क्स आपके कोड को केंद्रीकृत करने में मदद कर सकते हैं।

`const`, `let` और `var` का उपयोग करने पर एक वीडियो देखें:

[![Types of variables](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "Types of variables")

> 🎥 ऊपर दी गई छवि पर क्लिक करें और वेरिएबल्स के बारे में वीडियो देखें।

### स्टार्ट लॉजिक जोड़ें

गेम शुरू करने के लिए, खिलाड़ी **स्टार्ट** पर क्लिक करेगा। बेशक, हमें यह नहीं पता कि वे कब क्लिक करेंगे। यही वह जगह है जहां [इवेंट लिसनर](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) काम आता है। एक इवेंट लिसनर हमें किसी चीज़ (इवेंट) के होने का इंतजार करने और प्रतिक्रिया स्वरूप कोड निष्पादित करने की अनुमति देता है। हमारे मामले में, हम चाहते हैं कि जब उपयोगकर्ता **स्टार्ट** पर क्लिक करे, तो कोड निष्पादित हो।

जब उपयोगकर्ता **स्टार्ट** पर क्लिक करता है, तो हमें एक कोट चुनना होगा, यूजर इंटरफेस सेटअप करना होगा, और वर्तमान शब्द और समय को ट्रैक करना होगा। नीचे वह JavaScript है जिसे आपको जोड़ने की आवश्यकता है; हम इसे स्क्रिप्ट ब्लॉक के बाद चर्चा करेंगे।

```javascript
// at the end of script.js
document.getElementById('start').addEventListener('click', () => {
  // get a quote
  const quoteIndex = Math.floor(Math.random() * quotes.length);
  const quote = quotes[quoteIndex];
  // Put the quote into an array of words
  words = quote.split(' ');
  // reset the word index for tracking
  wordIndex = 0;

  // UI updates
  // Create an array of span elements so we can set a class
  const spanWords = words.map(function(word) { return `<span>${word} </span>`});
  // Convert into string and set as innerHTML on quote display
  quoteElement.innerHTML = spanWords.join('');
  // Highlight the first word
  quoteElement.childNodes[0].className = 'highlight';
  // Clear any prior messages
  messageElement.innerText = '';

  // Setup the textbox
  // Clear the textbox
  typedValueElement.value = '';
  // set focus
  typedValueElement.focus();
  // set the event handler

  // Start the timer
  startTime = new Date().getTime();
});
```

आइए कोड को तोड़ें!

- शब्द ट्रैकिंग सेटअप करें
  - [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) और [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) का उपयोग करके हम `quotes` ऐरे से एक कोट को रैंडमली चुन सकते हैं
  - हम `quote` को `words` के ऐरे में बदलते हैं ताकि हम उस शब्द को ट्रैक कर सकें जिसे खिलाड़ी वर्तमान में टाइप कर रहा है
  - `wordIndex` को 0 पर सेट किया जाता है, क्योंकि खिलाड़ी पहले शब्द से शुरू करेगा
- UI सेटअप करें
  - `spanWords` का एक ऐरे बनाएं, जिसमें प्रत्येक शब्द एक `span` तत्व के अंदर हो
    - यह हमें डिस्प्ले पर शब्द को हाइलाइट करने की अनुमति देगा
  - `join` का उपयोग करके ऐरे को एक स्ट्रिंग में बदलें, जिसे हम `quoteElement` के `innerHTML` को अपडेट करने के लिए उपयोग कर सकते हैं
    - यह खिलाड़ी को कोट दिखाएगा
  - पहले `span` तत्व के `className` को `highlight` पर सेट करें ताकि इसे पीले रंग में हाइलाइट किया जा सके
  - `messageElement` को साफ करें और `innerText` को `''` पर सेट करें
- टेक्स्टबॉक्स सेटअप करें
  - `typedValueElement` के वर्तमान `value` को साफ करें
  - `typedValueElement` पर `focus` सेट करें
- टाइमर शुरू करें और `getTime` को कॉल करें

### टाइपिंग लॉजिक जोड़ें

जैसे ही खिलाड़ी टाइप करता है, एक `input` इवेंट उठाया जाएगा। यह इवेंट लिसनर यह सुनिश्चित करेगा कि खिलाड़ी सही शब्द टाइप कर रहा है, और गेम की वर्तमान स्थिति को संभालेगा। **script.js** में, अंत में निम्नलिखित कोड जोड़ें। हम इसे बाद में तोड़ेंगे।

```javascript
// at the end of script.js
typedValueElement.addEventListener('input', () => {
  // Get the current word
  const currentWord = words[wordIndex];
  // get the current value
  const typedValue = typedValueElement.value;

  if (typedValue === currentWord && wordIndex === words.length - 1) {
    // end of sentence
    // Display success
    const elapsedTime = new Date().getTime() - startTime;
    const message = `CONGRATULATIONS! You finished in ${elapsedTime / 1000} seconds.`;
    messageElement.innerText = message;
  } else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
    // end of word
    // clear the typedValueElement for the new word
    typedValueElement.value = '';
    // move to the next word
    wordIndex++;
    // reset the class name for all elements in quote
    for (const wordElement of quoteElement.childNodes) {
      wordElement.className = '';
    }
    // highlight the new word
    quoteElement.childNodes[wordIndex].className = 'highlight';
  } else if (currentWord.startsWith(typedValue)) {
    // currently correct
    // highlight the next word
    typedValueElement.className = '';
  } else {
    // error state
    typedValueElement.className = 'error';
  }
});
```

आइए कोड को तोड़ें! हम सबसे पहले वर्तमान शब्द और खिलाड़ी द्वारा अब तक टाइप किए गए मूल्य को प्राप्त करते हैं। फिर हमारे पास वॉटरफॉल लॉजिक है, जहां हम जांचते हैं कि कोट पूरा हो गया है, शब्द पूरा हो गया है, शब्द सही है, या (अंत में), कोई त्रुटि है।

- कोट पूरा हो गया है, यह `typedValue` के `currentWord` के बराबर होने और `wordIndex` के `words` की `length` से एक कम होने से संकेतित होता है
  - `elapsedTime` की गणना `startTime` को वर्तमान समय से घटाकर की जाती है
  - `elapsedTime` को 1,000 से विभाजित करें ताकि इसे मिलीसेकंड से सेकंड में बदल सकें
  - एक सफलता संदेश दिखाएं
- शब्द पूरा हो गया है, यह `typedValue` के एक स्पेस (शब्द के अंत) के साथ समाप्त होने और `typedValue` के `currentWord` के बराबर होने से संकेतित होता है
  - अगले शब्द को टाइप करने की अनुमति देने के लिए `typedElement` के `value` को `''` पर सेट करें
  - अगले शब्द पर जाने के लिए `wordIndex` को बढ़ाएं
  - `quoteElement` के सभी `childNodes` के `className` को `''` पर सेट करें ताकि डिफ़ॉल्ट डिस्प्ले पर वापस आ सकें
  - वर्तमान शब्द के `className` को `highlight` पर सेट करें ताकि इसे अगले टाइप करने वाले शब्द के रूप में चिह्नित किया जा सके
- शब्द वर्तमान में सही टाइप किया गया है (लेकिन पूरा नहीं हुआ है), यह `currentWord` के `typedValue` से शुरू होने से संकेतित होता है
  - `typedValueElement` को डिफ़ॉल्ट रूप से दिखाने के लिए `className` को साफ करें
- यदि हम यहां तक पहुंच गए हैं, तो एक त्रुटि है
  - `typedValueElement` के `className` को `error` पर सेट करें

## अपने एप्लिकेशन का परीक्षण करें

आप अंत तक पहुंच गए हैं! अंतिम चरण यह सुनिश्चित करना है कि हमारा एप्लिकेशन काम कर रहा है। इसे आज़माएं! यदि कोई त्रुटि हो, तो चिंता न करें; **सभी डेवलपर्स** को त्रुटियां होती हैं। संदेशों की जांच करें और आवश्यकतानुसार डिबग करें।

**स्टार्ट** पर क्लिक करें और टाइप करना शुरू करें! यह कुछ इस तरह दिखना चाहिए जैसा हमने पहले एनीमेशन में देखा था।

![गेम का डेमो](../../../../4-typing-game/images/demo.gif)

---

## 🚀 चुनौती

अधिक फंक्शनलिटी जोड़ें

- कोट पूरा होने पर `input` इवेंट लिसनर को अक्षम करें, और बटन क्लिक करने पर इसे फिर से सक्षम करें
- जब खिलाड़ी कोट पूरा कर ले, तो टेक्स्टबॉक्स को अक्षम करें
- सफलता संदेश के साथ एक मोडल डायलॉग बॉक्स दिखाएं
- [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) का उपयोग करके उच्च स्कोर संग्रहीत करें

## व्याख्यान के बाद क्विज़

[व्याख्यान के बाद क्विज़](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/22)

## समीक्षा और स्व-अध्ययन

वेब ब्राउज़र के माध्यम से डेवलपर के लिए उपलब्ध [सभी इवेंट्स](https://developer.mozilla.org/docs/Web/Events) के बारे में पढ़ें, और उन परिदृश्यों पर विचार करें जिनमें आप प्रत्येक का उपयोग करेंगे।

## असाइनमेंट

[एक नया कीबोर्ड गेम बनाएं](assignment.md)

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता के लिए प्रयासरत हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।