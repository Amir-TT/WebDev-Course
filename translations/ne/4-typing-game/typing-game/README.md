<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e982871b8388c59c22a41b73b5fca70f",
  "translation_date": "2025-08-26T01:05:02+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "ne"
}
-->
# घटनाहरू प्रयोग गरेर खेल बनाउने

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/21)

## घटना-आधारित प्रोग्रामिङ

जब हामी ब्राउजरमा आधारित एप्लिकेसन बनाउँछौं, हामीले प्रयोगकर्तालाई हाम्रो बनाएको चीजसँग अन्तरक्रिया गर्न ग्राफिकल प्रयोगकर्ता इन्टरफेस (GUI) प्रदान गर्छौं। ब्राउजरसँग अन्तरक्रिया गर्ने सबैभन्दा सामान्य तरिका भनेको विभिन्न तत्वहरूमा क्लिक गर्ने र टाइप गर्ने हो। तर, हामीलाई थाहा छैन प्रयोगकर्ताले यी कार्यहरू कहिले गर्नेछन्, जुन हाम्रो चुनौती हो!

[घटना-आधारित प्रोग्रामिङ](https://en.wikipedia.org/wiki/Event-driven_programming) भनेको GUI बनाउन आवश्यक पर्ने प्रोग्रामिङको प्रकार हो। यदि हामी यस वाक्यांशलाई अलिकति तोड्यौं भने, यसको मुख्य शब्द **घटना** हो। [घटना](https://www.merriam-webster.com/dictionary/event) को परिभाषा Merriam-Webster अनुसार "केही कुरा जुन हुन्छ" हो। यो हाम्रो अवस्थालाई पूर्ण रूपमा वर्णन गर्दछ। हामीलाई थाहा छ केही हुनेवाला छ जसको प्रतिक्रिया स्वरूप हामीले केही कोड कार्यान्वयन गर्न चाहन्छौं, तर यो कहिले हुनेछ भन्ने थाहा छैन।

हामीले कार्यान्वयन गर्न चाहेको कोडको खण्डलाई चिन्ह लगाउने तरिका भनेको एउटा function सिर्जना गर्नु हो। [प्रक्रियात्मक प्रोग्रामिङ](https://en.wikipedia.org/wiki/Procedural_programming) मा, function हरूलाई विशेष क्रममा बोलाइन्छ। घटना-आधारित प्रोग्रामिङमा पनि यो सत्य हो। फरक भनेको function हरूलाई **कसरी** बोलाइन्छ भन्ने हो।

घटनाहरू (जस्तै बटन क्लिक, टाइपिङ) ह्यान्डल गर्न, हामी **घटना सुन्नेहरू** (event listeners) दर्ता गर्छौं। घटना सुन्ने function भनेको कुनै घटना घट्न पर्खने र त्यसको प्रतिक्रियामा कार्यान्वयन गर्ने function हो। घटना सुन्नेहरूले UI अपडेट गर्न, सर्भरमा कल गर्न, वा प्रयोगकर्ताको कार्यको प्रतिक्रियामा गर्नुपर्ने अन्य कार्यहरू गर्न सक्छन्। हामी [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) प्रयोग गरेर घटना सुन्ने थप्छौं र कार्यान्वयन गर्न function प्रदान गर्छौं।

> **NOTE:** घटना सुन्नेहरू सिर्जना गर्न धेरै तरिकाहरू छन्। तपाईंले अनाम function हरू प्रयोग गर्न सक्नुहुन्छ, वा नामित function हरू सिर्जना गर्न सक्नुहुन्छ। तपाईंले `click` प्रोपर्टी सेट गर्ने वा `addEventListener` प्रयोग गर्ने जस्ता विभिन्न छोटकरीहरू प्रयोग गर्न सक्नुहुन्छ। हाम्रो अभ्यासमा, हामी `addEventListener` र अनाम function हरूमा केन्द्रित हुनेछौं, किनभने यो वेब विकासकर्ताहरूले सबैभन्दा धेरै प्रयोग गर्ने प्रविधि हो। यो सबैभन्दा लचिलो पनि हो, किनभने `addEventListener` सबै घटनाहरूका लागि काम गर्छ, र घटना नामलाई प्यारामिटरको रूपमा प्रदान गर्न सकिन्छ।

### सामान्य घटनाहरू

एप्लिकेसन बनाउँदा तपाईंले सुन्न सक्ने [दर्जनौं घटना](https://developer.mozilla.org/docs/Web/Events) उपलब्ध छन्। पृष्ठमा प्रयोगकर्ताले गर्ने लगभग सबै कुरा एउटा घटना उठाउँछ, जसले तपाईंलाई उनीहरूले चाहेको अनुभव सुनिश्चित गर्न धेरै शक्ति दिन्छ। सौभाग्यवश, तपाईंलाई सामान्यतया थोरै मात्र घटनाहरू आवश्यक पर्छ। यहाँ केही सामान्य घटनाहरू छन् (जसमा हामीले हाम्रो खेल बनाउँदा प्रयोग गर्ने दुई घटनाहरू पनि समावेश छन्):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): प्रयोगकर्ताले केहीमा क्लिक गरे, सामान्यतया बटन वा हाइपरलिंक
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): प्रयोगकर्ताले दायाँ माउस बटन क्लिक गरे
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): प्रयोगकर्ताले केही पाठ चयन गरे
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): प्रयोगकर्ताले केही पाठ इनपुट गरे

