<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e10f168beac4e7b05e30e0eb5c92bf11",
  "translation_date": "2025-08-25T23:30:33+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "ne"
}
-->
# ब्राउजर एक्स्टेन्सन प्रोजेक्ट भाग २: API कल गर्नुहोस्, लोकल स्टोरेज प्रयोग गर्नुहोस्

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/25)

### परिचय

यस पाठमा, तपाईं आफ्नो ब्राउजर एक्स्टेन्सनको फारम सबमिट गरेर API कल गर्नुहुनेछ र नतिजाहरू ब्राउजर एक्स्टेन्सनमा देखाउनुहुनेछ। साथै, तपाईं आफ्नो ब्राउजरको लोकल स्टोरेजमा डाटा भविष्यको लागि कसरी भण्डारण गर्न सकिन्छ भन्ने कुरा पनि सिक्नुहुनेछ।

✅ कोड कहाँ राख्ने भनेर जान्नको लागि उपयुक्त फाइलहरूमा क्रमांकित खण्डहरू पालना गर्नुहोस्।

### एक्स्टेन्सनमा परिवर्तन गर्नका लागि तत्वहरू सेट गर्नुहोस्:

यस समयसम्म तपाईंले आफ्नो ब्राउजर एक्स्टेन्सनको फारम र नतिजाहरूको `<div>` को लागि HTML बनाइसक्नुभएको छ। अबदेखि, तपाईंले `/src/index.js` फाइलमा काम गर्नुपर्नेछ र आफ्नो एक्स्टेन्सनलाई क्रमशः निर्माण गर्नुपर्नेछ। आफ्नो प्रोजेक्ट सेटअप र निर्माण प्रक्रियाको लागि [अघिल्लो पाठ](../1-about-browsers/README.md) हेर्नुहोस्।

`index.js` फाइलमा काम गर्दै, विभिन्न फिल्डहरूसँग सम्बन्धित मानहरू समात्नका लागि केही `const` भेरिएबलहरू सिर्जना गरेर सुरु गर्नुहोस्:

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

यी सबै फिल्डहरू CSS क्लासद्वारा सन्दर्भित छन्, जुन तपाईंले अघिल्लो पाठमा HTML मा सेट गर्नुभएको थियो।

### लिस्नरहरू थप्नुहोस्

अब, फारम र रिसेट बटनमा इभेन्ट लिस्नरहरू थप्नुहोस् जसले फारम सबमिट गर्दा वा रिसेट बटन क्लिक गर्दा केही कार्य गर्दछ, र फाइलको अन्त्यमा एप्लिकेसनलाई इनिसियलाइज गर्ने कल थप्नुहोस्:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ ध्यान दिनुहोस्, सबमिट वा क्लिक इभेन्ट सुन्नको लागि प्रयोग गरिएको छोटो तरिका, र कसरी इभेन्टलाई `handleSubmit` वा `reset` फङ्सनमा पास गरिन्छ। के तपाईं यो छोटो तरिकाको लामो संस्करण लेख्न सक्नुहुन्छ? कुन तरिका तपाईंलाई मन पर्छ?

### `init()` र `reset()` फङ्सन निर्माण गर्नुहोस्:

अब तपाईं एक्स्टेन्सनलाई इनिसियलाइज गर्ने फङ्सन निर्माण गर्दै हुनुहुन्छ, जसलाई `init()` भनिन्छ:

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

यस फङ्सनमा केही रोचक तर्कहरू छन्। यसलाई पढ्दा, के हुन्छ भनेर बुझ्न सक्नुहुन्छ?

