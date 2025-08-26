<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e10f168beac4e7b05e30e0eb5c92bf11",
  "translation_date": "2025-08-25T23:29:57+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "mr"
}
-->
# ब्राउझर एक्स्टेंशन प्रोजेक्ट भाग 2: API कॉल करा, लोकल स्टोरेज वापरा

## प्री-लेक्चर क्विझ

[प्री-लेक्चर क्विझ](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/25)

### परिचय

या धड्यात, तुम्ही तुमच्या ब्राउझर एक्स्टेंशनच्या फॉर्मद्वारे API कॉल कराल आणि त्याचे परिणाम ब्राउझर एक्स्टेंशनमध्ये दाखवाल. याशिवाय, तुम्ही तुमच्या ब्राउझरच्या लोकल स्टोरेजमध्ये डेटा कसा साठवायचा आणि भविष्यात त्याचा कसा उपयोग करायचा हे शिकाल.

✅ योग्य फाईल्समधील क्रमांकित विभागांचे अनुसरण करा, जेथे कोड ठेवायचा आहे ते समजून घ्या.

### एक्स्टेंशनमध्ये बदल करण्यासाठी घटक सेट करा:

आतापर्यंत तुम्ही तुमच्या ब्राउझर एक्स्टेंशनसाठी फॉर्म आणि परिणाम `<div>` साठी HTML तयार केले आहे. आता तुम्हाला `/src/index.js` फाईलमध्ये काम करायचे आहे आणि तुमचे एक्स्टेंशन हळूहळू तयार करायचे आहे. प्रोजेक्ट सेटअप आणि बिल्ड प्रक्रियेबद्दल अधिक माहितीसाठी [मागील धडा](../1-about-browsers/README.md) पहा.

`index.js` फाईलमध्ये काम करताना, विविध फील्डशी संबंधित मूल्ये ठेवण्यासाठी काही `const` व्हेरिएबल्स तयार करा:

```JavaScript
// form fields
const form = document.querySelector('.form-data');
const region = document.querySelector('.region-name');
const apiKey = document.querySelector('.api-key');

// results
const errors = document.querySelector('.errors');
const loading = document.querySelector('.loading');
const results = document.querySelector('.result-container');
const usage = document.querySelector('.carbon-usage');
const fossilfuel = document.querySelector('.fossil-fuel');
const myregion = document.querySelector('.my-region');
const clearBtn = document.querySelector('.clear-btn');
```

हे सर्व फील्ड्स त्यांच्या CSS क्लासद्वारे संदर्भित केले जातात, जसे तुम्ही मागील धड्यात HTML मध्ये सेट केले आहे.

### लिसनर्स जोडा

यानंतर, फॉर्म आणि रीसेट बटणासाठी इव्हेंट लिसनर्स जोडा, जेणेकरून वापरकर्ता फॉर्म सबमिट करतो किंवा रीसेट बटणावर क्लिक करतो तेव्हा काहीतरी होईल. फाईलच्या शेवटी अॅप इनिशियलाइझ करण्यासाठी कॉल जोडा:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ सबमिट किंवा क्लिक इव्हेंटसाठी वापरलेली शॉर्टहँड पद्धत लक्षात घ्या आणि इव्हेंट कसे `handleSubmit` किंवा `reset` फंक्शनला पास केले जाते ते पहा. तुम्ही या शॉर्टहँडचे लांब स्वरूपात रूपांतर करू शकता का? तुम्हाला कोणती पद्धत जास्त आवडते?

### `init()` फंक्शन आणि `reset()` फंक्शन तयार करा:

आता तुम्ही एक्स्टेंशन इनिशियलाइझ करणारे फंक्शन तयार करणार आहात, ज्याला `init()` म्हणतात:

```JavaScript
function init() {
	//if anything is in localStorage, pick it up
	const storedApiKey = localStorage.getItem('apiKey');
	const storedRegion = localStorage.getItem('regionName');

	//set icon to be generic green
	//todo

	if (storedApiKey === null || storedRegion === null) {
		//if we don't have the keys, show the form
		form.style.display = 'block';
		results.style.display = 'none';
		loading.style.display = 'none';
		clearBtn.style.display = 'none';
		errors.textContent = '';
	} else {
        //if we have saved keys/regions in localStorage, show results when they load
        displayCarbonUsage(storedApiKey, storedRegion);
		results.style.display = 'none';
		form.style.display = 'none';
		clearBtn.style.display = 'block';
	}
};

function reset(e) {
	e.preventDefault();
	//clear local storage for region only
	localStorage.removeItem('regionName');
	init();
}

```

