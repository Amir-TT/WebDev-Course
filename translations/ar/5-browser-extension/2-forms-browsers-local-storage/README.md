<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e10f168beac4e7b05e30e0eb5c92bf11",
  "translation_date": "2025-08-25T23:28:03+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "ar"
}
-->
# مشروع إضافة المتصفح الجزء الثاني: استدعاء API واستخدام التخزين المحلي

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/25)

### المقدمة

في هذه الدرس، ستقوم باستدعاء API من خلال إرسال نموذج إضافة المتصفح الخاص بك وعرض النتائج داخل الإضافة. بالإضافة إلى ذلك، ستتعلم كيفية تخزين البيانات في التخزين المحلي للمتصفح لاستخدامها لاحقًا.

✅ اتبع الأجزاء المرقمة في الملفات المناسبة لمعرفة أين تضع الكود الخاص بك.

### إعداد العناصر للتعامل معها داخل الإضافة:

في هذه المرحلة، قمت ببناء HTML للنموذج و`<div>` الخاص بالنتائج لإضافة المتصفح. من الآن فصاعدًا، ستحتاج إلى العمل في ملف `/src/index.js` وبناء الإضافة خطوة بخطوة. ارجع إلى [الدرس السابق](../1-about-browsers/README.md) للحصول على معلومات حول إعداد المشروع وعملية البناء.

ابدأ في ملف `index.js` الخاص بك بإنشاء بعض المتغيرات `const` للاحتفاظ بالقيم المرتبطة بالحقول المختلفة:

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

جميع هذه الحقول يتم الإشارة إليها من خلال فئات CSS الخاصة بها، كما قمت بإعدادها في HTML في الدرس السابق.

### إضافة المستمعين

بعد ذلك، أضف مستمعي أحداث للنموذج وزر الإعادة الذي يعيد تعيين النموذج، بحيث إذا قام المستخدم بإرسال النموذج أو النقر على زر الإعادة، يحدث شيء ما، وأضف استدعاء لتهيئة التطبيق في نهاية الملف:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ لاحظ الاختصار المستخدم للاستماع إلى حدث الإرسال أو النقر، وكيف يتم تمرير الحدث إلى وظائف `handleSubmit` أو `reset`. هل يمكنك كتابة المكافئ لهذا الاختصار بتنسيق أطول؟ أيهما تفضل؟

### بناء وظيفة `init()` ووظيفة `reset()`:

الآن ستقوم ببناء الوظيفة التي تهيئ الإضافة، والتي تسمى `init()`:

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

في هذه الوظيفة، هناك منطق مثير للاهتمام. عند قراءته، هل يمكنك رؤية ما يحدث؟

- يتم إعداد متغيرين `const` للتحقق مما إذا كان المستخدم قد قام بتخزين مفتاح API ورمز المنطقة في التخزين المحلي.
- إذا كان أي منهما فارغًا، يتم عرض النموذج عن طريق تغيير نمطه ليظهر كـ 'block'.
- يتم إخفاء منطقة النتائج، التحميل، وزر الإعادة، ويتم تعيين أي نص خطأ ليكون فارغًا.
- إذا كان هناك مفتاح ومنطقة موجودة، يتم بدء روتين لـ:
  - استدعاء API للحصول على بيانات استخدام الكربون.
  - إخفاء منطقة النتائج.
  - إخفاء النموذج.
  - عرض زر الإعادة.

