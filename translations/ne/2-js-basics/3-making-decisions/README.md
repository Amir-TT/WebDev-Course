<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "888609c48329c280ca2477d2df40f2e5",
  "translation_date": "2025-08-25T21:35:25+00:00",
  "source_file": "2-js-basics/3-making-decisions/README.md",
  "language_code": "ne"
}
-->
# जाभास्क्रिप्ट आधारभूत: निर्णय लिनु

![जाभास्क्रिप्ट आधारभूत - निर्णय लिनु](../../../../translated_images/webdev101-js-decisions.69e1b20f272dd1f0b1cb2f8adaff3ed2a77c4f91db96d8a0594132a353fa189a.ne.png)

> स्केच नोट [Tomomi Imura](https://twitter.com/girlie_mac) द्वारा

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/11)

निर्णय लिनु र तपाईंको कोड कसरी चल्छ भन्ने क्रम नियन्त्रण गर्नुले तपाईंको कोडलाई पुन: प्रयोगयोग्य र बलियो बनाउँछ। यो खण्डले जाभास्क्रिप्टमा डाटा प्रवाह नियन्त्रण गर्ने सिन्ट्याक्स र बूलियन डाटा प्रकारसँग प्रयोग गर्दा यसको महत्त्वलाई समेट्छ।