या फंक्शनमध्ये काही मनोरंजक लॉजिक आहे. वाचताना, तुम्हाला काय घडते ते समजते का?

- दोन `const` तयार केले जातात जे तपासतात की वापरकर्त्याने APIKey आणि region code लोकल स्टोरेजमध्ये साठवले आहे का.
- जर त्यापैकी एकही null असेल, तर फॉर्मचे style 'block' म्हणून बदलून फॉर्म दाखवा.
- परिणाम, लोडिंग, आणि clearBtn लपवा आणि कोणताही error टेक्स्ट रिकामा ठेवा.
- जर APIKey आणि region अस्तित्वात असतील, तर पुढील प्रक्रिया सुरू करा:
  - API कॉल करून कार्बन वापर डेटा मिळवा.
  - परिणाम क्षेत्र लपवा.
  - फॉर्म लपवा.
  - रीसेट बटण दाखवा.

पुढे जाण्यापूर्वी, ब्राउझरमध्ये उपलब्ध असलेल्या एका महत्त्वाच्या संकल्पनेबद्दल जाणून घेणे उपयुक्त आहे: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage). LocalStorage ही ब्राउझरमध्ये `key-value` जोड्यांमध्ये स्ट्रिंग्स साठवण्याची उपयुक्त पद्धत आहे. या प्रकारचे वेब स्टोरेज जावास्क्रिप्टद्वारे ब्राउझरमधील डेटा व्यवस्थापित करण्यासाठी वापरले जाऊ शकते. LocalStorage कालबाह्य होत नाही, तर SessionStorage, वेब स्टोरेजचा दुसरा प्रकार, ब्राउझर बंद केल्यावर साफ केला जातो. वेगवेगळ्या प्रकारच्या स्टोरेजच्या वापराचे फायदे आणि तोटे आहेत.

> लक्षात ठेवा - तुमच्या ब्राउझर एक्स्टेंशनचे स्वतःचे लोकल स्टोरेज आहे; मुख्य ब्राउझर विंडो वेगळी असते आणि स्वतंत्रपणे वागते.

तुम्ही तुमच्या APIKey ला स्ट्रिंग मूल्य म्हणून सेट करता, उदाहरणार्थ, आणि तुम्ही Edge वर "inspect" करून हे पाहू शकता (ब्राउझरवर उजवे क्लिक करून inspect करा) आणि Applications टॅबमध्ये जाऊन स्टोरेज पाहू शकता.

![लोकल स्टोरेज पॅन](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.mr.png)

✅ अशा परिस्थितींबद्दल विचार करा जिथे तुम्हाला काही डेटा LocalStorage मध्ये साठवायचा नसेल. सामान्यतः, API Keys LocalStorage मध्ये ठेवणे चांगले नाही! तुम्हाला का वाटते? आमच्या बाबतीत, आमचे अॅप केवळ शिकण्यासाठी आहे आणि अॅप स्टोअरवर तैनात केले जाणार नाही, त्यामुळे आम्ही ही पद्धत वापरणार आहोत.

तुम्ही LocalStorage हाताळण्यासाठी Web API वापरता, `getItem()`, `setItem()`, किंवा `removeItem()` वापरून. हे सर्व ब्राउझरमध्ये मोठ्या प्रमाणावर समर्थित आहे.

`displayCarbonUsage()` फंक्शन तयार करण्यापूर्वी, जे `init()` मध्ये कॉल केले जाते, प्रारंभिक फॉर्म सबमिशन हाताळण्यासाठी कार्यक्षमता तयार करूया.

### फॉर्म सबमिशन हाताळा

