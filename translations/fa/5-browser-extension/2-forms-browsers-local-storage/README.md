<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e10f168beac4e7b05e30e0eb5c92bf11",
  "translation_date": "2025-08-24T13:09:34+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "fa"
}
-->
# پروژه افزونه مرورگر بخش ۲: فراخوانی یک API، استفاده از Local Storage

## آزمون پیش از درس

[آزمون پیش از درس](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/25)

### مقدمه

در این درس، شما با ارسال فرم افزونه مرورگر خود یک API را فراخوانی کرده و نتایج را در افزونه مرورگر نمایش خواهید داد. علاوه بر این، یاد خواهید گرفت که چگونه می‌توانید داده‌ها را در حافظه محلی مرورگر (Local Storage) برای استفاده و مراجعه در آینده ذخیره کنید.

✅ بخش‌های شماره‌گذاری‌شده در فایل‌های مربوطه را دنبال کنید تا بدانید کجا باید کد خود را قرار دهید.

### تنظیم عناصر برای دستکاری در افزونه:

تا این مرحله، شما HTML مربوط به فرم و `<div>` نتایج را برای افزونه مرورگر خود ساخته‌اید. از اینجا به بعد، باید در فایل `/src/index.js` کار کنید و افزونه خود را به تدریج بسازید. به [درس قبلی](../1-about-browsers/README.md) مراجعه کنید تا پروژه خود را تنظیم کرده و فرآیند ساخت را مرور کنید.

در فایل `index.js` خود، با ایجاد چند متغیر `const` شروع کنید تا مقادیر مرتبط با فیلدهای مختلف را نگه دارید:

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

تمام این فیلدها با استفاده از کلاس CSS که در درس قبلی در HTML تنظیم کرده‌اید، ارجاع داده می‌شوند.

### افزودن شنونده‌ها (Listeners)

در مرحله بعد، شنونده‌های رویداد را به فرم و دکمه پاک‌سازی اضافه کنید تا اگر کاربر فرم را ارسال کرد یا روی دکمه بازنشانی کلیک کرد، عملی انجام شود. همچنین، فراخوانی برای مقداردهی اولیه برنامه را در انتهای فایل اضافه کنید:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ به اختصار استفاده‌شده برای گوش دادن به رویداد ارسال یا کلیک توجه کنید و اینکه چگونه رویداد به توابع handleSubmit یا reset ارسال می‌شود. آیا می‌توانید معادل این اختصار را به صورت طولانی‌تر بنویسید؟ کدام روش را ترجیح می‌دهید؟

### ساخت توابع init() و reset():

اکنون شما باید تابعی که افزونه را مقداردهی اولیه می‌کند، یعنی init()، بسازید:

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

در این تابع، منطق جالبی وجود دارد. با خواندن آن، می‌توانید ببینید چه اتفاقی می‌افتد؟

- دو `const` تنظیم می‌شوند تا بررسی کنند آیا کاربر یک APIKey و کد منطقه را در حافظه محلی ذخیره کرده است یا خیر.
- اگر هر یک از این مقادیر null باشد، فرم را با تغییر سبک آن به 'block' نمایش دهید.
- بخش نتایج، بارگذاری و دکمه پاک‌سازی را مخفی کنید و هر متن خطا را به یک رشته خالی تنظیم کنید.
- اگر کلید و منطقه‌ای وجود داشته باشد، یک روال برای:
  - فراخوانی API برای دریافت داده‌های مصرف کربن
  - مخفی کردن بخش نتایج
  - مخفی کردن فرم
  - نمایش دکمه بازنشانی

قبل از ادامه، مفید است که درباره یک مفهوم بسیار مهم موجود در مرورگرها یاد بگیرید: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage). LocalStorage یک روش مفید برای ذخیره رشته‌ها در مرورگر به صورت جفت `کلید-مقدار` است. این نوع ذخیره‌سازی وب می‌تواند توسط جاوااسکریپت برای مدیریت داده‌ها در مرورگر دستکاری شود. LocalStorage منقضی نمی‌شود، در حالی که SessionStorage، نوع دیگری از ذخیره‌سازی وب، هنگام بسته شدن مرورگر پاک می‌شود. انواع مختلف ذخیره‌سازی مزایا و معایب خاص خود را دارند.

