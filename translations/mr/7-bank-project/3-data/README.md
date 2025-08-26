<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f587e913e3f7c0b1c549a05dd74ee8e5",
  "translation_date": "2025-08-26T00:22:01+00:00",
  "source_file": "7-bank-project/3-data/README.md",
  "language_code": "mr"
}
-->
# बँकिंग अ‍ॅप तयार करा भाग ३: डेटा मिळवण्याचे आणि वापरण्याचे पद्धती

## पूर्व-व्याख्यान प्रश्नमंजुषा

[पूर्व-व्याख्यान प्रश्नमंजुषा](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/45)

### परिचय

प्रत्येक वेब अ‍ॅप्लिकेशनच्या केंद्रस्थानी *डेटा* असतो. डेटा विविध स्वरूपात असतो, परंतु त्याचा मुख्य उद्देश नेहमीच वापरकर्त्याला माहिती दाखवणे असतो. वेब अ‍ॅप्स अधिकाधिक परस्परसंवादी आणि जटिल होत असल्यामुळे, वापरकर्त्याने माहिती कशी प्रवेश करावी आणि त्याचा कसा उपयोग करावा हे वेब विकासाचा महत्त्वाचा भाग बनला आहे.

या धड्यात, आम्ही पाहू की सर्व्हरवरून डेटा असिंक्रोनस पद्धतीने कसा मिळवायचा आणि HTML पुन्हा लोड न करता वेब पृष्ठावर माहिती कशी दाखवायची.

### पूर्वतयारी