`handleSubmit` नावाचे फंक्शन तयार करा जे `(e)` इव्हेंट आर्ग्युमेंट स्वीकारते. इव्हेंटचा प्रसार थांबवा (या प्रकरणात, आम्हाला ब्राउझर रीफ्रेश होण्यापासून थांबवायचे आहे) आणि `setUpUser` नावाच्या नवीन फंक्शनला कॉल करा, `apiKey.value` आणि `region.value` आर्ग्युमेंट्स पास करत. अशा प्रकारे, तुम्ही प्रारंभिक फॉर्मद्वारे आणलेल्या दोन मूल्यांचा उपयोग करता, जेव्हा योग्य फील्ड भरले जातात.

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ तुमची आठवण ताजी करा - मागील धड्यात सेट केलेल्या HTML मध्ये दोन इनपुट फील्ड्स आहेत, ज्यांचे `values` तुम्ही फाईलच्या शीर्षस्थानी सेट केलेल्या `const` द्वारे कॅप्चर केले जातात, आणि ते दोन्ही `required` आहेत, त्यामुळे ब्राउझर वापरकर्त्यांना null मूल्ये इनपुट करण्यापासून थांबवतो.

### वापरकर्ता सेट करा

`setUpUser` फंक्शनकडे वळूया, येथे तुम्ही apiKey आणि regionName साठी लोकल स्टोरेज मूल्ये सेट करता. एक नवीन फंक्शन जोडा:

```JavaScript
function setUpUser(apiKey, regionName) {
	localStorage.setItem('apiKey', apiKey);
	localStorage.setItem('regionName', regionName);
	loading.style.display = 'block';
	errors.textContent = '';
	clearBtn.style.display = 'block';
	//make initial call
	displayCarbonUsage(apiKey, regionName);
}
```

हे फंक्शन API कॉल करताना लोडिंग मेसेज दाखवते. या टप्प्यावर, तुम्ही या ब्राउझर एक्स्टेंशनच्या सर्वात महत्त्वाच्या फंक्शनपर्यंत पोहोचला आहात!

### कार्बन वापर दाखवा

शेवटी, API क्वेरी करण्याची वेळ आली आहे!