> توجه - افزونه مرورگر شما حافظه محلی مخصوص به خود را دارد؛ پنجره اصلی مرورگر یک نمونه جداگانه است و به طور جداگانه عمل می‌کند.

شما مقدار APIKey خود را به عنوان یک رشته تنظیم می‌کنید، برای مثال، و می‌توانید ببینید که این مقدار در Edge با "بازرسی" یک صفحه وب (می‌توانید روی مرورگر راست کلیک کرده و بازرسی کنید) و رفتن به تب Applications برای مشاهده ذخیره‌سازی تنظیم شده است.

![پنل حافظه محلی](../../../../5-browser-extension/2-forms-browsers-local-storage/images/localstorage.png)

✅ به موقعیت‌هایی فکر کنید که نمی‌خواهید برخی داده‌ها را در LocalStorage ذخیره کنید. به طور کلی، قرار دادن API Keys در LocalStorage ایده بدی است! آیا می‌توانید دلیل آن را ببینید؟ در مورد ما، از آنجا که برنامه ما صرفاً برای یادگیری است و در فروشگاه برنامه منتشر نخواهد شد، از این روش استفاده خواهیم کرد.

توجه کنید که از Web API برای دستکاری LocalStorage استفاده می‌کنید، یا با استفاده از `getItem()`، `setItem()` یا `removeItem()`. این روش به طور گسترده در مرورگرها پشتیبانی می‌شود.

قبل از ساخت تابع `displayCarbonUsage()` که در `init()` فراخوانی می‌شود، بیایید عملکردی برای مدیریت ارسال اولیه فرم بسازیم.

### مدیریت ارسال فرم

یک تابع به نام `handleSubmit` ایجاد کنید که یک آرگومان رویداد `(e)` را می‌پذیرد. از انتشار رویداد جلوگیری کنید (در این مورد، می‌خواهیم از تازه‌سازی مرورگر جلوگیری کنیم) و یک تابع جدید به نام `setUpUser` را فراخوانی کنید و آرگومان‌های `apiKey.value` و `region.value` را به آن ارسال کنید. به این ترتیب، از دو مقداری که از طریق فرم اولیه وارد شده‌اند استفاده می‌کنید.

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ حافظه خود را تازه کنید - HTML که در درس قبلی تنظیم کرده‌اید دارای دو فیلد ورودی است که `مقادیر` آنها از طریق `const` که در بالای فایل تنظیم کرده‌اید، گرفته می‌شود و هر دو `required` هستند، بنابراین مرورگر از وارد کردن مقادیر null توسط کاربران جلوگیری می‌کند.

### تنظیم کاربر

به تابع `setUpUser` بروید، در اینجا مقادیر حافظه محلی برای apiKey و regionName تنظیم می‌شوند. یک تابع جدید اضافه کنید:

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

این تابع یک پیام بارگذاری را برای نمایش در حین فراخوانی API تنظیم می‌کند. در این مرحله، شما به مهم‌ترین تابع این افزونه مرورگر رسیده‌اید!

### نمایش مصرف کربن

در نهایت، زمان آن رسیده که API را پرس‌وجو کنید!

