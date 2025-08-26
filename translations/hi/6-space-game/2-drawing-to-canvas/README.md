<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "41be8d35e7f30aa9dad10773c35e89c4",
  "translation_date": "2025-08-24T12:35:01+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "hi"
}
-->
# स्पेस गेम बनाएं भाग 2: हीरो और मॉन्स्टर्स को कैनवास पर ड्रॉ करें

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/31)

## कैनवास

कैनवास एक HTML एलिमेंट है जो डिफ़ॉल्ट रूप से खाली होता है; यह एक खाली स्लेट की तरह है। आपको इस पर ड्रॉ करके सामग्री जोड़नी होती है।

✅ [कैनवास API के बारे में अधिक पढ़ें](https://developer.mozilla.org/docs/Web/API/Canvas_API) MDN पर।

यह आमतौर पर पेज के बॉडी के हिस्से के रूप में इस तरह घोषित किया जाता है:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

ऊपर हम `id`, `width` और `height` सेट कर रहे हैं।

- `id`: इसे सेट करें ताकि जब आपको इसके साथ इंटरैक्ट करना हो तो इसका रेफरेंस प्राप्त कर सकें।
- `width`: यह एलिमेंट की चौड़ाई है।
- `height`: यह एलिमेंट की ऊंचाई है।

## सरल ज्यामिति ड्रॉ करना

कैनवास चीजों को ड्रॉ करने के लिए एक कार्टेशियन कोऑर्डिनेट सिस्टम का उपयोग करता है। इसलिए यह x-अक्ष और y-अक्ष का उपयोग करता है यह व्यक्त करने के लिए कि कुछ कहाँ स्थित है। लोकेशन `0,0` टॉप लेफ्ट पोजिशन है और बॉटम राइट वह है जिसे आपने कैनवास की चौड़ाई और ऊंचाई के रूप में सेट किया है।

![कैनवास का ग्रिड](../../../../6-space-game/2-drawing-to-canvas/canvas_grid.png)
> छवि [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes) से

कैनवास एलिमेंट पर ड्रॉ करने के लिए आपको निम्नलिखित चरणों से गुजरना होगा:

1. **रेफरेंस प्राप्त करें** कैनवास एलिमेंट का।
1. **रेफरेंस प्राप्त करें** उस कॉन्टेक्स्ट एलिमेंट का जो कैनवास एलिमेंट पर बैठता है।
1. **ड्रॉइंग ऑपरेशन करें** कॉन्टेक्स्ट एलिमेंट का उपयोग करके।

ऊपर दिए गए चरणों के लिए कोड आमतौर पर इस तरह दिखता है:

```javascript
// draws a red rectangle
//1. get the canvas reference
canvas = document.getElementById("myCanvas");

//2. set the context to 2D to draw basic shapes
ctx = canvas.getContext("2d");

//3. fill it with the color red
ctx.fillStyle = 'red';

//4. and draw a rectangle with these parameters, setting location and size
ctx.fillRect(0,0, 200, 200) // x,y,width, height
```

✅ कैनवास API मुख्य रूप से 2D शेप्स पर केंद्रित है, लेकिन आप वेब साइट पर 3D एलिमेंट भी ड्रॉ कर सकते हैं; इसके लिए आप [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) का उपयोग कर सकते हैं।

आप कैनवास API के साथ कई प्रकार की चीजें ड्रॉ कर सकते हैं जैसे:

- **ज्यामितीय आकृतियाँ**, हमने पहले ही दिखाया है कि आयत कैसे ड्रॉ करें, लेकिन आप और भी बहुत कुछ ड्रॉ कर सकते हैं।
- **टेक्स्ट**, आप किसी भी फॉन्ट और रंग के साथ टेक्स्ट ड्रॉ कर सकते हैं।
- **इमेजेस**, आप किसी इमेज एसेट जैसे .jpg या .png के आधार पर इमेज ड्रॉ कर सकते हैं।

✅ इसे आज़माएं! आप जानते हैं कि आयत कैसे ड्रॉ करें, क्या आप पेज पर एक सर्कल ड्रॉ कर सकते हैं? CodePen पर कुछ दिलचस्प कैनवास ड्रॉइंग्स देखें। यहाँ एक [विशेष रूप से प्रभावशाली उदाहरण](https://codepen.io/dissimulate/pen/KrAwx) है।

## इमेज एसेट लोड और ड्रॉ करें

आप एक इमेज एसेट को `Image` ऑब्जेक्ट बनाकर और उसकी `src` प्रॉपर्टी सेट करके लोड करते हैं। फिर आप `load` इवेंट को सुनते हैं ताकि यह जान सकें कि इसे उपयोग करने के लिए तैयार है। कोड इस तरह दिखता है:

### एसेट लोड करें

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### एसेट लोड पैटर्न

ऊपर दिए गए को एक संरचना में लपेटने की सिफारिश की जाती है ताकि इसे उपयोग करना आसान हो और आप केवल तभी इसे संशोधित करने का प्रयास करें जब यह पूरी तरह से लोड हो जाए:

```javascript
function loadAsset(path) {
  return new Promise((resolve) => {
    const img = new Image();
    img.src = path;
    img.onload = () => {
      // image loaded and ready to be used
      resolve(img);
    }
  })
}

// use like so

async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')
}

```

गेम एसेट्स को स्क्रीन पर ड्रॉ करने के लिए, आपका कोड इस तरह दिखेगा:

```javascript
async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')

  canvas = document.getElementById("myCanvas");
  ctx = canvas.getContext("2d");
  ctx.drawImage(heroImg, canvas.width/2,canvas.height/2);
  ctx.drawImage(monsterImg, 0,0);
}
```

## अब समय है अपना गेम बनाना शुरू करने का

### क्या बनाना है

आप एक वेब पेज बनाएंगे जिसमें एक कैनवास एलिमेंट होगा। इसे एक काले स्क्रीन `1024*768` पर रेंडर करना चाहिए। हमने आपको दो इमेजेस प्रदान की हैं:

- हीरो शिप

   ![हीरो शिप](../../../../6-space-game/2-drawing-to-canvas/solution/assets/player.png)

- 5*5 मॉन्स्टर

   ![मॉन्स्टर शिप](../../../../6-space-game/2-drawing-to-canvas/solution/assets/enemyShip.png)

### विकास शुरू करने के लिए अनुशंसित चरण

उन फाइल्स को ढूंढें जो आपके लिए `your-work` सब फोल्डर में बनाई गई हैं। इसमें निम्नलिखित शामिल होना चाहिए:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

इस फोल्डर की एक कॉपी को Visual Studio Code में खोलें। आपको एक स्थानीय विकास वातावरण सेटअप करना होगा, अधिमानतः Visual Studio Code के साथ जिसमें NPM और Node इंस्टॉल हो। यदि आपके कंप्यूटर पर `npm` सेटअप नहीं है, तो [यहाँ बताया गया है कि इसे कैसे करें](https://www.npmjs.com/get-npm)।

अपने प्रोजेक्ट को `your_work` फोल्डर पर नेविगेट करके शुरू करें:

```bash
cd your-work
npm start
```

ऊपर दिया गया आपके कंप्यूटर पर `http://localhost:5000` एड्रेस पर एक HTTP सर्वर शुरू करेगा। एक ब्राउज़र खोलें और उस एड्रेस को इनपुट करें। यह अभी एक खाली पेज है, लेकिन यह बदल जाएगा।

> नोट: स्क्रीन पर बदलाव देखने के लिए, अपने ब्राउज़र को रिफ्रेश करें।

### कोड जोड़ें

`your-work/app.js` में आवश्यक कोड जोड़ें ताकि नीचे दिए गए को हल किया जा सके:

1. **ड्रॉ करें** एक कैनवास काले बैकग्राउंड के साथ
   > टिप: `/app.js` में उपयुक्त TODO के तहत दो लाइनें जोड़ें, `ctx` एलिमेंट को काला सेट करें और टॉप/लेफ्ट कोऑर्डिनेट्स को 0,0 पर सेट करें और कैनवास की ऊंचाई और चौड़ाई के बराबर करें।
2. **लोड करें** टेक्सचर्स
   > टिप: `await loadTexture` का उपयोग करके और इमेज पाथ पास करके प्लेयर और दुश्मन इमेजेस जोड़ें। आप उन्हें अभी स्क्रीन पर नहीं देखेंगे!
3. **ड्रॉ करें** हीरो को स्क्रीन के सेंटर में नीचे के आधे हिस्से में
   > टिप: `drawImage` API का उपयोग करके हीरो इमेज को स्क्रीन पर ड्रॉ करें, `canvas.width / 2 - 45` और `canvas.height - canvas.height / 4)` सेट करें।
4. **ड्रॉ करें** 5*5 मॉन्स्टर्स
   > टिप: अब आप स्क्रीन पर दुश्मनों को ड्रॉ करने के लिए कोड को अनकमेंट कर सकते हैं। फिर, `createEnemies` फंक्शन पर जाएं और इसे बनाएं।

   पहले, कुछ कॉन्स्टेंट्स सेट करें:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    फिर, मॉन्स्टर्स की एक एरे को स्क्रीन पर ड्रॉ करने के लिए एक लूप बनाएं:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## परिणाम

अंतिम परिणाम इस तरह दिखना चाहिए:

![काली स्क्रीन जिसमें एक हीरो और 5*5 मॉन्स्टर्स हैं](../../../../6-space-game/2-drawing-to-canvas/partI-solution.png)

## समाधान

कृपया पहले इसे स्वयं हल करने का प्रयास करें लेकिन यदि आप अटक जाते हैं, तो [समाधान](../../../../6-space-game/2-drawing-to-canvas/solution/app.js) देखें।

---

## 🚀 चुनौती

आपने 2D-केंद्रित कैनवास API के साथ ड्रॉ करना सीखा है; [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) पर एक नज़र डालें, और 3D ऑब्जेक्ट ड्रॉ करने का प्रयास करें।

## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/32)

## समीक्षा और स्व-अध्ययन

कैनवास API के बारे में अधिक जानने के लिए [इसके बारे में पढ़ें](https://developer.mozilla.org/docs/Web/API/Canvas_API)।

## असाइनमेंट

[कैनवास API के साथ खेलें](assignment.md)

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता के लिए प्रयासरत हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।