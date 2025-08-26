<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e10f168beac4e7b05e30e0eb5c92bf11",
  "translation_date": "2025-08-25T23:28:26+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "ur"
}
-->
# براؤزر ایکسٹینشن پروجیکٹ حصہ 2: API کال کریں، لوکل اسٹوریج استعمال کریں

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/25)

### تعارف

اس سبق میں، آپ اپنے براؤزر ایکسٹینشن کے فارم کے ذریعے ایک API کال کریں گے اور نتائج کو براؤزر ایکسٹینشن میں دکھائیں گے۔ اس کے علاوہ، آپ یہ بھی سیکھیں گے کہ کس طرح ڈیٹا کو براؤزر کے لوکل اسٹوریج میں محفوظ کیا جا سکتا ہے تاکہ مستقبل میں اس کا حوالہ دیا جا سکے اور استعمال کیا جا سکے۔

✅ مناسب فائلوں میں نمبر شدہ حصوں کی پیروی کریں تاکہ آپ کو معلوم ہو کہ کوڈ کہاں رکھنا ہے۔

### ایکسٹینشن میں عناصر کو ترتیب دیں:

اس وقت تک آپ نے اپنے براؤزر ایکسٹینشن کے لیے فارم اور نتائج کے `<div>` کے لیے HTML بنا لیا ہوگا۔ اب سے، آپ کو `/src/index.js` فائل میں کام کرنا ہوگا اور اپنی ایکسٹینشن کو تھوڑا تھوڑا بنا کر مکمل کرنا ہوگا۔ [پچھلے سبق](../1-about-browsers/README.md) کا حوالہ دیں تاکہ آپ اپنے پروجیکٹ کو ترتیب دینے اور بلڈ پروسیس کے بارے میں جان سکیں۔

اپنی `index.js` فائل میں کام کرتے ہوئے، کچھ `const` ویریبلز بنائیں تاکہ مختلف فیلڈز سے وابستہ ویلیوز کو محفوظ کیا جا سکے:

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

یہ تمام فیلڈز ان کے CSS کلاس کے ذریعے حوالہ دیے گئے ہیں، جیسا کہ آپ نے پچھلے سبق میں HTML میں ترتیب دیا تھا۔

### لسٹنرز شامل کریں

اگلے مرحلے میں، فارم اور کلئیر بٹن کے لیے ایونٹ لسٹنرز شامل کریں جو فارم کو ری سیٹ کرتا ہے، تاکہ اگر کوئی صارف فارم جمع کرے یا ری سیٹ بٹن پر کلک کرے تو کچھ ہو۔ فائل کے آخر میں ایپ کو انیشیالائز کرنے کے لیے کال شامل کریں:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ نوٹ کریں کہ سبمٹ یا کلک ایونٹ سننے کے لیے شارٹ ہینڈ استعمال کیا گیا ہے، اور کس طرح ایونٹ کو `handleSubmit` یا `reset` فنکشنز میں پاس کیا جاتا ہے۔ کیا آپ اس شارٹ ہینڈ کا طویل فارمیٹ میں مساوی لکھ سکتے ہیں؟ آپ کو کون سا فارمیٹ زیادہ پسند ہے؟

### `init()` اور `reset()` فنکشنز کو بنائیں:

اب آپ ایکسٹینشن کو انیشیالائز کرنے والے فنکشن کو بنائیں گے، جسے `init()` کہا جاتا ہے:

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

اس فنکشن میں کچھ دلچسپ منطق موجود ہے۔ اسے پڑھتے ہوئے، کیا آپ دیکھ سکتے ہیں کہ کیا ہو رہا ہے؟

- دو `const` ویریبلز ترتیب دیے گئے ہیں تاکہ چیک کیا جا سکے کہ آیا صارف نے لوکل اسٹوریج میں APIKey اور ریجن کوڈ محفوظ کیا ہے۔
- اگر ان میں سے کوئی بھی `null` ہو، تو فارم کو 'block' کے طور پر دکھائیں۔
- نتائج، لوڈنگ، اور `clearBtn` کو چھپائیں اور کسی بھی ایرر ٹیکسٹ کو خالی سٹرنگ پر سیٹ کریں۔
- اگر کوئی key اور region موجود ہو، تو ایک روٹین شروع کریں:
  - API کو کاربن یوزج ڈیٹا حاصل کرنے کے لیے کال کریں۔
  - نتائج کے علاقے کو چھپائیں۔
  - فارم کو چھپائیں۔
  - ری سیٹ بٹن دکھائیں۔

آگے بڑھنے سے پہلے، براؤزرز میں دستیاب ایک بہت اہم تصور کے بارے میں سیکھنا مفید ہے: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage)۔ لوکل اسٹوریج براؤزر میں سٹرنگز کو `key-value` پیر کے طور پر محفوظ کرنے کا ایک مفید طریقہ ہے۔ اس قسم کے ویب اسٹوریج کو جاوا اسکرپٹ کے ذریعے براؤزر میں ڈیٹا کو منظم کرنے کے لیے استعمال کیا جا سکتا ہے۔ لوکل اسٹوریج ختم نہیں ہوتا، جبکہ سیشن اسٹوریج، ایک اور قسم کا ویب اسٹوریج، براؤزر بند ہونے پر صاف ہو جاتا ہے۔ مختلف قسم کے اسٹوریج کے استعمال کے فوائد اور نقصانات ہیں۔