- दुई `const` सेटअप गरिन्छ, जसले जाँच गर्छ कि प्रयोगकर्ताले लोकल स्टोरेजमा APIKey र क्षेत्र कोड भण्डारण गरेका छन् कि छैनन्।
- यदि यीमध्ये कुनै पनि `null` छ भने, फारमलाई 'block' शैलीमा देखाउनुहोस्।
- नतिजाहरू, लोडिङ, र `clearBtn` लुकाउनुहोस् र कुनै पनि त्रुटि पाठलाई खाली स्ट्रिङमा सेट गर्नुहोस्।
- यदि कुञ्जी र क्षेत्र छ भने, निम्न कार्य सुरु गर्नुहोस्:
  - API कल गरेर कार्बन प्रयोगको डाटा प्राप्त गर्नुहोस्।
  - नतिजा क्षेत्र लुकाउनुहोस्।
  - फारम लुकाउनुहोस्।
  - रिसेट बटन देखाउनुहोस्।

अगाडि बढ्नु अघि, ब्राउजरमा उपलब्ध एक महत्त्वपूर्ण अवधारणाबारे सिक्नु उपयोगी हुन्छ: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)। LocalStorage ब्राउजरमा `key-value` जोडीको रूपमा स्ट्रिङहरू भण्डारण गर्न उपयोगी तरिका हो। यो प्रकारको वेब स्टोरेजलाई ब्राउजरमा डाटा व्यवस्थापन गर्न JavaScript द्वारा हेरफेर गर्न सकिन्छ। LocalStorage कहिल्यै समाप्त हुँदैन, जबकि SessionStorage, अर्को प्रकारको वेब स्टोरेज, ब्राउजर बन्द हुँदा खाली हुन्छ। विभिन्न प्रकारका स्टोरेजको प्रयोगका लागि फाइदा र बेफाइदा छन्।

> नोट - तपाईंको ब्राउजर एक्स्टेन्सनको आफ्नै लोकल स्टोरेज छ; मुख्य ब्राउजर विन्डो भने फरक इन्स्टेन्स हो र अलग व्यवहार गर्दछ।

तपाईंले आफ्नो APIKey लाई स्ट्रिङ मान दिनुहुन्छ, उदाहरणका लागि, र तपाईंले Edge मा यो सेट भएको देख्न सक्नुहुन्छ, वेब पेजलाई "inspect" गरेर (ब्राउजरमा राइट-क्लिक गरेर inspect गर्न सकिन्छ) र Applications ट्याबमा गएर स्टोरेज हेर्न सकिन्छ।

![लोकल स्टोरेज प्यान](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.ne.png)

✅ सोच्नुहोस्, कुन अवस्थामा तपाईंले लोकल स्टोरेजमा केही डाटा भण्डारण गर्न नचाहनुहुनेछ। सामान्यतया, लोकल स्टोरेजमा API कुञ्जीहरू राख्नु खराब विचार हो! किन हो, तपाईं देख्न सक्नुहुन्छ? हाम्रो केसमा, किनभने हाम्रो एप केवल सिकाइका लागि हो र एप स्टोरमा तैनाथ हुने छैन, हामी यो विधि प्रयोग गर्नेछौं।

ध्यान दिनुहोस्, तपाईंले लोकल स्टोरेजलाई हेरफेर गर्न Web API प्रयोग गर्नुहुन्छ, `getItem()`, `setItem()`, वा `removeItem()` प्रयोग गरेर। यो ब्राउजरहरूमा व्यापक रूपमा समर्थित छ।

`displayCarbonUsage()` फङ्सन निर्माण गर्नु अघि, जुन `init()` मा कल गरिएको छ, सुरुमा फारम सबमिशन ह्यान्डल गर्ने कार्यक्षमता निर्माण गरौं।

### फारम सबमिशन ह्यान्डल गर्नुहोस्