## खेल बनाउने

हामी घटनाहरू कसरी काम गर्छन् भनेर बुझ्न खेल बनाउनेछौं। हाम्रो खेलले खेलाडीको टाइपिङ सीप परीक्षण गर्नेछ, जुन सबै विकासकर्ताहरूले अभ्यास गर्नुपर्ने सबैभन्दा कम मूल्याङ्कन गरिएको सीप हो। खेलको सामान्य प्रवाह यस प्रकार हुनेछ:

- खेलाडीले स्टार्ट बटनमा क्लिक गर्छ र टाइप गर्नको लागि एउटा उद्धरण देखाइन्छ
- खेलाडीले उद्धरण सकेसम्म छिटो टाइप गर्छ
  - प्रत्येक शब्द पूरा हुँदा, अर्को शब्द हाइलाइट हुन्छ
  - यदि खेलाडीले टाइपो गर्छ भने, टेक्स्टबक्स रातो हुन्छ
  - खेलाडीले उद्धरण पूरा गरेपछि, सफलताको सन्देश र समय देखाइन्छ

आउनुहोस्, खेल बनाऔं र घटनाहरूको बारेमा सिकौं!

### फाइल संरचना

हामीलाई जम्मा तीनवटा फाइलहरू चाहिन्छ: **index.html**, **script.js**, र **style.css**। यी सेटअप गरेर सुरु गरौं।

- कन्सोल वा टर्मिनल विन्डो खोल्नुहोस् र निम्न आदेश जारी गरेर आफ्नो कामको लागि नयाँ फोल्डर बनाउनुहोस्:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- Visual Studio Code खोल्नुहोस्

```bash
code .
```

- Visual Studio Code मा फोल्डरमा निम्न नामका तीन फाइलहरू थप्नुहोस्:
  - index.html
  - script.js
  - style.css

## प्रयोगकर्ता इन्टरफेस बनाउनुहोस्

आवश्यकताहरू हेर्दा, हामीलाई HTML पृष्ठमा केही तत्वहरू चाहिन्छ। यो एक प्रकारको रेसिपी जस्तै हो, जहाँ हामीलाई केही सामग्रीहरू चाहिन्छ:

- प्रयोगकर्ताले टाइप गर्न उद्धरण देखाउने ठाउँ
- सन्देशहरू (जस्तै सफलताको सन्देश) देखाउने ठाउँ
- टाइप गर्नको लागि टेक्स्टबक्स
- स्टार्ट बटन

यी प्रत्येकलाई ID दिनु आवश्यक छ ताकि हामी तिनीहरूसँग JavaScript मा काम गर्न सकौं। हामी CSS र JavaScript फाइलहरूको सन्दर्भ पनि थप्नेछौं।

**index.html** नामको नयाँ फाइल बनाउनुहोस्। निम्न HTML थप्नुहोस्:

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

### एप्लिकेसन सुरु गर्नुहोस्