या धड्यासाठी तुम्ही वेब अ‍ॅपचा [लॉगिन आणि नोंदणी फॉर्म](../2-forms/README.md) तयार केला असावा. तुम्हाला [Node.js](https://nodejs.org) स्थापित करणे आणि [सर्व्हर API](../api/README.md) स्थानिक पातळीवर चालवणे आवश्यक आहे जेणेकरून तुम्हाला खाते डेटा मिळेल.

सर्व्हर योग्यरित्या चालू आहे की नाही हे तपासण्यासाठी टर्मिनलमध्ये खालील कमांड चालवा:

```sh
curl http://localhost:5000/api
# -> should return "Bank API v1.0.0" as a result
```

---

## AJAX आणि डेटा मिळवणे

पारंपरिक वेब साइट्स वापरकर्त्याने लिंक निवडल्यावर किंवा फॉर्मद्वारे डेटा सबमिट केल्यावर पूर्ण HTML पृष्ठ पुन्हा लोड करून सामग्री अपडेट करतात. नवीन डेटा लोड करण्यासाठी प्रत्येक वेळी वेब सर्व्हर नवीन HTML पृष्ठ परत करतो ज्याला ब्राउझरद्वारे प्रक्रिया करावी लागते, सध्याच्या वापरकर्त्याच्या क्रियेत व्यत्यय आणतो आणि रीलोड दरम्यान परस्परसंवाद मर्यादित करतो. या कार्यप्रवाहाला *मल्टी-पेज अ‍ॅप्लिकेशन* किंवा *MPA* असेही म्हणतात.

![मल्टी-पेज अ‍ॅप्लिकेशनमधील अपडेट कार्यप्रवाह](../../../../translated_images/mpa.7f7375a1a2d4aa779d3f928a2aaaf9ad76bcdeb05cfce2dc27ab126024050f51.mr.png)

वेब अ‍ॅप्लिकेशन्स अधिक जटिल आणि परस्परसंवादी होऊ लागल्यावर, [AJAX (Asynchronous JavaScript and XML)](https://en.wikipedia.org/wiki/Ajax_(programming)) नावाची नवीन तंत्रज्ञान विकसित झाली. या तंत्रज्ञानामुळे वेब अ‍ॅप्सना JavaScript वापरून सर्व्हरकडून डेटा असिंक्रोनस पद्धतीने पाठवणे आणि मिळवणे शक्य झाले, HTML पृष्ठ पुन्हा लोड न करता, ज्यामुळे जलद अपडेट्स आणि गुळगुळीत वापरकर्ता परस्परसंवाद शक्य झाले. सर्व्हरकडून नवीन डेटा प्राप्त झाल्यावर, सध्याचे HTML पृष्ठ JavaScript वापरून [DOM](https://developer.mozilla.org/docs/Web/API/Document_Object_Model) API च्या मदतीने अपडेट केले जाऊ शकते. कालांतराने, ही पद्धत [*सिंगल-पेज अ‍ॅप्लिकेशन* किंवा *SPA*](https://en.wikipedia.org/wiki/Single-page_application) म्हणून विकसित झाली.

![सिंगल-पेज अ‍ॅप्लिकेशनमधील अपडेट कार्यप्रवाह](../../../../translated_images/spa.268ec73b41f992c2a21ef9294235c6ae597b3c37e2c03f0494c2d8857325cc57.mr.png)

AJAX प्रथम सादर झाल्यावर, असिंक्रोनस पद्धतीने डेटा मिळवण्यासाठी उपलब्ध असलेली एकमेव API [`XMLHttpRequest`](https://developer.mozilla.org/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) होती. परंतु आधुनिक ब्राउझर आता अधिक सोयीस्कर आणि शक्तिशाली [`Fetch` API](https://developer.mozilla.org/docs/Web/API/Fetch_API) लागू करतात, जी प्रॉमिसेस वापरते आणि JSON डेटा हाताळण्यासाठी अधिक योग्य आहे.

> सर्व आधुनिक ब्राउझर `Fetch API` ला समर्थन देतात, परंतु तुमचे वेब अ‍ॅप्लिकेशन जुने किंवा वारसा ब्राउझरवर कार्य करावे अशी तुमची इच्छा असल्यास, [caniuse.com वर सुसंगतता टेबल](https://caniuse.com/fetch) तपासणे नेहमीच चांगले आहे.

### कार्य

[मागील धड्यात](../2-forms/README.md) आम्ही खाते तयार करण्यासाठी नोंदणी फॉर्म अंमलात आणला. आता आम्ही विद्यमान खात्याचा वापर करून लॉगिन करण्यासाठी कोड जोडू आणि त्याचा डेटा मिळवू. `app.js` फाइल उघडा आणि नवीन `login` फंक्शन जोडा:

```js
async function login() {
  const loginForm = document.getElementById('loginForm')
  const user = loginForm.user.value;
}
```

येथे आम्ही `getElementById()` वापरून फॉर्म घटक मिळवण्यास सुरुवात करतो आणि नंतर `loginForm.user.value` वापरून इनपुटमधून वापरकर्त्याचे नाव मिळवतो. प्रत्येक फॉर्म कंट्रोलला त्याच्या नावाने (HTML मध्ये `name` अ‍ॅट्रिब्युट वापरून सेट केलेले) फॉर्मच्या प्रॉपर्टी म्हणून प्रवेश करता येतो.

नोंदणीसाठी केलेल्या पद्धतीप्रमाणेच, आम्ही सर्व्हर विनंती करण्यासाठी आणखी एक फंक्शन तयार करू, परंतु यावेळी खाते डेटा मिळवण्यासाठी:

```js
async function getAccount(user) {
  try {
    const response = await fetch('//localhost:5000/api/accounts/' + encodeURIComponent(user));
    return await response.json();
  } catch (error) {
    return { error: error.message || 'Unknown error' };
  }
}
```

आम्ही `fetch` API वापरून सर्व्हरकडून डेटा असिंक्रोनस पद्धतीने मिळवतो, परंतु यावेळी आम्हाला फक्त डेटा क्वेरी करायचा असल्यामुळे URL व्यतिरिक्त कोणतेही अतिरिक्त पॅरामीटर्स आवश्यक नाहीत. डीफॉल्टनुसार, `fetch` [`GET`](https://developer.mozilla.org/docs/Web/HTTP/Methods/GET) HTTP विनंती तयार करते, जी आम्हाला येथे हवी आहे.

✅ `encodeURIComponent()` ही एक फंक्शन आहे जी URL साठी विशेष वर्ण एस्केप करते. जर आम्ही ही फंक्शन कॉल केली नाही आणि थेट `user` मूल्य URL मध्ये वापरले तर कोणती समस्या उद्भवू शकते?

आता आमच्या `login` फंक्शनला `getAccount` वापरण्यासाठी अपडेट करूया:

```js
async function login() {
  const loginForm = document.getElementById('loginForm')
  const user = loginForm.user.value;
  const data = await getAccount(user);

  if (data.error) {
    return console.log('loginError', data.error);
  }

  account = data;
  navigate('/dashboard');
}
```

प्रथम, `getAccount` हे असिंक्रोनस फंक्शन असल्याने आम्हाला सर्व्हरच्या निकालाची वाट पाहण्यासाठी `await` कीवर्ड वापरावा लागतो. कोणत्याही सर्व्हर विनंतीप्रमाणे, आम्हाला त्रुटी प्रकरणांशी देखील व्यवहार करावा लागतो. सध्या आम्ही फक्त त्रुटी प्रदर्शित करण्यासाठी लॉग संदेश जोडू आणि नंतर त्याकडे परत येऊ.

यानंतर, आम्हाला डेटा कुठेतरी संग्रहित करावा लागतो जेणेकरून आम्ही नंतर डॅशबोर्ड माहिती प्रदर्शित करण्यासाठी त्याचा उपयोग करू शकू. कारण `account` व्हेरिएबल अद्याप अस्तित्वात नाही, आम्ही आमच्या फाइलच्या शीर्षस्थानी एक ग्लोबल व्हेरिएबल तयार करू:

```js
let account = null;
```

वापरकर्ता डेटा व्हेरिएबलमध्ये सेव्ह झाल्यानंतर आम्ही *लॉगिन* पृष्ठावरून *डॅशबोर्ड* वर `navigate()` फंक्शन वापरून जाऊ शकतो.

शेवटी, लॉगिन फॉर्म सबमिट झाल्यावर आमच्या `login` फंक्शनला कॉल करणे आवश्यक आहे, HTML बदलून:

```html
<form id="loginForm" action="javascript:login()">
```

नवीन खाते नोंदणी करून आणि त्याच खात्याचा वापर करून लॉगिन करण्याचा प्रयत्न करून सर्वकाही योग्यरित्या कार्य करत आहे की नाही हे तपासा.

पुढील भागाकडे जाण्यापूर्वी, आम्ही `register` फंक्शन पूर्ण करू शकतो आणि फंक्शनच्या शेवटी हे जोडू शकतो:

```js
account = result;
navigate('/dashboard');
```

✅ तुम्हाला माहित आहे का की डीफॉल्टनुसार, तुम्ही फक्त *समान डोमेन आणि पोर्ट* वरून सर्व्हर API कॉल करू शकता ज्यावर तुम्ही वेब पृष्ठ पाहत आहात? हे ब्राउझरद्वारे लागू केलेले सुरक्षा यंत्रणा आहे. पण थांबा, आमचे वेब अ‍ॅप `localhost:3000` वर चालत आहे तर सर्व्हर API `localhost:5000` वर चालत आहे, तरीही ते कार्य करते का? [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS) नावाच्या तंत्राचा वापर करून, सर्व्हरने प्रतिसादामध्ये विशेष हेडर्स जोडल्यास, विशिष्ट डोमेनसाठी अपवाद परवानगी देऊन क्रॉस-ऑरिजिन HTTP विनंत्या करणे शक्य आहे.

> API बद्दल अधिक जाणून घेण्यासाठी [हा धडा](https://docs.microsoft.com/learn/modules/use-apis-discover-museum-art/?WT.mc_id=academic-77807-sagibbon) घ्या

## HTML अपडेट करून डेटा प्रदर्शित करा

आता आपल्याकडे वापरकर्ता डेटा आहे, आपल्याला तो प्रदर्शित करण्यासाठी विद्यमान HTML अपडेट करावा लागेल. आम्हाला आधीच माहित आहे की DOM मधून घटक कसा मिळवायचा, उदाहरणार्थ `document.getElementById()` वापरून. एकदा तुम्हाला बेस घटक मिळाला की, तुम्ही त्याला बदलण्यासाठी किंवा त्यामध्ये उपघटक जोडण्यासाठी खालील API वापरू शकता:

- [`textContent`](https://developer.mozilla.org/docs/Web/API/Node/textContent) प्रॉपर्टी वापरून तुम्ही घटकाचा मजकूर बदलू शकता. लक्षात ठेवा की हे मूल्य बदलल्याने घटकाचे सर्व उपघटक (जर काही असतील) काढून टाकले जातात आणि प्रदान केलेल्या मजकूराने बदलले जाते. त्यामुळे, दिलेल्या घटकाचे सर्व उपघटक काढून टाकण्यासाठी रिक्त स्ट्रिंग `''` नियुक्त करणे ही एक कार्यक्षम पद्धत आहे.

- [`document.createElement()`](https://developer.mozilla.org/docs/Web/API/Document/createElement) आणि [`append()`](https://developer.mozilla.org/docs/Web/API/ParentNode/append) पद्धतीसह तुम्ही एक किंवा अधिक नवीन उपघटक तयार करू शकता आणि जोडू शकता.

✅ [`innerHTML`](https://developer.mozilla.org/docs/Web/API/Element/innerHTML) प्रॉपर्टी वापरून घटकाची HTML सामग्री बदलणे देखील शक्य आहे, परंतु हे [क्रॉस-साइट स्क्रिप्टिंग (XSS)](https://developer.mozilla.org/docs/Glossary/Cross-site_scripting) हल्ल्यांसाठी असुरक्षित असल्यामुळे टाळले पाहिजे.

### कार्य

डॅशबोर्ड स्क्रीनवर जाण्यापूर्वी, *लॉगिन* पृष्ठावर एक गोष्ट करणे आवश्यक आहे. सध्या, जर तुम्ही अस्तित्वात नसलेल्या वापरकर्त्याचे नाव वापरून लॉगिन करण्याचा प्रयत्न केला, तर कन्सोलमध्ये संदेश दाखवला जातो परंतु सामान्य वापरकर्त्यासाठी काहीही बदलत नाही आणि तुम्हाला काय चालले आहे हे कळत नाही.

चला लॉगिन `<button>` च्या अगोदर फॉर्ममध्ये एक प्लेसहोल्डर घटक जोडूया जिथे आवश्यक असल्यास त्रुटी संदेश प्रदर्शित करू शकतो:

```html
...
<div id="loginError"></div>
<button>Login</button>
...
```

हा `<div>` घटक रिक्त आहे, म्हणजे स्क्रीनवर काहीही प्रदर्शित होणार नाही जोपर्यंत आम्ही त्यामध्ये काही सामग्री जोडत नाही. आम्ही त्याला `id` देखील देतो जेणेकरून आम्ही JavaScript सह सहजपणे त्याला मिळवू शकू.

`app.js` फाइलवर परत जा आणि नवीन हेल्पर फंक्शन `updateElement` तयार करा:

```js
function updateElement(id, text) {
  const element = document.getElementById(id);
  element.textContent = text;
}
```

हे फंक्शन अगदी सोपे आहे: दिलेल्या घटक *id* आणि *text* च्या आधारे, ते `id` असलेल्या DOM घटकाच्या मजकूर सामग्रीला अपडेट करेल. चला `login` फंक्शनमधील पूर्वीच्या त्रुटी संदेशाच्या जागी ही पद्धत वापरूया:

```js
if (data.error) {
  return updateElement('loginError', data.error);
}
```

आता जर तुम्ही अवैध खात्याने लॉगिन करण्याचा प्रयत्न केला, तर तुम्हाला असे काहीतरी दिसेल:

![लॉगिन दरम्यान प्रदर्शित त्रुटी संदेश दर्शवणारा स्क्रीनशॉट](../../../../translated_images/login-error.416fe019b36a63276764c2349df5d99e04ebda54fefe60c715ee87a28d5d4ad0.mr.png)

आता आमच्याकडे व्हिज्युअली त्रुटी मजकूर आहे, परंतु जर तुम्ही स्क्रीन रीडर वापरून प्रयत्न केला तर तुम्हाला लक्षात येईल की काहीही घोषित केले जात नाही. पृष्ठावर डायनॅमिक पद्धतीने जोडलेला मजकूर स्क्रीन रीडरद्वारे घोषित होण्यासाठी, त्याला [Live Region](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) वापरावे लागेल. येथे आम्ही अलर्ट नावाच्या लाइव्ह रिजनचा विशिष्ट प्रकार वापरणार आहोत:

```html
<div id="loginError" role="alert"></div>
```

`register` फंक्शन त्रुटींसाठी समान वर्तन अंमलात आणा (HTML अपडेट करायला विसरू नका).

## डॅशबोर्डवर माहिती प्रदर्शित करा

आत्ताच पाहिलेल्या तंत्रांचा वापर करून, आम्ही डॅशबोर्ड पृष्ठावर खाते माहिती प्रदर्शित करण्याची काळजी घेऊ.

सर्व्हरकडून प्राप्त झालेले खाते ऑब्जेक्ट असे दिसते:

```json
{
  "user": "test",
  "currency": "$",
  "description": "Test account",
  "balance": 75,
  "transactions": [
    { "id": "1", "date": "2020-10-01", "object": "Pocket money", "amount": 50 },
    { "id": "2", "date": "2020-10-03", "object": "Book", "amount": -10 },
    { "id": "3", "date": "2020-10-04", "object": "Sandwich", "amount": -5 }
  ],
}
```

> टीप: तुमचे काम सोपे करण्यासाठी, तुम्ही आधीच डेटा भरलेले `test` खाते वापरू शकता.

### कार्य

चला HTML मधील "Balance" विभाग बदलून प्लेसहोल्डर घटक जोडूया:

```html
<section>
  Balance: <span id="balance"></span><span id="currency"></span>
</section>
```

आम्ही खाते वर्णन प्रदर्शित करण्यासाठी खाली नवीन विभाग देखील जोडू:

```html
<h2 id="description"></h2>
```

✅ कारण खाते वर्णन त्याखालील सामग्रीसाठी शीर्षक म्हणून कार्य करते, ते अर्थपूर्णपणे शीर्षक म्हणून चिन्हांकित केले आहे. [शीर्षक संरचना](https://www.nomensa.com/blog/2017/how-structure-headings-web-accessibility) कशी महत्त्वाची आहे याबद्दल अधिक जाणून घ्या आणि पृष्ठावर इतर काय शीर्षक असू शकते याचा गंभीरपणे विचार करा.

पुढे, आम्ही `app.js` मध्ये नवीन फंक्शन तयार करू जे प्लेसहोल्डर भरते:

```js
function updateDashboard() {
  if (!account) {
    return navigate('/login');
  }

  updateElement('description', account.description);
  updateElement('balance', account.balance.toFixed(2));
  updateElement('currency', account.currency);
}
```

प्रथम, आम्ही पुढे जाण्यापूर्वी आमच्याकडे आवश्यक खाते डेटा आहे की नाही हे तपासतो. त्यानंतर आम्ही HTML अपडेट करण्यासाठी आम्ही पूर्वी तयार केलेल्या `updateElement()` फंक्शनचा वापर करतो.

> बॅलन्स डिस्प्ले अधिक आकर्षक बनवण्यासाठी, आम्ही [`toFixed(2)`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) पद्धत वापरतो जेणेकरून मूल्य दशांश बिंदू नंतर 2 अंकांसह प्रदर्शित होईल.

आता आम्हाला डॅशबोर्ड लोड झाल्यावर प्रत्येक वेळी आमच्या `updateDashboard()` फंक्शनला कॉल करणे आवश्यक आहे. जर तुम्ही [धडा १ असाइनमेंट](../1-template-route/assignment.md) पूर्ण केला असेल तर हे सोपे असावे, अन्यथा तुम्ही खालील अंमलबजावणी वापरू शकता.

`updateRoute()` फंक्शनच्या शेवटी हा कोड जोडा:

```js
if (typeof route.init === 'function') {
  route.init();
}
```

आणि रूट्स परिभाषा अपडेट करा:

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard', init: updateDashboard }
};
```

या बदलासह, डॅशबोर्ड पृष्ठ प्रदर्शित झाल्यावर प्रत्येक वेळी `updateDashboard()` फंक्शन कॉल केले जाते. लॉगिननंतर, तुम्हाला खाते बॅलन्स, चलन आणि वर्णन पाहता येईल.

## HTML टेम्पलेट्ससह टेबल रो डायनॅमिक पद्धतीने तयार करा

[पहिल्या धड्यात](../1-template-route/README.md) आम्ही HTML टेम्पलेट्ससह [`appendChild()`](https://developer.mozilla.org/docs/Web/API/Node/appendChild) पद्धत वापरून अ‍ॅपमधील नेव्हिगेशन अंमलात आणले. टेम्पलेट्स लहान देखील असू शकतात आणि पृष्ठाच्या पुनरावृत्ती भागांना डायनॅमिक पद्धतीने भरण्यासाठी वापरले जाऊ शकतात.

आम्ही HTML टेबलमध्ये व्यवहारांची यादी प्रदर्शित करण्यासाठी समान दृष्टिकोन वापरणार आहोत.

### कार्य

HTML `<body>` मध्ये नवीन टेम्पलेट जोडा:

```html
<template id="transaction">
  <tr>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</template>
```

हे टेम्पलेट एकच टेबल रो दर्शवते, ज्यामध्ये आम्हाला भरायचे असलेले ३ कॉलम आहेत: व्यवहाराचा *date*, *object* आणि *amount*.

यानंतर, टेबलमधील `<tbody>` घटकाला JavaScript वापरून शोधणे सोपे करण्यासाठी `id` प्रॉपर्टी जोडा:

```html
<tbody id="transactions"></tbody>
```

आमचे HTML तयार आहे, चला JavaScript कोडकडे वळूया आणि नवीन फंक्शन `createTransactionRow` तयार करूया:

```js
function createTransactionRow(transaction) {
  const template = document.getElementById('transaction');
  const transactionRow = template.content.cloneNode(true);
  const tr = transactionRow.querySelector('tr');
  tr.children[0].textContent = transaction.date;
  tr.children[1].textContent = transaction.object;
  tr.children[2].textContent = transaction.amount.toFixed(2);
  return transactionRow;
}
```

हे फंक्शन त्याचे नाव सूचित करते तेच करते: आम्ही पूर्वी तयार केलेल्या टेम्पलेटचा वापर करून, ते नवीन टेबल रो तयार करते आणि व्यवहार डेटा वापरून त्याची सामग्री भरते. आम्ही आमच्या `updateDashboard()` फंक्शनमध्ये टेबल भरण्यासाठी याचा वापर करू:

```js
const transactionsRows = document.createDocumentFragment();
for (const transaction of account.transactions) {
  const transactionRow = createTransactionRow(transaction);
  transactionsRows.appendChild(transactionRow);
}
updateElement('transactions', transactionsRows);
```

येथे आम्ही [`document.createDocumentFragment()`](https://developer.mozilla.org/docs/Web/API/Document/createDocumentFragment) पद्धत वापरतो जी नवीन DOM फ्रॅगमेंट तयार करते ज्यावर आम्ही काम करू शकतो, शेवटी ते आमच्या HTML टेबलला जोडण्यापूर्वी.

हा कोड कार्य करू शकतो यासाठी अजून एक गोष्ट करणे आवश्यक आहे, कारण आमचे `updateElement()` फंक
जर तुम्ही `test` खाते वापरून लॉगिन करण्याचा प्रयत्न केला, तर आता तुम्हाला डॅशबोर्डवर व्यवहारांची यादी दिसेल 🎉.

---

## 🚀 आव्हान

डॅशबोर्ड पृष्ठ खऱ्या बँकिंग अॅपसारखे दिसण्यासाठी एकत्र काम करा. जर तुम्ही आधीच तुमचे अॅप स्टाइल केले असेल, तर [मीडिया क्वेरीज](https://developer.mozilla.org/docs/Web/CSS/Media_Queries) वापरून [प्रतिसादक्षम डिझाइन](https://developer.mozilla.org/docs/Web/Progressive_web_apps/Responsive/responsive_design_building_blocks) तयार करण्याचा प्रयत्न करा, जे डेस्कटॉप आणि मोबाइल डिव्हाइसवर चांगले कार्य करेल.

स्टाइल केलेल्या डॅशबोर्ड पृष्ठाचे एक उदाहरण येथे आहे:

![स्टाइल केलेल्या डॅशबोर्डचा स्क्रीनशॉट](../../../../translated_images/screen2.123c82a831a1d14ab2061994be2fa5de9cec1ce651047217d326d4773a6348e4.mr.png)

## व्याख्यानानंतरचा प्रश्नमंजूषा

[व्याख्यानानंतरचा प्रश्नमंजूषा](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/46)

## असाइनमेंट

[तुमचा कोड पुनर्रचित करा आणि त्यावर टिप्पणी द्या](assignment.md)

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरांमध्ये त्रुटी किंवा अचूकतेचा अभाव असू शकतो. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून निर्माण होणाऱ्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.