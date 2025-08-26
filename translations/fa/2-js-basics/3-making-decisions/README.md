<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "888609c48329c280ca2477d2df40f2e5",
  "translation_date": "2025-08-24T12:13:27+00:00",
  "source_file": "2-js-basics/3-making-decisions/README.md",
  "language_code": "fa"
}
-->
# اصول اولیه جاوااسکریپت: تصمیم‌گیری

![اصول اولیه جاوااسکریپت - تصمیم‌گیری](../../../../sketchnotes/webdev101-js-decisions.png)

> اسکیچ‌نوت از [Tomomi Imura](https://twitter.com/girlie_mac)

## آزمون پیش از درس

[آزمون پیش از درس](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/11)

تصمیم‌گیری و کنترل ترتیب اجرای کد باعث می‌شود کد شما قابل استفاده مجدد و قوی‌تر باشد. این بخش به بررسی سینتکس کنترل جریان داده در جاوااسکریپت و اهمیت آن در استفاده با انواع داده بولی می‌پردازد.

[![تصمیم‌گیری](https://img.youtube.com/vi/SxTp8j-fMMY/0.jpg)](https://youtube.com/watch?v=SxTp8j-fMMY "تصمیم‌گیری")

> 🎥 برای مشاهده ویدئویی درباره تصمیم‌گیری، روی تصویر بالا کلیک کنید.

> می‌توانید این درس را در [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-if-else/?WT.mc_id=academic-77807-sagibbon) مطالعه کنید!

## مرور کوتاه بر بولین‌ها

بولین‌ها فقط می‌توانند دو مقدار داشته باشند: `true` یا `false`. بولین‌ها به تصمیم‌گیری درباره اینکه کدام خطوط کد باید اجرا شوند، کمک می‌کنند.

بولین خود را به این صورت به مقدار true یا false تنظیم کنید:

`let myTrueBool = true`  
`let myFalseBool = false`

✅ بولین‌ها به نام ریاضی‌دان، فیلسوف و منطق‌دان انگلیسی، جورج بول (1815–1864) نام‌گذاری شده‌اند.

## عملگرهای مقایسه و بولین‌ها

عملگرها برای ارزیابی شرایط با انجام مقایسه‌هایی که یک مقدار بولین ایجاد می‌کنند، استفاده می‌شوند. در زیر لیستی از عملگرهای پرکاربرد آورده شده است.

| نماد   | توضیحات                                                                                                                                                     | مثال               |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| `<`    | **کمتر از**: دو مقدار را مقایسه می‌کند و اگر مقدار سمت چپ کمتر از مقدار سمت راست باشد، مقدار بولین `true` را برمی‌گرداند                                  | `5 < 6 // true`    |
| `<=`   | **کمتر یا مساوی با**: دو مقدار را مقایسه می‌کند و اگر مقدار سمت چپ کمتر یا مساوی مقدار سمت راست باشد، مقدار بولین `true` را برمی‌گرداند                  | `5 <= 6 // true`   |
| `>`    | **بزرگتر از**: دو مقدار را مقایسه می‌کند و اگر مقدار سمت چپ بزرگتر از مقدار سمت راست باشد، مقدار بولین `true` را برمی‌گرداند                             | `5 > 6 // false`   |
| `>=`   | **بزرگتر یا مساوی با**: دو مقدار را مقایسه می‌کند و اگر مقدار سمت چپ بزرگتر یا مساوی مقدار سمت راست باشد، مقدار بولین `true` را برمی‌گرداند             | `5 >= 6 // false`  |
| `===`  | **برابری سختگیرانه**: دو مقدار را مقایسه می‌کند و اگر مقادیر سمت راست و چپ برابر و از یک نوع داده باشند، مقدار بولین `true` را برمی‌گرداند              | `5 === 6 // false` |
| `!==`  | **نابرابری**: دو مقدار را مقایسه می‌کند و مقدار بولین مخالف آنچه عملگر برابری سختگیرانه برمی‌گرداند، بازمی‌گرداند                                        | `5 !== 6 // true`  |

✅ با نوشتن چند مقایسه در کنسول مرورگر خود، دانش خود را بررسی کنید. آیا داده‌های بازگشتی شما را شگفت‌زده می‌کنند؟

## دستور If

دستور if کدی که بین بلوک‌های آن قرار دارد را در صورتی که شرط برقرار باشد، اجرا می‌کند.

```javascript
if (condition) {
  //Condition is true. Code in this block will run.
}
```

عملگرهای منطقی اغلب برای تشکیل شرط استفاده می‌شوند.

```javascript
let currentMoney;
let laptopPrice;

if (currentMoney >= laptopPrice) {
  //Condition is true. Code in this block will run.
  console.log("Getting a new laptop!");
}
```

## دستور If..Else

دستور `else` کدی که بین بلوک‌های آن قرار دارد را در صورتی که شرط برقرار نباشد، اجرا می‌کند. استفاده از آن با دستور `if` اختیاری است.

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

✅ با اجرای این کد و کد زیر در کنسول مرورگر، درک خود را آزمایش کنید. مقادیر متغیرهای currentMoney و laptopPrice را تغییر دهید تا خروجی `console.log()` تغییر کند.

## دستور Switch

دستور `switch` برای انجام اقدامات مختلف بر اساس شرایط مختلف استفاده می‌شود. از دستور `switch` برای انتخاب یکی از چند بلوک کد برای اجرا استفاده کنید.

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

✅ با اجرای این کد و کد زیر در کنسول مرورگر، درک خود را آزمایش کنید. مقادیر متغیر a را تغییر دهید تا خروجی `console.log()` تغییر کند.

## عملگرهای منطقی و بولین‌ها

تصمیم‌گیری ممکن است به بیش از یک مقایسه نیاز داشته باشد و می‌توان آن‌ها را با عملگرهای منطقی ترکیب کرد تا یک مقدار بولین تولید شود.

| نماد   | توضیحات                                                                                     | مثال                                                                 |
| ------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `&&`   | **و منطقی**: دو عبارت بولین را مقایسه می‌کند. فقط در صورتی که هر دو طرف true باشند، true بازمی‌گرداند | `(5 > 6) && (5 < 6 ) // یک طرف false است، طرف دیگر true. نتیجه false` |
| `\|\|` | **یا منطقی**: دو عبارت بولین را مقایسه می‌کند. اگر حداقل یکی از طرفین true باشد، true بازمی‌گرداند | `(5 > 6) \|\| (5 < 6) // یک طرف false است، طرف دیگر true. نتیجه true` |
| `!`    | **نقیض منطقی**: مقدار مخالف یک عبارت بولین را بازمی‌گرداند                               | `!(5 > 6) // 5 بزرگتر از 6 نیست، اما "!" مقدار true بازمی‌گرداند`   |

## شرایط و تصمیم‌گیری با عملگرهای منطقی

عملگرهای منطقی می‌توانند برای تشکیل شرایط در دستورات if..else استفاده شوند.

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

### عملگر نقیض

تا اینجا دیدید که چگونه می‌توانید از دستور `if...else` برای ایجاد منطق شرطی استفاده کنید. هر چیزی که درون یک `if` قرار می‌گیرد باید به true/false ارزیابی شود. با استفاده از عملگر `!` می‌توانید عبارت را _نقیض_ کنید. به این صورت خواهد بود:

```javascript
if (!condition) {
  // runs if condition is false
} else {
  // runs if condition is true
}
```

### عبارات سه‌تایی

`if...else` تنها راه برای بیان منطق تصمیم‌گیری نیست. می‌توانید از چیزی به نام عملگر سه‌تایی نیز استفاده کنید. سینتکس آن به این صورت است:

```javascript
let variable = condition ? <return this if true> : <return this if false>
```

در زیر یک مثال ملموس‌تر آورده شده است:

```javascript
let firstNumber = 20;
let secondNumber = 10;
let biggestNumber = firstNumber > secondNumber ? firstNumber : secondNumber;
```

✅ چند دقیقه وقت بگذارید و این کد را چند بار بخوانید. آیا متوجه می‌شوید که این عملگرها چگونه کار می‌کنند؟

کد بالا بیان می‌کند که:

- اگر `firstNumber` بزرگتر از `secondNumber` باشد
- سپس مقدار `firstNumber` را به `biggestNumber` اختصاص بده
- در غیر این صورت مقدار `secondNumber` را اختصاص بده.

عبارت سه‌تایی فقط یک روش فشرده برای نوشتن کد زیر است:

```javascript
let biggestNumber;
if (firstNumber > secondNumber) {
  biggestNumber = firstNumber;
} else {
  biggestNumber = secondNumber;
}
```

---

## 🚀 چالش

برنامه‌ای بنویسید که ابتدا با عملگرهای منطقی نوشته شده باشد و سپس آن را با استفاده از یک عبارت سه‌تایی بازنویسی کنید. کدام سینتکس را ترجیح می‌دهید؟

---

## آزمون پس از درس

[آزمون پس از درس](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/12)

## مرور و مطالعه شخصی

درباره عملگرهای مختلفی که در اختیار کاربر قرار دارد، بیشتر در [MDN](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators) بخوانید.

به ابزار فوق‌العاده [operator lookup](https://joshwcomeau.com/operator-lookup/) از Josh Comeau نگاهی بیندازید!

## تکلیف

[عملگرها](assignment.md)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم دقت را حفظ کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادقتی‌ها باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.