> نوٹ - آپ کے براؤزر ایکسٹینشن کا اپنا لوکل اسٹوریج ہوتا ہے؛ مین براؤزر ونڈو ایک الگ انسٹینس ہے اور الگ سے کام کرتی ہے۔

آپ اپنے APIKey کو ایک سٹرنگ ویلیو پر سیٹ کرتے ہیں، مثال کے طور پر، اور آپ دیکھ سکتے ہیں کہ یہ ایج پر کیسے سیٹ کیا گیا ہے جب آپ کسی ویب پیج کو "انسپیکٹ" کرتے ہیں (آپ براؤزر پر رائٹ کلک کر کے انسپیکٹ کر سکتے ہیں) اور ایپلیکیشنز ٹیب پر جا کر اسٹوریج دیکھ سکتے ہیں۔

![لوکل اسٹوریج پین](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.ur.png)

✅ ان حالات کے بارے میں سوچیں جہاں آپ لوکل اسٹوریج میں کچھ ڈیٹا محفوظ نہیں کرنا چاہیں گے۔ عام طور پر، APIKeys کو لوکل اسٹوریج میں رکھنا ایک برا خیال ہے! کیا آپ دیکھ سکتے ہیں کیوں؟ ہمارے کیس میں، چونکہ ہماری ایپ صرف سیکھنے کے لیے ہے اور ایپ اسٹور میں ڈپلائے نہیں ہوگی، ہم اس طریقے کو استعمال کریں گے۔

نوٹ کریں کہ آپ لوکل اسٹوریج کو Web API کے ذریعے منظم کرتے ہیں، یا تو `getItem()`، `setItem()`، یا `removeItem()` استعمال کر کے۔ یہ براؤزرز میں وسیع پیمانے پر سپورٹڈ ہے۔

اس سے پہلے کہ آپ `displayCarbonUsage()` فنکشن بنائیں جو `init()` میں کال کیا جاتا ہے، آئیے ابتدائی فارم سبمیشن کو ہینڈل کرنے کی فعالیت بنائیں۔

### فارم سبمیشن کو ہینڈل کریں

ایک فنکشن بنائیں جسے `handleSubmit` کہا جاتا ہے جو ایک ایونٹ آرگومنٹ `(e)` قبول کرتا ہے۔ ایونٹ کو پھیلنے سے روکیں (اس کیس میں، ہم براؤزر کو ریفریش ہونے سے روکنا چاہتے ہیں) اور ایک نیا فنکشن `setUpUser` کو کال کریں، جس میں `apiKey.value` اور `region.value` آرگومنٹس پاس کریں۔ اس طرح، آپ ان دو ویلیوز کو استعمال کرتے ہیں جو ابتدائی فارم کے ذریعے لائی جاتی ہیں جب مناسب فیلڈز کو پاپولیٹ کیا جاتا ہے۔

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ اپنی یادداشت تازہ کریں - پچھلے سبق میں آپ نے جو HTML ترتیب دیا تھا اس میں دو ان پٹ فیلڈز ہیں جن کی `values` کو آپ نے فائل کے اوپر سیٹ کیے گئے `const` کے ذریعے کیپچر کیا ہے، اور وہ دونوں `required` ہیں تاکہ براؤزر صارفین کو null ویلیوز ان پٹ کرنے سے روک سکے۔

### صارف کو ترتیب دیں

`setUpUser` فنکشن کی طرف بڑھتے ہوئے، یہاں آپ لوکل اسٹوریج ویلیوز کو `apiKey` اور `regionName` کے لیے سیٹ کرتے ہیں۔ ایک نیا فنکشن شامل کریں:

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

یہ فنکشن ایک لوڈنگ میسج کو دکھاتا ہے جب تک کہ API کو کال کیا جا رہا ہو۔ اس وقت، آپ اس براؤزر ایکسٹینشن کے سب سے اہم فنکشن کو بنانے کے مرحلے پر پہنچ چکے ہیں!

### کاربن یوزج دکھائیں

آخر کار، API کو کوئری کرنے کا وقت آ گیا ہے!