قبل از ادامه، باید درباره APIها صحبت کنیم. APIها یا [رابط‌های برنامه‌نویسی کاربردی](https://www.webopedia.com/TERM/A/API.html)، یک عنصر حیاتی در جعبه ابزار یک توسعه‌دهنده وب هستند. آنها روش‌های استانداردی برای برنامه‌ها فراهم می‌کنند تا با یکدیگر تعامل و ارتباط برقرار کنند. برای مثال، اگر در حال ساخت یک وب‌سایت هستید که نیاز به پرس‌وجو از یک پایگاه داده دارد، ممکن است کسی یک API برای شما ایجاد کرده باشد. در حالی که انواع مختلفی از APIها وجود دارد، یکی از محبوب‌ترین آنها [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/) است.

✅ اصطلاح 'REST' مخفف 'Representational State Transfer' است و شامل استفاده از URLهای مختلف برای دریافت داده‌ها می‌شود. کمی تحقیق کنید درباره انواع مختلف APIهایی که برای توسعه‌دهندگان در دسترس هستند. کدام فرمت برای شما جذاب‌تر است؟

چند نکته مهم درباره این تابع وجود دارد. ابتدا، به کلمه کلیدی [`async`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) توجه کنید. نوشتن توابع به گونه‌ای که به صورت ناهمگام اجرا شوند به این معناست که آنها منتظر یک عمل، مانند بازگشت داده‌ها، می‌مانند تا قبل از ادامه کار تکمیل شود.

در اینجا یک ویدیو کوتاه درباره `async` وجود دارد:

[![Async و Await برای مدیریت وعده‌ها](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async و Await برای مدیریت وعده‌ها")

> 🎥 روی تصویر بالا کلیک کنید تا ویدیویی درباره async/await ببینید.

یک تابع جدید برای پرس‌وجو از API C02Signal ایجاد کنید:

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

این یک تابع بزرگ است. چه اتفاقی در اینجا می‌افتد؟

- با پیروی از بهترین شیوه‌ها، از کلمه کلیدی `async` استفاده می‌کنید تا این تابع به صورت ناهمگام عمل کند. این تابع شامل یک بلوک `try/catch` است زیرا هنگام بازگشت داده‌ها از API یک وعده بازمی‌گرداند. از آنجا که شما کنترلی بر سرعت پاسخ API ندارید (ممکن است اصلاً پاسخ ندهد!)، باید این عدم قطعیت را با فراخوانی آن به صورت ناهمگام مدیریت کنید.
- شما API co2signal را برای دریافت داده‌های منطقه خود پرس‌وجو می‌کنید و از کلید API خود استفاده می‌کنید. برای استفاده از آن کلید، باید نوعی احراز هویت را در پارامترهای هدر خود قرار دهید.
- هنگامی که API پاسخ می‌دهد، عناصر مختلف داده‌های پاسخ آن را به بخش‌هایی از صفحه که برای نمایش این داده‌ها تنظیم کرده‌اید، اختصاص می‌دهید.
- اگر خطایی وجود داشته باشد یا نتیجه‌ای نباشد، یک پیام خطا نمایش می‌دهید.

✅ استفاده از الگوهای برنامه‌نویسی ناهمگام ابزار بسیار مفیدی در جعبه ابزار شماست. [درباره روش‌های مختلف](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) پیکربندی این نوع کد مطالعه کنید.

تبریک می‌گویم! اگر افزونه خود را بسازید (`npm run build`) و آن را در پنل افزونه‌ها تازه‌سازی کنید، یک افزونه کاربردی خواهید داشت! تنها چیزی که کار نمی‌کند، آیکون است و آن را در درس بعدی درست خواهید کرد.

---

## 🚀 چالش

ما تاکنون درباره چند نوع API در این درس‌ها صحبت کرده‌ایم. یک API وب انتخاب کنید و به طور عمیق تحقیق کنید که چه امکاناتی ارائه می‌دهد. برای مثال، به APIهای موجود در مرورگرها مانند [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API) نگاهی بیندازید. به نظر شما چه چیزی یک API عالی را می‌سازد؟

## آزمون پس از درس

[آزمون پس از درس](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/26)

## مرور و مطالعه شخصی

شما در این درس درباره LocalStorage و APIها یاد گرفتید، هر دو برای یک توسعه‌دهنده وب حرفه‌ای بسیار مفید هستند. آیا می‌توانید به این فکر کنید که چگونه این دو با هم کار می‌کنند؟ به این فکر کنید که چگونه یک وب‌سایت طراحی می‌کنید که آیتم‌هایی را برای استفاده توسط یک API ذخیره کند.

## تکلیف

[پذیرش یک API](assignment.md)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم دقت را حفظ کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.