قبل المتابعة، من المفيد التعرف على مفهوم مهم جدًا متاح في المتصفحات: [التخزين المحلي](https://developer.mozilla.org/docs/Web/API/Window/localStorage). التخزين المحلي هو طريقة مفيدة لتخزين النصوص في المتصفح كزوج `key-value`. يمكن التلاعب بهذا النوع من التخزين بواسطة JavaScript لإدارة البيانات في المتصفح. التخزين المحلي لا ينتهي صلاحيته، بينما يتم مسح التخزين المؤقت (SessionStorage)، وهو نوع آخر من التخزين، عند إغلاق المتصفح. لكل نوع من أنواع التخزين مزايا وعيوب في استخدامه.

> ملاحظة - إضافة المتصفح الخاصة بك لديها تخزين محلي خاص بها؛ نافذة المتصفح الرئيسية هي حالة مختلفة وتتصرف بشكل منفصل.

يمكنك تعيين مفتاح API ليكون له قيمة نصية، على سبيل المثال، ويمكنك رؤية أنه تم تعيينه على Edge عن طريق "فحص" صفحة ويب (يمكنك النقر بزر الماوس الأيمن على المتصفح للفحص) والانتقال إلى علامة التبويب التطبيقات لرؤية التخزين.

![لوحة التخزين المحلي](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.ar.png)

✅ فكر في المواقف التي لا ترغب فيها بتخزين بعض البيانات في التخزين المحلي. بشكل عام، وضع مفاتيح API في التخزين المحلي فكرة سيئة! هل يمكنك رؤية السبب؟ في حالتنا، نظرًا لأن التطبيق الخاص بنا مخصص للتعلم فقط ولن يتم نشره في متجر التطبيقات، سنستخدم هذه الطريقة.

لاحظ أنك تستخدم Web API للتعامل مع التخزين المحلي، إما باستخدام `getItem()`، `setItem()`، أو `removeItem()`. يتم دعمها على نطاق واسع عبر المتصفحات.

قبل بناء وظيفة `displayCarbonUsage()` التي يتم استدعاؤها في `init()`، دعنا نبني الوظيفة التي تتعامل مع إرسال النموذج الأولي.

### التعامل مع إرسال النموذج

قم بإنشاء وظيفة تسمى `handleSubmit` تقبل وسيط حدث `(e)`. أوقف انتشار الحدث (في هذه الحالة، نريد إيقاف المتصفح من التحديث) واستدعِ وظيفة جديدة، `setUpUser`، مع تمرير الوسيطين `apiKey.value` و`region.value`. بهذه الطريقة، تستخدم القيمتين اللتين يتم جلبهما عبر النموذج الأولي عندما يتم ملء الحقول المناسبة.

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ قم بتحديث ذاكرتك - HTML الذي قمت بإعداده في الدرس الأخير يحتوي على حقلين إدخال يتم التقاط قيمهما عبر `const` الذي قمت بإعداده في أعلى الملف، وكلاهما `required` بحيث يمنع المتصفح المستخدمين من إدخال قيم فارغة.

### إعداد المستخدم

بالانتقال إلى وظيفة `setUpUser`، هنا حيث تقوم بتعيين قيم التخزين المحلي لـ apiKey وregionName. أضف وظيفة جديدة:

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

تقوم هذه الوظيفة بتعيين رسالة تحميل لتظهر أثناء استدعاء API. في هذه المرحلة، وصلت إلى إنشاء الوظيفة الأكثر أهمية في إضافة المتصفح هذه!

### عرض استخدام الكربون

أخيرًا، حان الوقت لاستعلام API!

قبل المتابعة، يجب أن نناقش APIs. APIs، أو [واجهات برمجة التطبيقات](https://www.webopedia.com/TERM/A/API.html)، هي عنصر حيوي في أدوات مطور الويب. توفر طرقًا قياسية لتفاعل البرامج والتواصل مع بعضها البعض. على سبيل المثال، إذا كنت تقوم ببناء موقع ويب يحتاج إلى استعلام قاعدة بيانات، قد يكون هناك API تم إنشاؤه لتستخدمه. بينما هناك العديد من أنواع APIs، أحد الأنواع الأكثر شيوعًا هو [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/).

✅ مصطلح 'REST' يرمز إلى 'نقل الحالة التمثيلية' ويتميز باستخدام عناوين URL مختلفة لجلب البيانات. قم ببعض البحث حول الأنواع المختلفة من APIs المتاحة للمطورين. أي تنسيق يروق لك؟

هناك أشياء مهمة يجب ملاحظتها حول هذه الوظيفة. أولاً، لاحظ الكلمة المفتاحية [`async`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function). كتابة الوظائف بحيث تعمل بشكل غير متزامن يعني أنها تنتظر اكتمال إجراء معين، مثل عودة البيانات، قبل المتابعة.

إليك فيديو سريع عن `async`:

[![Async و Await لإدارة الوعود](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async و Await لإدارة الوعود")

> 🎥 انقر على الصورة أعلاه لمشاهدة فيديو عن async/await.

قم بإنشاء وظيفة جديدة لاستعلام C02Signal API:

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

هذه وظيفة كبيرة. ما الذي يحدث هنا؟

- باتباع أفضل الممارسات، تستخدم الكلمة المفتاحية `async` لجعل هذه الوظيفة تعمل بشكل غير متزامن. تحتوي الوظيفة على كتلة `try/catch` لأنها ستعيد وعدًا عندما يعيد API البيانات. نظرًا لأنك لا تتحكم في سرعة استجابة API (قد لا يستجيب على الإطلاق!)، تحتاج إلى التعامل مع هذا الأمر عن طريق استدعائه بشكل غير متزامن.
- تقوم باستعلام co2signal API للحصول على بيانات منطقتك، باستخدام مفتاح API الخاص بك. لاستخدام هذا المفتاح، يجب عليك استخدام نوع من المصادقة في معلمات الرأس.
- بمجرد أن يستجيب API، تقوم بتعيين عناصر مختلفة من بيانات الاستجابة إلى الأجزاء التي قمت بإعدادها لعرض هذه البيانات.
- إذا كان هناك خطأ، أو إذا لم يكن هناك نتيجة، تعرض رسالة خطأ.

✅ استخدام أنماط البرمجة غير المتزامنة هو أداة مفيدة أخرى في صندوق أدواتك. اقرأ [عن الطرق المختلفة](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) التي يمكنك بها تكوين هذا النوع من الكود.

تهانينا! إذا قمت ببناء الإضافة الخاصة بك (`npm run build`) وقمت بتحديثها في لوحة الإضافات الخاصة بك، لديك إضافة تعمل! الشيء الوحيد الذي لا يعمل هو الأيقونة، وستقوم بإصلاح ذلك في الدرس التالي.

---

## 🚀 التحدي

لقد ناقشنا عدة أنواع من APIs حتى الآن في هذه الدروس. اختر API ويب وابحث بعمق في ما يقدمه. على سبيل المثال، ألقِ نظرة على APIs المتاحة داخل المتصفحات مثل [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API). ما الذي يجعل API رائعًا في رأيك؟

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/26)

## المراجعة والدراسة الذاتية

تعلمت عن التخزين المحلي وAPIs في هذا الدرس، وكلاهما مفيد جدًا لمطور الويب المحترف. هل يمكنك التفكير في كيفية عمل هذين الشيئين معًا؟ فكر في كيفية تصميم موقع ويب يقوم بتخزين العناصر ليتم استخدامها بواسطة API.

## الواجب

[تبني API](assignment.md)

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الموثوق. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة ناتجة عن استخدام هذه الترجمة.