آگے بڑھنے سے پہلے، ہمیں APIs پر بات کرنی چاہیے۔ APIs، یا [ایپلیکیشن پروگرامنگ انٹرفیسز](https://www.webopedia.com/TERM/A/API.html)، ویب ڈیولپر کے ٹول باکس کا ایک اہم عنصر ہیں۔ یہ پروگرامز کو ایک دوسرے کے ساتھ انٹرفیس کرنے کے لیے معیاری طریقے فراہم کرتے ہیں۔ مثال کے طور پر، اگر آپ ایک ویب سائٹ بنا رہے ہیں جسے ڈیٹا بیس کو کوئری کرنے کی ضرورت ہے، تو کوئی آپ کے لیے ایک API بنا سکتا ہے۔ جبکہ APIs کی بہت سی اقسام ہیں، ان میں سے ایک مقبول قسم [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/) ہے۔

✅ 'REST' کا مطلب 'Representational State Transfer' ہے اور مختلف طریقے سے ترتیب دیے گئے URLs کا استعمال کرتے ہوئے ڈیٹا حاصل کرنے کی خصوصیت رکھتا ہے۔ ڈیولپرز کے لیے دستیاب مختلف قسم کے APIs پر تھوڑا سا تحقیق کریں۔ آپ کو کون سا فارمیٹ زیادہ پسند ہے؟

اس فنکشن کے بارے میں اہم باتیں نوٹ کریں۔ سب سے پہلے، [`async` کی ورڈ](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) پر غور کریں۔ اپنے فنکشنز کو اس طرح لکھنا کہ وہ غیر متزامن طور پر چلیں، اس کا مطلب ہے کہ وہ کسی ایکشن، جیسے ڈیٹا کے واپس آنے، کے مکمل ہونے کا انتظار کرتے ہیں اس سے پہلے کہ وہ آگے بڑھیں۔

یہاں `async` کے بارے میں ایک مختصر ویڈیو ہے:

[![Async اور Await کے ذریعے پرومسز کو منظم کرنا](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async اور Await کے ذریعے پرومسز کو منظم کرنا")

> 🎥 اوپر دی گئی تصویر پر کلک کریں `async/await` کے بارے میں ویڈیو دیکھنے کے لیے۔

C02Signal API کو کوئری کرنے کے لیے ایک نیا فنکشن بنائیں:

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

یہ ایک بڑا فنکشن ہے۔ یہاں کیا ہو رہا ہے؟

- بہترین طریقوں پر عمل کرتے ہوئے، آپ `async` کی ورڈ استعمال کرتے ہیں تاکہ یہ فنکشن غیر متزامن طور پر کام کرے۔ فنکشن میں ایک `try/catch` بلاک شامل ہے کیونکہ یہ API کے ڈیٹا واپس کرنے پر ایک پرومس واپس کرے گا۔ چونکہ آپ کے پاس API کے جواب دینے کی رفتار پر کنٹرول نہیں ہے (یہ بالکل جواب نہیں دے سکتا)، آپ کو اس غیر یقینی صورتحال کو غیر متزامن طور پر کال کر کے ہینڈل کرنا ہوگا۔
- آپ co2signal API کو اپنے ریجن کا ڈیٹا حاصل کرنے کے لیے کوئری کر رہے ہیں، اپنے API Key کا استعمال کرتے ہوئے۔ اس key کو استعمال کرنے کے لیے، آپ کو اپنے ہیڈر پیرامیٹرز میں ایک قسم کی تصدیق کا استعمال کرنا ہوگا۔
- ایک بار جب API جواب دیتا ہے، آپ اس کے جواب کے مختلف عناصر کو اپنی اسکرین کے ان حصوں میں تفویض کرتے ہیں جنہیں آپ نے یہ ڈیٹا دکھانے کے لیے ترتیب دیا ہے۔
- اگر کوئی ایرر ہو، یا کوئی نتیجہ نہ ہو، تو آپ ایک ایرر میسج دکھاتے ہیں۔

✅ غیر متزامن پروگرامنگ پیٹرنز کا استعمال آپ کے ٹول باکس میں ایک اور بہت مفید ٹول ہے۔ [مختلف طریقوں](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) کے بارے میں پڑھیں جن سے آپ اس قسم کے کوڈ کو ترتیب دے سکتے ہیں۔

مبارک ہو! اگر آپ اپنی ایکسٹینشن کو بلڈ کریں (`npm run build`) اور اسے اپنی ایکسٹینشنز پین میں ریفریش کریں، تو آپ کے پاس ایک کام کرنے والی ایکسٹینشن ہے! واحد چیز جو کام نہیں کر رہی وہ آئیکن ہے، اور آپ اسے اگلے سبق میں ٹھیک کریں گے۔

---

## 🚀 چیلنج

ہم نے ان اسباق میں اب تک کئی قسم کے APIs پر بات کی ہے۔ ایک ویب API کا انتخاب کریں اور گہرائی میں تحقیق کریں کہ یہ کیا پیش کرتا ہے۔ مثال کے طور پر، براؤزرز میں دستیاب APIs جیسے [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) کو دیکھیں۔ آپ کے خیال میں ایک بہترین API کیا چیز بناتی ہے؟

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/26)

## جائزہ اور خود مطالعہ

آپ نے اس سبق میں لوکل اسٹوریج اور APIs کے بارے میں سیکھا، جو پیشہ ور ویب ڈیولپر کے لیے بہت مفید ہیں۔ کیا آپ سوچ سکتے ہیں کہ یہ دونوں چیزیں ایک ساتھ کیسے کام کرتی ہیں؟ سوچیں کہ آپ ایک ایسی ویب سائٹ کو کیسے آرکیٹیکٹ کریں گے جو ایک API کے ذریعے استعمال ہونے والی اشیاء کو محفوظ کرے۔

## اسائنمنٹ

[ایک API اپنائیں](assignment.md)

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