`handleSubmit` नामक फङ्सन सिर्जना गर्नुहोस्, जसले `(e)` इभेन्ट आर्गुमेन्ट स्वीकार्छ। इभेन्टलाई फैलिनबाट रोक्नुहोस् (यस अवस्थामा, हामी ब्राउजरलाई रिफ्रेस हुनबाट रोक्न चाहन्छौं) र नयाँ फङ्सन `setUpUser` कल गर्नुहोस्, जसमा `apiKey.value` र `region.value` आर्गुमेन्ट पास गर्नुहोस्। यसरी, तपाईंले प्रारम्भिक फारमबाट ल्याइएका दुई मानहरू प्रयोग गर्नुहुन्छ, जब उपयुक्त फिल्डहरू भरिएका हुन्छन्।

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ आफ्नो स्मरण ताजा गर्नुहोस् - अघिल्लो पाठमा सेट गरिएको HTML मा दुई इनपुट फिल्डहरू छन्, जसको `values` माथि सेट गरिएको `const` द्वारा समातिन्छ, र ती दुवै `required` छन्, जसले ब्राउजरलाई प्रयोगकर्ताहरूलाई `null` मानहरू इनपुट गर्नबाट रोक्छ।

### प्रयोगकर्ता सेट गर्नुहोस्

`setUpUser` फङ्सनतर्फ अगाडि बढ्दै, यहाँ तपाईंले लोकल स्टोरेज मानहरू `apiKey` र `regionName` का लागि सेट गर्नुहुन्छ। नयाँ फङ्सन थप्नुहोस्:

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

यो फङ्सनले API कल गर्दा देखिने लोडिङ सन्देश सेट गर्दछ। यस बिन्दुमा, तपाईं आफ्नो ब्राउजर एक्स्टेन्सनको सबैभन्दा महत्त्वपूर्ण फङ्सन सिर्जना गर्न आइपुग्नुभएको छ!

### कार्बन प्रयोग देखाउनुहोस्

अन्ततः, API क्वेरी गर्ने समय आएको छ!

