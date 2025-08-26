<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e982871b8388c59c22a41b73b5fca70f",
  "translation_date": "2025-08-26T01:04:19+00:00",
  "source_file": "4-typing-game/typing-game/README.md",
  "language_code": "mr"
}
-->
# इव्हेंट्स वापरून गेम तयार करणे

## प्री-लेक्चर क्विझ

[प्री-लेक्चर क्विझ](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/21)

## इव्हेंट-ड्रिव्हन प्रोग्रामिंग

ब्राउझर आधारित अॅप्लिकेशन तयार करताना, आपण वापरकर्त्याला आपल्याने तयार केलेल्या गोष्टींशी संवाद साधण्यासाठी ग्राफिकल यूजर इंटरफेस (GUI) प्रदान करतो. ब्राउझरशी संवाद साधण्याचा सर्वात सामान्य मार्ग म्हणजे विविध घटकांवर क्लिक करणे आणि टाइप करणे. एक विकसक म्हणून आपल्याला आव्हान हे आहे की, वापरकर्ता हे ऑपरेशन कधी करेल हे आपल्याला माहित नसते!

[इव्हेंट-ड्रिव्हन प्रोग्रामिंग](https://en.wikipedia.org/wiki/Event-driven_programming) ही आपल्याला GUI तयार करण्यासाठी आवश्यक असलेल्या प्रोग्रामिंग प्रकाराचे नाव आहे. जर आपण या वाक्यांशाचे थोडेसे विश्लेषण केले तर आपल्याला मुख्य शब्द **इव्हेंट** दिसतो. [इव्हेंट](https://www.merriam-webster.com/dictionary/event) म्हणजे "काहीतरी जे घडते". ही व्याख्या आपल्या परिस्थितीला अगदी योग्य प्रकारे वर्णन करते. आपल्याला माहित आहे की काहीतरी घडणार आहे ज्यासाठी आपल्याला प्रतिसाद म्हणून काही कोड अंमलात आणायचा आहे, परंतु ते कधी घडेल हे आपल्याला माहित नाही.

आपण अंमलात आणू इच्छित असलेल्या कोडच्या विभागाला चिन्हांकित करण्याचा मार्ग म्हणजे फंक्शन तयार करणे. [प्रोसीजरल प्रोग्रामिंग](https://en.wikipedia.org/wiki/Procedural_programming) विचारात घेतल्यास, फंक्शन्स विशिष्ट क्रमाने कॉल केल्या जातात. इव्हेंट-ड्रिव्हन प्रोग्रामिंगसाठीही हेच खरे आहे. फरक फक्त **कसा** फंक्शन्स कॉल केले जातात यामध्ये आहे.

इव्हेंट्स (बटण क्लिक करणे, टाइप करणे, इ.) हाताळण्यासाठी, आपण **इव्हेंट लिसनर्स** नोंदवतो. इव्हेंट लिसनर म्हणजे एक फंक्शन जे इव्हेंट घडण्याची वाट पाहते आणि प्रतिसाद म्हणून अंमलात आणते. इव्हेंट लिसनर्स UI अपडेट करू शकतात, सर्व्हरला कॉल करू शकतात किंवा वापरकर्त्याच्या कृतीच्या प्रतिसादात जे काही करणे आवश्यक आहे ते करू शकतात. आपण [addEventListener](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) वापरून इव्हेंट लिसनर जोडतो आणि अंमलात आणण्यासाठी फंक्शन प्रदान करतो.

> **NOTE:** इव्हेंट लिसनर्स तयार करण्याचे अनेक मार्ग आहेत हे लक्षात घेण्यासारखे आहे. आपण अज्ञात फंक्शन्स वापरू शकता किंवा नाव दिलेल्या फंक्शन्स तयार करू शकता. आपण `click` प्रॉपर्टी सेट करणे किंवा `addEventListener` वापरणे यासारख्या विविध शॉर्टकट्स वापरू शकता. आपल्या सरावामध्ये आपण `addEventListener` आणि अज्ञात फंक्शन्सवर लक्ष केंद्रित करणार आहोत, कारण वेब डेव्हलपर्स सर्वात सामान्यतः ही तंत्रे वापरतात. हे सर्वात लवचिक आहे, कारण `addEventListener` सर्व इव्हेंट्ससाठी कार्य करते आणि इव्हेंटचे नाव पॅरामीटर म्हणून प्रदान केले जाऊ शकते.

### सामान्य इव्हेंट्स

[डझनभर इव्हेंट्स](https://developer.mozilla.org/docs/Web/Events) उपलब्ध आहेत जेव्हा आपण अॅप्लिकेशन तयार करतो तेव्हा आपण त्यांचा वापर करू शकतो. वापरकर्ता पृष्ठावर जे काही करतो ते इव्हेंट निर्माण करते, ज्यामुळे आपल्याला त्यांना हवे असलेले अनुभव देण्यासाठी खूप ताकद मिळते. सुदैवाने, आपल्याला सामान्यतः फक्त काही इव्हेंट्सची आवश्यकता असते. येथे काही सामान्य इव्हेंट्स दिले आहेत (ज्यामध्ये आपण गेम तयार करताना वापरणार आहोत):

- [click](https://developer.mozilla.org/docs/Web/API/Element/click_event): वापरकर्त्याने काहीतरी क्लिक केले, सामान्यतः बटण किंवा हायपरलिंक
- [contextmenu](https://developer.mozilla.org/docs/Web/API/Element/contextmenu_event): वापरकर्त्याने उजव्या माऊस बटणावर क्लिक केले
- [select](https://developer.mozilla.org/docs/Web/API/Element/select_event): वापरकर्त्याने काही मजकूर हायलाइट केला
- [input](https://developer.mozilla.org/docs/Web/API/Element/input_event): वापरकर्त्याने काही मजकूर टाइप केला

## गेम तयार करणे

आता आपण इव्हेंट्स जावास्क्रिप्टमध्ये कसे कार्य करतात हे शोधण्यासाठी एक गेम तयार करणार आहोत. आपला गेम खेळाडूच्या टाइपिंग कौशल्याची चाचणी घेणार आहे, जे सर्व डेव्हलपर्ससाठी एक अत्यंत उपेक्षित कौशल्य आहे. आपल्याला नेहमीच टाइपिंगचा सराव करायला हवा! गेमचा सामान्य प्रवाह असा असेल:

- खेळाडू **start** बटणावर क्लिक करतो आणि टाइप करण्यासाठी एक कोट दिला जातो
- खेळाडू कोट जितक्या लवकर शक्य असेल तितक्या लवकर टाइप करतो
  - प्रत्येक शब्द पूर्ण झाल्यावर पुढील शब्द हायलाइट केला जातो
  - जर खेळाडूने टायपो केला तर टेक्स्टबॉक्स लाल रंगात अपडेट होतो
  - खेळाडू कोट पूर्ण केल्यावर यशस्वी संदेश आणि लागलेला वेळ दाखवला जातो

चला आपला गेम तयार करूया आणि इव्हेंट्सबद्दल शिकूया!

### फाइल स्ट्रक्चर

आपल्याला एकूण तीन फाइल्सची आवश्यकता आहे: **index.html**, **script.js** आणि **style.css**. चला त्या सेटअप करूया जेणेकरून आपले काम सोपे होईल.

- एक नवीन फोल्डर तयार करा. कन्सोल किंवा टर्मिनल विंडो उघडा आणि खालील कमांड टाइप करा:

```bash
# Linux or macOS
mkdir typing-game && cd typing-game

# Windows
md typing-game && cd typing-game
```

- व्हिज्युअल स्टुडिओ कोड उघडा

```bash
code .
```

- व्हिज्युअल स्टुडिओ कोडमध्ये फोल्डरमध्ये खालील नावांच्या तीन फाइल्स जोडा:
  - index.html
  - script.js
  - style.css

## यूजर इंटरफेस तयार करा

आपल्या गरजांचा विचार केल्यास, आपल्याला HTML पृष्ठावर काही घटकांची आवश्यकता आहे. हे जसे एखाद्या रेसिपीसारखे आहे, जिथे आपल्याला काही साहित्य लागते:

- वापरकर्त्याला टाइप करण्यासाठी कोट दाखवण्यासाठी जागा
- यशस्वी संदेशासारखे कोणतेही संदेश दाखवण्यासाठी जागा
- टाइप करण्यासाठी टेक्स्टबॉक्स
- **start** बटण

प्रत्येक घटकाला IDs असणे आवश्यक आहे जेणेकरून आपण त्यांच्याशी जावास्क्रिप्टमध्ये काम करू शकू. आपण तयार करणार असलेल्या CSS आणि जावास्क्रिप्ट फाइल्ससाठी संदर्भ देखील जोडूया.

एक नवीन फाइल तयार करा ज्याचे नाव **index.html** असे ठेवा. खालील HTML जोडा:

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

### अॅप्लिकेशन लाँच करा

नेहमीच पुनरावृत्तीने विकसित करणे चांगले असते जेणेकरून गोष्टी कशा दिसतात हे पाहता येईल. आपले अॅप्लिकेशन लाँच करूया. व्हिज्युअल स्टुडिओ कोडसाठी [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) नावाचा एक उत्कृष्ट एक्सटेंशन आहे जो आपले अॅप्लिकेशन स्थानिक पातळीवर होस्ट करतो आणि प्रत्येक वेळी आपण सेव्ह केल्यावर ब्राउझर रीफ्रेश करतो.

- [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer&WT.mc_id=academic-77807-sagibbon) इंस्टॉल करा. लिंकवर क्लिक करा आणि **Install** बटणावर क्लिक करा.
  - ब्राउझर आपल्याला व्हिज्युअल स्टुडिओ कोड उघडण्यास सांगेल, त्यानंतर व्हिज्युअल स्टुडिओ कोड आपल्याला इंस्टॉलेशन करण्यास सांगेल.
  - जर विचारले गेले तर व्हिज्युअल स्टुडिओ कोड रीस्टार्ट करा.
- इंस्टॉल झाल्यानंतर, व्हिज्युअल स्टुडिओ कोडमध्ये Ctrl-Shift-P (किंवा Cmd-Shift-P) क्लिक करा जेणेकरून कमांड पॅलेट उघडेल.
- **Live Server: Open with Live Server** टाइप करा.
  - Live Server आपले अॅप्लिकेशन होस्ट करणे सुरू करेल.
- ब्राउझर उघडा आणि **https://localhost:5500** वर जा.
- आता आपण तयार केलेले पृष्ठ पाहू शकता!

चला काही फंक्शनॅलिटी जोडूया.

## CSS जोडा

आपले HTML तयार झाल्यानंतर, आता कोर स्टाइलिंगसाठी CSS जोडा. आपल्याला खेळाडूने टाइप करायचा शब्द हायलाइट करायचा आहे आणि त्यांनी चुकीचे टाइप केल्यास टेक्स्टबॉक्स रंगवायचा आहे. आपण हे दोन क्लासेससह करू.

एक नवीन फाइल तयार करा ज्याचे नाव **style.css** असे ठेवा आणि खालील सिंटॅक्स जोडा.

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

✅ CSS बाबतीत आपण आपले पृष्ठ कसेही लेआउट करू शकता. थोडा वेळ घ्या आणि पृष्ठ अधिक आकर्षक बनवा:

- वेगळा फॉन्ट निवडा
- हेडर्स रंगवा
- आयटम्सचा आकार बदला

## जावास्क्रिप्ट

आपले UI तयार झाल्यानंतर, आता आपण जावास्क्रिप्टवर लक्ष केंद्रित करूया जी लॉजिक प्रदान करेल. आपण हे काही चरणांमध्ये विभागणार आहोत:

- [कॉन्स्टंट्स तयार करा](../../../../4-typing-game/typing-game)
- [गेम सुरू करण्यासाठी इव्हेंट लिसनर](../../../../4-typing-game/typing-game)
- [टाइपिंगसाठी इव्हेंट लिसनर](../../../../4-typing-game/typing-game)

पण आधी, एक नवीन फाइल तयार करा ज्याचे नाव **script.js** असे ठेवा.

### कॉन्स्टंट्स जोडा

आपले प्रोग्रामिंग सोपे करण्यासाठी आपल्याला काही आयटम्सची आवश्यकता आहे. पुन्हा, एखाद्या रेसिपीसारखे, आपल्याला याची आवश्यकता आहे:

- सर्व कोट्सची यादी असलेली अॅरे
- सध्याच्या कोटसाठी सर्व शब्द साठवण्यासाठी रिकामी अॅरे
- खेळाडू सध्या टाइप करत असलेल्या शब्दाचा इंडेक्स साठवण्यासाठी जागा
- खेळाडूने **start** क्लिक केलेला वेळ

आपल्याला UI घटकांचे संदर्भ देखील हवे आहेत:

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

✅ आपल्या गेममध्ये अधिक कोट्स जोडा

> **NOTE:** आपण `document.getElementById` वापरून कोडमध्ये कधीही घटक मिळवू शकतो. कारण आपण नियमितपणे या घटकांचा संदर्भ घेणार आहोत, आपण स्ट्रिंग लिटरल्समध्ये टायपो टाळण्यासाठी कॉन्स्टंट्स वापरणार आहोत. [Vue.js](https://vuejs.org/) किंवा [React](https://reactjs.org/) सारखी फ्रेमवर्क्स आपल्याला आपला कोड अधिक चांगल्या प्रकारे केंद्रीकृत करण्यास मदत करू शकतात.

`const`, `let` आणि `var` वापरण्याबद्दल एक व्हिडिओ पाहण्यासाठी थोडा वेळ घ्या.

[![व्हेरिएबल्सचे प्रकार](https://img.youtube.com/vi/JNIXfGiDWM8/0.jpg)](https://youtube.com/watch?v=JNIXfGiDWM8 "व्हेरिएबल्सचे प्रकार")

> 🎥 वरील प्रतिमेवर क्लिक करा आणि व्हेरिएबल्सबद्दल व्हिडिओ पहा.

### सुरू करण्याचे लॉजिक जोडा

गेम सुरू करण्यासाठी, खेळाडू **start** क्लिक करेल. अर्थात, ते कधी क्लिक करतील हे आपल्याला माहित नाही. येथे [इव्हेंट लिसनर](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener) उपयोगी पडतो. इव्हेंट लिसनर आपल्याला काहीतरी घडण्याची (इव्हेंट) वाट पाहण्याची आणि प्रतिसाद म्हणून कोड अंमलात आणण्याची परवानगी देतो. आपल्या बाबतीत, वापरकर्त्याने **start** क्लिक केल्यावर कोड अंमलात आणायचा आहे.

जेव्हा वापरकर्ता **start** क्लिक करतो, तेव्हा आपल्याला एक कोट निवडायचा आहे, यूजर इंटरफेस सेटअप करायचा आहे आणि सध्याच्या शब्दासाठी आणि टाइमिंगसाठी ट्रॅकिंग सेट करायचे आहे. खाली आपल्याला आवश्यक जावास्क्रिप्ट दिली आहे; आम्ही स्क्रिप्ट ब्लॉकनंतर त्यावर चर्चा करतो.

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

चला कोड समजून घेऊया!

- शब्द ट्रॅकिंग सेटअप करा
  - [Math.floor](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) आणि [Math.random](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math/random) वापरून आपण `quotes` अॅरेमधून एक कोट निवडतो
  - `quote` ला `words` अॅरेमध्ये रूपांतरित करतो जेणेकरून आपण खेळाडू सध्या टाइप करत असलेल्या शब्दाचा ट्रॅक ठेवू शकतो
  - `wordIndex` 0 वर सेट करतो, कारण खेळाडू पहिल्या शब्दावर सुरू करेल
- UI सेटअप करा
  - `spanWords` अॅरे तयार करतो, ज्यामध्ये प्रत्येक शब्द `span` घटकात असतो
    - हे आपल्याला डिस्प्लेवरील शब्द हायलाइट करण्यास अनुमती देते
  - `join` अॅरे वापरून एक स्ट्रिंग तयार करतो ज्याचा उपयोग `quoteElement` च्या `innerHTML` अपडेट करण्यासाठी करतो
    - हे खेळाडूला कोट दाखवते
  - पहिल्या `span` घटकाचा `className` `highlight` सेट करतो जेणेकरून तो पिवळा हायलाइट होईल
  - `messageElement` साफ करतो आणि त्याचा `innerText` `''` सेट करतो
- टेक्स्टबॉक्स सेटअप करा
  - `typedValueElement` चा सध्याचा `value` साफ करतो
  - `typedValueElement` वर `focus` सेट करतो
- `getTime` कॉल करून टाइमर सुरू करतो

### टाइपिंग लॉजिक जोडा

जेव्हा खेळाडू टाइप करतो, तेव्हा `input` इव्हेंट उघड होतो. हा इव्हेंट लिसनर खेळाडू योग्य शब्द टाइप करत आहे याची खात्री करतो आणि गेमची सध्याची स्थिती हाताळतो. **script.js** मध्ये परत जा आणि खालील कोड शेवटी जोडा. त्यानंतर आपण त्याचे विश्लेषण करू.

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

चला कोड समजून घेऊया! आपण सध्याचा शब्द आणि खेळाडूने आतापर्यंत टाइप केलेले मूल्य घेतो. त्यानंतर आपल्याकडे वॉटरफॉल लॉजिक आहे, जिथे आपण तपासतो की कोट पूर्ण आहे, शब्द पूर्ण आहे, शब्द योग्य आहे किंवा (शेवटी) काहीतरी चूक आहे.

- कोट पूर्ण आहे, हे `typedValue` `currentWord` च्या समान असल्याने आणि `wordIndex` `words` च्या `length` पेक्षा एक कमी असल्याने सूचित होते
  - `elapsedTime` काढतो, `startTime` मधून सध्याचा वेळ वजा करून
  - `elapsedTime` ला 1,000 ने भाग देतो जेणेकरून मिलिसेकंद सेकंदात रूपांतरित होईल
  - यशस्वी संदेश दाखवतो
- शब्द पूर्ण आहे, हे `typedValue` स्पेसने संपते (शब्दाचा शेवट) आणि `typedValue` `currentWord` च्या समान असल्याने सूचित होते
  - पुढील शब्द टाइप करण्यासाठी `typedElement` चा `value` `''` सेट करतो
  - पुढील शब्दावर जाण्यासाठी `wordIndex` वाढवतो
  - `quoteElement` च्या सर्व `childNodes` लूप करतो आणि त्यांचा `className` `''` सेट करतो जेणेकरून तो डीफॉल्ट डिस्प्लेवर परत जाईल
  - सध्याच्या शब्दाचा `className` `highlight` सेट करतो जेणेकरून तो पुढील टाइप करण्याचा शब्द म्हणून फ्लॅग होईल
- शब्द सध्या योग्य प्रकारे टाइप केला जात आहे (पण पूर्ण नाही), हे `currentWord` `typedValue` ने सुरू होत असल्याने सूचित होते
  - `typedValueElement` डीफॉल्ट डिस्प्लेवर असल्याचे सुनिश्चित करतो, `className` साफ करून
- जर आपण येथे पोहोचलो, तर आपल्याकडे एक चूक आहे
  - `typedValueElement` चा `className` `error` सेट करतो

## आप
- [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) वापरून उच्च स्कोअर जतन करा

## व्याख्यानानंतरचा क्विझ

[व्याख्यानानंतरचा क्विझ](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/22)

## पुनरावलोकन आणि स्व-अभ्यास

वेब ब्राउझरद्वारे डेव्हलपरसाठी उपलब्ध असलेल्या [सर्व इव्हेंट्स](https://developer.mozilla.org/docs/Web/Events) बद्दल वाचा आणि प्रत्येक इव्हेंट कोणत्या परिस्थितीत वापरला जाईल याचा विचार करा.

## असाइनमेंट

[नवीन कीबोर्ड गेम तयार करा](assignment.md)

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.