सधैं राम्रो हुन्छ कि विकास गर्दा क्रमिक रूपमा हेर्ने कि चीजहरू कस्तो देखिन्छ। हाम्रो एप्लिकेसन सुरु गरौं। Visual Studio Code को लागि [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) नामक उत्कृष्ट एक्सटेन्सन छ, जसले तपाईंको एप्लिकेसनलाई स्थानीय रूपमा होस्ट गर्नेछ र तपाईंले फाइल सेभ गर्दा ब्राउजरलाई रिफ्रेस गर्नेछ।

- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) इन्स्टल गर्नुहोस्
  - ब्राउजरले Visual Studio Code खोल्न अनुरोध गर्नेछ, त्यसपछि Visual Studio Code ले इन्स्टलेसन गर्न अनुमति माग्नेछ
  - आवश्यक परे Visual Studio Code पुनः सुरु गर्नुहोस्
- इन्स्टल भएपछि, Visual Studio Code मा Ctrl-Shift-P (वा Cmd-Shift-P) थिचेर कमाण्ड प्यालेट खोल्नुहोस्
- **Live Server: Open with Live Server** टाइप गर्नुहोस्
  - Live Server ले तपाईंको एप्लिकेसन होस्ट गर्न सुरु गर्नेछ
- ब्राउजर खोल्नुहोस् र **https://localhost:5500** मा जानुहोस्
- तपाईंले बनाएको पृष्ठ देखिनु पर्नेछ!

अब केही कार्यक्षमता थपौं।

## CSS थप्नुहोस्

HTML तयार भएपछि, कोर स्टाइलिङका लागि CSS थपौं। हामीले खेलाडीले टाइप गर्नुपर्ने शब्दलाई हाइलाइट गर्न र गलत टाइप गर्दा टेक्स्टबक्सलाई रंगीन बनाउन दुईवटा कक्षाहरू प्रयोग गर्नेछौं।

**style.css** नामको नयाँ फाइल बनाउनुहोस् र निम्न CSS थप्नुहोस्:

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

✅ CSS को कुरा गर्दा तपाईं आफ्नो पृष्ठलाई मनपर्ने तरिकाले लेआउट गर्न सक्नुहुन्छ। पृष्ठलाई अझ आकर्षक बनाउन केही समय लिनुहोस्:

- फरक फन्ट छान्नुहोस्
- हेडरहरूलाई रंगीन बनाउनुहोस्
- वस्तुहरूको आकार परिवर्तन गर्नुहोस्

## JavaScript

UI तयार भएपछि, अब हाम्रो ध्यान JavaScript मा केन्द्रित गरौं, जसले तार्किक पक्ष प्रदान गर्नेछ। हामी यसलाई केही चरणहरूमा तोड्नेछौं:

- [Constants बनाउनुहोस्](../../../../4-typing-game/typing-game)
- [खेल सुरु गर्ने Event Listener](../../../../4-typing-game/typing-game)
- [टाइपिङको Event Listener](../../../../4-typing-game/typing-game)

तर पहिले, **script.js** नामको नयाँ फाइल बनाउनुहोस्।

### Constants बनाउनुहोस्

हामीलाई प्रोग्रामिङलाई सजिलो बनाउन केही वस्तुहरू चाहिन्छ। यो पनि रेसिपी जस्तै हो, जहाँ हामीलाई चाहिने सामग्रीहरू यस्ता छन्:

- उद्धरणहरूको सूची भएको array
- हालको उद्धरणका सबै शब्दहरू भण्डारण गर्न खाली array
- खेलाडीले हाल टाइप गरिरहेको शब्दको सूचकांक भण्डारण गर्ने ठाउँ
- खेलाडीले स्टार्ट क्लिक गरेको समय

हामीलाई UI तत्वहरूको सन्दर्भ पनि चाहिन्छ:

- टेक्स्टबक्स (**typed-value**)
- उद्धरण प्रदर्शन (**quote**)
- सन्देश (**message**)

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

✅ आफ्नो खेलमा थप उद्धरणहरू थप्नुहोस्