पुढे जाण्यापूर्वी, आपण API बद्दल चर्चा करूया. API म्हणजे [Application Programming Interfaces](https://www.webopedia.com/TERM/A/API.html), जे वेब डेव्हलपरच्या टूलबॉक्समधील एक महत्त्वाचा घटक आहे. ते प्रोग्राम्सना एकमेकांशी संवाद साधण्यासाठी मानक मार्ग प्रदान करतात. उदाहरणार्थ, जर तुम्ही डेटाबेस क्वेरी करणार्‍या वेबसाइट तयार करत असाल, तर कदाचित कोणी तुमच्यासाठी API तयार केले असेल. अनेक प्रकारचे API आहेत, परंतु सर्वात लोकप्रिय प्रकारांपैकी एक म्हणजे [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/).

✅ 'REST' म्हणजे 'Representational State Transfer' आणि डेटा मिळवण्यासाठी विविध प्रकारे कॉन्फिगर केलेल्या URL चा वापर करणे. डेव्हलपर्ससाठी उपलब्ध असलेल्या विविध प्रकारच्या API बद्दल थोडे संशोधन करा. तुम्हाला कोणता फॉर्मॅट जास्त आवडतो?

या फंक्शनबद्दल काही महत्त्वाच्या गोष्टी लक्षात घ्या. प्रथम, [`async` कीवर्ड](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) लक्षात घ्या. तुमचे फंक्शन्स असिंक्रोनस पद्धतीने चालतील याची खात्री करण्यासाठी `async` वापरले जाते, म्हणजे डेटा परत येईपर्यंत ते थांबते.

`async` बद्दल एक जलद व्हिडिओ येथे आहे:

[![Async आणि Await प्रॉमिसेस व्यवस्थापित करण्यासाठी](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async आणि Await प्रॉमिसेस व्यवस्थापित करण्यासाठी")

> 🎥 `async/await` बद्दल व्हिडिओसाठी वरील प्रतिमेवर क्लिक करा.

C02Signal API क्वेरी करण्यासाठी एक नवीन फंक्शन तयार करा:

```JavaScript
import axios from '../node_modules/axios';

async function displayCarbonUsage(apiKey, region) {
	try {
		await axios
			.get('https://api.co2signal.com/v1/latest', {
				params: {
					countryCode: region,
				},
				headers: {
					'auth-token': apiKey,
				},
			})
			.then((response) => {
				let CO2 = Math.floor(response.data.data.carbonIntensity);

				//calculateColor(CO2);

				loading.style.display = 'none';
				form.style.display = 'none';
				myregion.textContent = region;
				usage.textContent =
					Math.round(response.data.data.carbonIntensity) + ' grams (grams C02 emitted per kilowatt hour)';
				fossilfuel.textContent =
					response.data.data.fossilFuelPercentage.toFixed(2) +
					'% (percentage of fossil fuels used to generate electricity)';
				results.style.display = 'block';
			});
	} catch (error) {
		console.log(error);
		loading.style.display = 'none';
		results.style.display = 'none';
		errors.textContent = 'Sorry, we have no data for the region you have requested.';
	}
}
```

हे एक मोठे फंक्शन आहे. येथे काय चालले आहे?

- सर्वोत्तम पद्धतींचे अनुसरण करत, तुम्ही `async` कीवर्ड वापरता जेणेकरून हे फंक्शन असिंक्रोनस पद्धतीने वागेल. फंक्शनमध्ये `try/catch` ब्लॉक आहे कारण API डेटा परत करताना प्रॉमिस परत करेल. API प्रतिसाद देण्याच्या गतीवर तुमचे नियंत्रण नसल्यामुळे (कदाचित ते प्रतिसाद देणार नाही!), तुम्हाला ही अनिश्चितता असिंक्रोनस पद्धतीने हाताळावी लागेल.
- तुम्ही co2signal API क्वेरी करत आहात तुमच्या region चा डेटा मिळवण्यासाठी, तुमच्या API Key चा वापर करून. त्या कीचा वापर करण्यासाठी, तुम्हाला तुमच्या हेडर पॅरामीटर्समध्ये ऑथेंटिकेशनचा एक प्रकार वापरावा लागतो.
- एकदा API प्रतिसाद दिल्यावर, त्याच्या प्रतिसाद डेटाचे विविध घटक स्क्रीनच्या त्या भागांना असाइन केले जातात, जे तुम्ही हा डेटा दाखवण्यासाठी सेट केले आहे.
- जर एखादी त्रुटी असेल किंवा कोणताही परिणाम नसेल, तर तुम्ही एरर मेसेज दाखवता.

✅ असिंक्रोनस प्रोग्रामिंग पॅटर्न्स वापरणे तुमच्या टूलबॉक्समधील आणखी एक उपयुक्त साधन आहे. [या प्रकारच्या कोडचे कॉन्फिगरेशन करण्याच्या विविध मार्गांबद्दल](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) वाचा.

अभिनंदन! जर तुम्ही तुमचे एक्स्टेंशन तयार केले (`npm run build`) आणि ते एक्स्टेंशन पॅनमध्ये रिफ्रेश केले, तर तुमचे एक्स्टेंशन कार्यरत आहे! फक्त आयकॉन कार्यरत नाही, आणि तुम्ही ते पुढील धड्यात दुरुस्त कराल.

---

## 🚀 आव्हान

आतापर्यंत या धड्यांमध्ये आपण अनेक प्रकारच्या API बद्दल चर्चा केली आहे. एक वेब API निवडा आणि ते काय ऑफर करते याचा सखोल अभ्यास करा. उदाहरणार्थ, ब्राउझरमध्ये उपलब्ध असलेल्या [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) वर एक नजर टाका. तुमच्या मते, एक उत्कृष्ट API कसे असावे?

## पोस्ट-लेक्चर क्विझ

[पोस्ट-लेक्चर क्विझ](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/26)

## पुनरावलोकन आणि स्व-अभ्यास

या धड्यात तुम्ही LocalStorage आणि API बद्दल शिकलात, जे व्यावसायिक वेब डेव्हलपरसाठी खूप उपयुक्त आहेत. हे दोन घटक एकत्र कसे कार्य करतात याचा विचार करा. अशा प्रकारे वेबसाइट कशी आर्किटेक्ट कराल याचा विचार करा, जी API द्वारे वापरण्यासाठी आयटम्स स्टोअर करेल.

## असाइनमेंट

[API स्वीकारा](assignment.md)

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरे त्रुटी किंवा अचूकतेच्या अभावाने युक्त असू शकतात. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार राहणार नाही.