अगाडि बढ्नु अघि, हामीले API हरूबारे छलफल गर्नुपर्छ। API हरू, वा [Application Programming Interfaces](https://www.webopedia.com/TERM/A/API.html), वेब विकासकर्ताको उपकरणको महत्त्वपूर्ण तत्व हो। तिनीहरूले प्रोग्रामहरूलाई एकअर्कासँग अन्तरक्रिया गर्न र इन्टरफेस गर्न मानक तरिकाहरू प्रदान गर्छन्। उदाहरणका लागि, यदि तपाईंले डेटाबेस क्वेरी गर्नुपर्ने वेबसाइट निर्माण गर्दै हुनुहुन्छ भने, कसैले तपाईंलाई प्रयोग गर्नको लागि API सिर्जना गरेको हुन सक्छ। धेरै प्रकारका API हरू छन्, तर सबैभन्दा लोकप्रियमध्ये एक हो [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)।

✅ 'REST' को अर्थ 'Representational State Transfer' हो र यसले विभिन्न प्रकारका URL हरू प्रयोग गरेर डाटा ल्याउने सुविधा दिन्छ। विकासकर्ताहरूलाई उपलब्ध विभिन्न प्रकारका API हरूबारे थोरै अनुसन्धान गर्नुहोस्। कुन ढाँचा तपाईंलाई मन पर्छ?

यस फङ्सनका महत्त्वपूर्ण कुराहरू नोट गर्नुहोस्। पहिलो, [`async` कीवर्ड](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) लाई ध्यान दिनुहोस्। तपाईंको फङ्सनहरूलाई असिन्क्रोनस रूपमा चल्ने बनाउनाले तिनीहरूले कुनै कार्य, जस्तै डाटा फर्कने, पूरा नभएसम्म पर्खन्छन्।

`async` को बारेमा छोटो भिडियो यहाँ छ:

[![Async र Await द्वारा प्रबन्धित प्रॉमिसहरू](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async र Await द्वारा प्रबन्धित प्रॉमिसहरू")

> 🎥 माथिको छविमा क्लिक गरेर `async/await` को बारेमा भिडियो हेर्नुहोस्।

C02Signal API क्वेरी गर्न नयाँ फङ्सन सिर्जना गर्नुहोस्:

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

यो ठूलो फङ्सन हो। यहाँ के भइरहेको छ?

- राम्रो अभ्यासहरू पालना गर्दै, तपाईंले यो फङ्सनलाई असिन्क्रोनस बनाउन `async` कीवर्ड प्रयोग गर्नुभएको छ। फङ्सनले `try/catch` ब्लक समावेश गर्दछ, किनभने यो API ले डाटा फर्काउँदा प्रॉमिस फर्काउँछ। किनभने तपाईंले API ले कति छिटो प्रतिक्रिया दिनेछ भन्ने नियन्त्रण गर्न सक्नुहुन्न (यो प्रतिक्रिया नदिन पनि सक्छ!), तपाईंले यो अनिश्चिततालाई असिन्क्रोनस रूपमा कल गरेर ह्यान्डल गर्नुपर्छ।
- तपाईं co2signal API लाई आफ्नो क्षेत्रको डाटा प्राप्त गर्न क्वेरी गर्दै हुनुहुन्छ, आफ्नो API कुञ्जी प्रयोग गरेर। त्यो कुञ्जी प्रयोग गर्न, तपाईंले आफ्नो हेडर प्यारामिटरहरूमा एक प्रकारको प्रमाणीकरण प्रयोग गर्नुपर्छ।
- एकपटक API ले प्रतिक्रिया दिएपछि, तपाईंले यसको प्रतिक्रिया डाटाका विभिन्न तत्वहरूलाई आफ्नो स्क्रिनका भागहरूमा असाइन गर्नुहुन्छ, जुन तपाईंले यो डाटा देखाउन सेट गर्नुभएको थियो।
- यदि कुनै त्रुटि छ, वा कुनै नतिजा छैन भने, तपाईंले त्रुटि सन्देश देखाउनुहुन्छ।

✅ असिन्क्रोनस प्रोग्रामिङ ढाँचाहरू प्रयोग गर्नु तपाईंको उपकरणको अर्को धेरै उपयोगी उपकरण हो। [यस प्रकारको कोड कन्फिगर गर्न सकिने विभिन्न तरिकाहरू](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) को बारेमा पढ्नुहोस्।

बधाई छ! यदि तपाईंले आफ्नो एक्स्टेन्सन निर्माण गर्नुभयो (`npm run build`) र यसलाई आफ्नो एक्स्टेन्सन प्यानमा रिफ्रेस गर्नुभयो भने, तपाईंको एक्स्टेन्सन काम गरिरहेको छ! केवल आइकन काम गरिरहेको छैन, र तपाईंले यो अर्को पाठमा समाधान गर्नुहुनेछ।

---

## 🚀 चुनौती

हामीले यी पाठहरूमा अहिलेसम्म विभिन्न प्रकारका API हरूबारे छलफल गरिसकेका छौं। कुनै वेब API छान्नुहोस् र यसले के प्रस्ताव गर्दछ भन्ने कुरा गहिरो रूपमा अनुसन्धान गर्नुहोस्। उदाहरणका लागि, ब्राउजरभित्र उपलब्ध API हरू जस्तै [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) हेर्नुहोस्। तपाईंको विचारमा, केले राम्रो API बनाउँछ?

## पोस्ट-लेक्चर क्विज

[पोस्ट-लेक्चर क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/26)

## समीक्षा र आत्म-अध्ययन

यस पाठमा तपाईंले LocalStorage र API हरूबारे सिक्नुभयो, जुन व्यावसायिक वेब विकासकर्ताका लागि धेरै उपयोगी छन्। यी दुई चीजहरू कसरी सँगै काम गर्छन् भनेर सोच्न सक्नुहुन्छ? तपाईंले API द्वारा प्रयोग गरिने वस्तुहरू भण्डारण गर्ने वेबसाइट कसरी आर्किटेक्चर गर्नुहुन्छ भनेर सोच्नुहोस्।

## असाइनमेन्ट

[API अपनाउनुहोस्](assignment.md)

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।