[![निर्णय लिनु](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "निर्णय लिनु")

> 🎥 माथिको तस्बिरमा क्लिक गरेर निर्णय लिनु सम्बन्धी भिडियो हेर्नुहोस्।

> तपाईं यो पाठ [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon) मा लिन सक्नुहुन्छ!

## बूलियनको संक्षिप्त पुनरावलोकन

बूलियनमा केवल दुई मानहरू हुन सक्छ: `true` वा `false`। बूलियनले निर्णय लिन मद्दत गर्छ कि कुन लाइनको कोड निश्चित सर्तहरू पूरा हुँदा चल्नुपर्छ।

तपाईंको बूलियनलाई यसरी `true` वा `false` मा सेट गर्नुहोस्:

`let myTrueBool = true`  
`let myFalseBool = false`

✅ बूलियनको नाम अंग्रेज गणितज्ञ, दार्शनिक र तर्कशास्त्री George Boole (1815–1864) बाट राखिएको हो।

## तुलना अपरेटरहरू र बूलियनहरू

अपरेटरहरू सर्तहरू मूल्याङ्कन गर्न प्रयोग गरिन्छ जसले बूलियन मान सिर्जना गर्न तुलना गर्छ। तल बारम्बार प्रयोग गरिने अपरेटरहरूको सूची छ।

| प्रतीक | विवरण                                                                                                                                                   | उदाहरण            |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `<`    | **कम छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षको भन्दा कम छ भने `true` बूलियन डाटा प्रकार फर्काउँछ                              | `5 < 6 // true`    |
| `<=`   | **कम वा बराबर छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षको भन्दा कम वा बराबर छ भने `true` बूलियन डाटा प्रकार फर्काउँछ            | `5 <= 6 // true`   |
| `>`    | **ठूलो छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षको भन्दा ठूलो छ भने `true` बूलियन डाटा प्रकार फर्काउँछ                          | `5 > 6 // false`   |
| `>=`   | **ठूलो वा बराबर छ**: दुई मानहरूको तुलना गर्छ र यदि बाँया पक्षको मान दायाँ पक्षको भन्दा ठूलो वा बराबर छ भने `true` बूलियन डाटा प्रकार फर्काउँछ        | `5 >= 6 // false`  |
| `===`  | **सख्त समानता**: दुई मानहरूको तुलना गर्छ र यदि बाँया र दायाँ पक्षको मान समान छ र समान डाटा प्रकार छ भने `true` बूलियन डाटा प्रकार फर्काउँछ         | `5 === 6 // false` |
| `!==`  | **असमानता**: दुई मानहरूको तुलना गर्छ र सख्त समानता अपरेटरले फर्काउने विपरीत बूलियन मान फर्काउँछ                                                       | `5 !== 6 // true`  |

✅ तपाईंको ब्राउजरको कन्सोलमा केही तुलना लेखेर तपाईंको ज्ञान जाँच गर्नुहोस्। के कुनै फर्काइएको डाटाले तपाईंलाई अचम्मित बनायो?

## If स्टेटमेन्ट

If स्टेटमेन्टले आफ्नो ब्लकभित्रको कोड चलाउँछ यदि सर्त `true` छ भने।

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

तर्कशास्त्र अपरेटरहरू प्राय: सर्त बनाउन प्रयोग गरिन्छ।

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## If..Else स्टेटमेन्ट

`else` स्टेटमेन्टले आफ्नो ब्लकभित्रको कोड चलाउँछ जब सर्त `false` हुन्छ। यो `if` स्टेटमेन्टसँग वैकल्पिक छ।

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is false. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

✅ यो कोड र तलको कोडलाई ब्राउजर कन्सोलमा चलाएर तपाईंको बुझाइ जाँच गर्नुहोस्। `currentMoney` र `laptopPrice` भेरिएबलहरूको मान परिवर्तन गरेर फर्काइएको `console.log()` परिवर्तन गर्नुहोस्।

## Switch स्टेटमेन्ट

`switch` स्टेटमेन्ट विभिन्न सर्तहरूमा आधारित विभिन्न कार्यहरू प्रदर्शन गर्न प्रयोग गरिन्छ। `switch` स्टेटमेन्ट प्रयोग गरेर धेरै कोड ब्लकहरू मध्ये एक चयन गर्न सकिन्छ।

```javascript
switch (expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
  // code block
}
```

```javascript
// program using switch statement
let a = 2;

switch (a) {
  case 1:
    a = "one";
    break;
  case 2:
    a = "two";
    break;
  default:
    a = "not found";
    break;
}
console.log(`The value is ${a}`);
```

✅ यो कोड र तलको कोडलाई ब्राउजर कन्सोलमा चलाएर तपाईंको बुझाइ जाँच गर्नुहोस्। `a` भेरिएबलको मान परिवर्तन गरेर फर्काइएको `console.log()` परिवर्तन गर्नुहोस्।

## तर्कशास्त्र अपरेटरहरू र बूलियनहरू

निर्णयले एकभन्दा बढी तुलना आवश्यक हुन सक्छ, र तर्कशास्त्र अपरेटरहरूसँग जोडेर बूलियन मान उत्पादन गर्न सकिन्छ।

| प्रतीक | विवरण                                                                                     | उदाहरण                                                                 |
| ------ | ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `&&`   | **तर्कशास्त्र AND**: दुई बूलियन अभिव्यक्तिहरू तुलना गर्छ। दुवै पक्ष `true` भए मात्र `true` फर्काउँछ | `(5 > 6) && (5 < 6 ) //एक पक्ष false छ, अर्को true छ। false फर्काउँछ` |
| `\|\|` | **तर्कशास्त्र OR**: दुई बूलियन अभिव्यक्तिहरू तुलना गर्छ। कम्तीमा एक पक्ष `true` भए `true` फर्काउँछ | `(5 > 6) \|\| (5 < 6) //एक पक्ष false छ, अर्को true छ। true फर्काउँछ` |
| `!`    | **तर्कशास्त्र NOT**: बूलियन अभिव्यक्तिको विपरीत मान फर्काउँछ                             | `!(5 > 6) // 5 6 भन्दा ठूलो छैन, तर "!" ले true फर्काउँछ`             |

## तर्कशास्त्र अपरेटरहरूसँग सर्तहरू र निर्णयहरू

तर्कशास्त्र अपरेटरहरू if..else स्टेटमेन्टमा सर्त बनाउन प्रयोग गर्न सकिन्छ।

```javascript
let currentMoney;
let laptopPrice;
let laptopDiscountPrice = laptopPrice - laptopPrice * 0.2; //Laptop price at 20 percent off

if (currentMoney >= laptopPrice || currentMoney >= laptopDiscountPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
} else {
  //Condition is true. Code in this block will run.
  console.log("Can't afford a new laptop, yet!");
}
```

### नेगेसन अपरेटर

तपाईंले अहिलेसम्म देख्नुभएको छ कि कसरी `if...else` स्टेटमेन्ट प्रयोग गरेर सर्तात्मक तर्क सिर्जना गर्न सकिन्छ। `if` मा जाने कुनै पनि कुरा true/false मा मूल्याङ्कन गर्नुपर्छ। `!` अपरेटर प्रयोग गरेर तपाईं अभिव्यक्तिलाई _नेगेट_ गर्न सक्नुहुन्छ। यसले यसरी देखिन्छ:

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### टर्नरी अभिव्यक्ति

`if...else` निर्णय तर्क व्यक्त गर्ने एकमात्र तरिका होइन। तपाईंले टर्नरी अपरेटर भनिने केही पनि प्रयोग गर्न सक्नुहुन्छ। यसको सिन्ट्याक्स यसरी देखिन्छ:

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

तल एक थप स्पष्ट उदाहरण छ:

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ यो कोडलाई केही पटक पढ्न समय लिनुहोस्। के तपाईंलाई यी अपरेटरहरू कसरी काम गरिरहेका छन् भन्ने बुझ्नुभयो?

माथिको कोडले भन्छ:

- यदि `firstNumber` `secondNumber` भन्दा ठूलो छ
- भने `firstNumber` लाई `biggestNumber` मा असाइन गर्नुहोस्
- अन्यथा `secondNumber` लाई असाइन गर्नुहोस्।

टर्नरी अभिव्यक्ति तलको कोड लेख्ने संक्षिप्त तरिका मात्र हो:

```javascript
let biggestNumber;
if (firstNumber > secondNumber) {
  biggestNumber = firstNumber;
} else {
  biggestNumber = secondNumber;
}
```

---

## 🚀 चुनौती

पहिले तर्कशास्त्र अपरेटरहरूसँग लेखिएको र त्यसपछि टर्नरी अभिव्यक्ति प्रयोग गरेर पुन: लेखिएको प्रोग्राम सिर्जना गर्नुहोस्। तपाईंलाई कुन सिन्ट्याक्स मनपर्छ?

---

## पोस्ट-लेक्चर क्विज

[पोस्ट-लेक्चर क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/12)

## समीक्षा र आत्म-अध्ययन

प्रयोगकर्तालाई उपलब्ध धेरै अपरेटरहरूको बारेमा [MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators) मा थप पढ्नुहोस्।

Josh Comeau को उत्कृष्ट [अपरेटर लुकअप](https://joshwcomeau.com/operator-lookup/) हेर्नुहोस्!

## असाइनमेन्ट

[अपरेटरहरू](assignment.md)

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।