> **NOTE:** हामी `document.getElementById` प्रयोग गरेर कोडमा जबसुकै तत्वहरू पुनः प्राप्त गर्न सक्छौं। तर, यी तत्वहरूलाई बारम्बार सन्दर्भ गर्ने भएकाले, स्ट्रिङ लिटेरलहरूमा टाइपोबाट बच्न Constants प्रयोग गर्नेछौं। [Vue.js](https://vuejs.org/) वा [React](https://reactjs.org/) जस्ता फ्रेमवर्कहरूले तपाईंलाई कोडलाई केन्द्रित गर्न मद्दत गर्न सक्छ।

`const`, `let` र `var` प्रयोग गर्नेबारे भिडियो हेर्न एक मिनेट समय लिनुहोस्:

[![भिन्न प्रकारका भेरिएबलहरू](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "भिन्न प्रकारका भेरिएबलहरू")

> 🎥 माथिको तस्बिरमा क्लिक गरेर भेरिएबलहरूको बारेमा भिडियो हेर्नुहोस्।

### सुरु गर्ने तर्क थप्नुहोस्

खेल सुरु गर्न, खेलाडीले स्टार्टमा क्लिक गर्नेछ। तर, उनीहरूले कहिले क्लिक गर्नेछन् भन्ने हामीलाई थाहा छैन। यस्तै अवस्थामा [घटना सुन्ने](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) काममा आउँछ। घटना सुन्नेले कुनै कुरा (घटना) घट्न पर्खने र त्यसको प्रतिक्रियामा कोड कार्यान्वयन गर्ने अनुमति दिन्छ। हाम्रो अवस्थामा, प्रयोगकर्ताले स्टार्ट क्लिक गर्दा कोड कार्यान्वयन गर्न चाहन्छौं।

जब प्रयोगकर्ताले **स्टार्ट** क्लिक गर्छ, हामीले उद्धरण चयन गर्न, UI सेटअप गर्न, र हालको शब्द र समय ट्र्याक गर्न आवश्यक छ। तल JavaScript दिइएको छ; हामी यसलाई स्क्रिप्ट ब्लकपछि छलफल गर्नेछौं।

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

कोडलाई तोडेर बुझौं:

- शब्द ट्र्याकिङ सेटअप गर्नुहोस्
  - [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) र [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) प्रयोग गरेर `quotes` array बाट र्यान्डम उद्धरण चयन गर्नुहोस्
  - `quote` लाई `words` array मा रूपान्तरण गर्नुहोस् ताकि खेलाडीले हाल टाइप गरिरहेको शब्द ट्र्याक गर्न सकियोस्
  - `wordIndex` लाई 0 मा सेट गर्नुहोस्, किनभने खेलाडी पहिलो शब्दबाट सुरु गर्नेछ
- UI सेटअप गर्नुहोस्
  - `spanWords` को array बनाउनुहोस्, जसमा प्रत्येक शब्द `span` तत्वभित्र हुन्छ
    - यसले प्रदर्शनमा शब्दलाई हाइलाइट गर्न अनुमति दिनेछ
  - array लाई `join` गरेर string बनाउनुहोस्, जसलाई `quoteElement` को `innerHTML` अपडेट गर्न प्रयोग गर्न सकिन्छ
    - यसले खेलाडीलाई उद्धरण देखाउनेछ
  - पहिलो `span` तत्वको `className` लाई `highlight` मा सेट गर्नुहोस् ताकि यो पहेंलो हाइलाइट होस्
  - `messageElement` लाई सफा गर्न `innerText` लाई `''` मा सेट गर्नुहोस्
- टेक्स्टबक्स सेटअप गर्नुहोस्
  - `typedValueElement` मा हालको `value` सफा गर्नुहोस्
  - `typedValueElement` मा `focus` सेट गर्नुहोस्
- टाइमर सुरु गर्न `getTime` कल गर्नुहोस्

### टाइपिङ तर्क थप्नुहोस्

जब खेलाडीले टाइप गर्छ, `input` घटना उठ्छ। यो घटना सुन्नेले खेलाडीले शब्द सही टाइप गरिरहेको छ कि छैन जाँच गर्नेछ, र खेलको हालको स्थिति ह्यान्डल गर्नेछ। **script.js** मा, तलको कोड अन्त्यमा थप्नुहोस्। हामी यसलाई पछि तोड्नेछौं।

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

कोडलाई तोडेर बुझौं! हामीले हालको शब्द र खेलाडीले अहिलेसम्म टाइप गरेको मान प्राप्त गर्छौं। त्यसपछि, हामी वॉटरफॉल तर्क प्रयोग गर्छौं, जहाँ हामी जाँच गर्छौं कि उद्धरण पूरा भयो, शब्द पूरा भयो, शब्द सही छ, वा (अन्तमा) त्रुटि छ।

- उद्धरण पूरा भयो, `typedValue` `currentWord` बराबर छ, र `wordIndex` `words` को `length` भन्दा एक कम छ
  - `startTime` बाट हालको समय घटाएर `elapsedTime` गणना गर्नुहोस्
  - `elapsedTime` लाई 1,000 ले भाग गरेर मिलिसेकेन्डलाई सेकेन्डमा रूपान्तरण गर्नुहोस्
  - सफलताको सन्देश प्रदर्शन गर्नुहोस्
- शब्द पूरा भयो, `typedValue` ले स्पेसमा अन्त्य हुन्छ (शब्दको अन्त्य) र `typedValue` `currentWord` बराबर छ
  - `typedElement` मा `value` लाई `''` मा सेट गर्नुहोस् ताकि अर्को शब्द टाइप गर्न सकियोस्
  - `wordIndex` लाई इन्क्रिमेन्ट गर्नुहोस् ताकि अर्को शब्दमा जाओस्
  - `quoteElement` का सबै `childNodes` मा `className` लाई `''` मा सेट गर्नुहोस् ताकि यो डिफल्ट प्रदर्शनमा फर्कियोस्
  - हालको शब्दको `className` लाई `highlight` मा सेट गर्नुहोस् ताकि यो अर्को टाइप गर्नुपर्ने शब्द होस्
- शब्द हाल सही टाइप भइरहेको छ (तर पूरा भएको छैन), `currentWord` `typedValue` बाट सुरु हुन्छ
  - `typedValueElement` लाई डिफल्टमा प्रदर्शन गर्न सुनिश्चित गर्नुहोस्, `className` सफा गरेर
- यदि हामी यहाँसम्म आइपुग्यौं भने, त्रुटि छ
  - `typedValueElement` मा `className` लाई `error` मा सेट गर्नुहोस्

## आफ्नो एप्लिकेसन परीक्षण गर्नुहोस्

तपाईं अन्त्यसम्म आइपुग्नुभयो! अन्तिम चरण भनेको हाम्रो एप्लिकेसन काम गर्छ कि छैन सुनिश्चित गर्नु हो। प्रयास गर्नुहोस्! यदि त्रुटिहरू छन् भने चिन्ता नगर्नुहोस्; **सबै विकासकर्ताहरू** ले त्रुटिहरू सामना गर्छन्। सन्देशहरू जाँच गर्नुहोस् र आवश्यक परे डिबग गर्नुहोस्।

**स्टार्ट** मा क्लिक गर्नुहोस्, र टाइप गर्न सुरु गर्नुहोस्! यो तलको एनिमेसन जस्तै देखिनु पर्छ।

![खेलको एनिमेसन](../../../../4-typing-game/images/demo.gif)

---

## 🚀 चुनौती

थप कार्यक्षमता थप्नुहोस्

- उद्धरण पूरा भएपछि `input` घटना सुन्नेलाई निष्क्रिय गर्नुहोस्, र बटन क्लिक गर्दा पुनः सक्रिय गर्नुहोस्
- खेलाडीले उद्धरण पूरा गरेपछि टेक्स्टबक्स निष्क्रिय गर्नुहोस्
- सफलताको सन्देशसहितको मोडल डाइलग बक्स प्रदर्शन गर्नुहोस्
- उच्च स्कोरहरू [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) प्रयोग गरेर भण्डारण गर्नुहोस्

## पोस्ट-व्याख्यान क्विज

[पोस्ट-व्याख्यान क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/22)

## समीक्षा र आत्म-अध्ययन

वेब ब्राउजरमार्फत विकासकर्तालाई उपलब्ध [सबै घटनाहरू](https://developer.mozilla.org/docs/Web/Events) को बारेमा पढ्नुहोस्, र प्रत्येक घटनालाई प्रयोग गर्न सकिने परिदृश्यहरूको बारेमा विचार गर्नुहोस्।

## असाइनमेन्ट

[नयाँ किबोर्ड खेल सिर्जना गर्नुहोस्](assignment.md)

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।