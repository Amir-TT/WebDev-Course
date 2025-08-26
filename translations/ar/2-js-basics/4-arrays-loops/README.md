<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "3f7f87871312cf6cc12662da7d973182",
  "translation_date": "2025-08-25T21:46:18+00:00",
  "source_file": "2-js-basics/4-arrays-loops/README.md",
  "language_code": "ar"
}
-->
# أساسيات JavaScript: المصفوفات والحلقات

![أساسيات JavaScript - المصفوفات](../../../../translated_images/webdev101-js-arrays.439d7528b8a294558d0e4302e448d193f8ad7495cc407539cc81f1afe904b470.ar.png)
> رسم توضيحي بواسطة [Tomomi Imura](https://twitter.com/girlie_mac)

## اختبار ما قبل المحاضرة
[اختبار ما قبل المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/13)

تغطي هذه الدرس أساسيات JavaScript، اللغة التي تضيف التفاعلية إلى الويب. في هذا الدرس، ستتعلم عن المصفوفات والحلقات، والتي تُستخدم لمعالجة البيانات.

[![المصفوفات](https://img.youtube.com/vi/1U4qTyq02Xw/0.jpg)](https://youtube.com/watch?v=1U4qTyq02Xw "المصفوفات")

[![الحلقات](https://img.youtube.com/vi/Eeh7pxtTZ3k/0.jpg)](https://www.youtube.com/watch?v=Eeh7pxtTZ3k "الحلقات")

> 🎥 انقر على الصور أعلاه لمشاهدة فيديوهات عن المصفوفات والحلقات.

> يمكنك متابعة هذا الدرس على [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-arrays/?WT.mc_id=academic-77807-sagibbon)!

## المصفوفات

التعامل مع البيانات هو مهمة شائعة في أي لغة برمجة، وتصبح هذه المهمة أسهل عندما يتم تنظيم البيانات في هيكل مثل المصفوفات. باستخدام المصفوفات، يتم تخزين البيانات في هيكل يشبه القائمة. واحدة من الفوائد الرئيسية للمصفوفات هي أنه يمكنك تخزين أنواع مختلفة من البيانات في مصفوفة واحدة.

✅ المصفوفات موجودة في كل مكان حولنا! هل يمكنك التفكير في مثال من الحياة الواقعية لمصفوفة، مثل مصفوفة ألواح شمسية؟

صيغة كتابة المصفوفة هي زوج من الأقواس المربعة.

```javascript
let myArray = [];
```

هذه مصفوفة فارغة، ولكن يمكن تعريف المصفوفات وهي تحتوي بالفعل على بيانات. يتم فصل القيم المتعددة في المصفوفة بفاصلة.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

يتم تعيين قيم المصفوفة قيمة فريدة تُسمى **الفهرس**، وهو رقم صحيح يتم تعيينه بناءً على المسافة من بداية المصفوفة. في المثال أعلاه، القيمة النصية "Chocolate" لها فهرس 0، وفهرس "Rocky Road" هو 4. يمكنك استخدام الفهرس مع الأقواس المربعة لاسترجاع أو تغيير أو إدخال قيم المصفوفة.

✅ هل يفاجئك أن المصفوفات تبدأ بالفهرس صفر؟ في بعض لغات البرمجة، تبدأ الفهارس من 1. هناك تاريخ مثير للاهتمام حول هذا الموضوع، يمكنك [قراءته على ويكيبيديا](https://en.wikipedia.org/wiki/Zero-based_numbering).

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors[2]; //"Vanilla"
```

يمكنك استخدام الفهرس لتغيير قيمة، مثل هذا:

```javascript
iceCreamFlavors[4] = "Butter Pecan"; //Changed "Rocky Road" to "Butter Pecan"
```

ويمكنك إدخال قيمة جديدة في فهرس معين مثل هذا:

```javascript
iceCreamFlavors[5] = "Cookie Dough"; //Added "Cookie Dough"
```

✅ الطريقة الأكثر شيوعًا لإضافة قيم إلى مصفوفة هي باستخدام العمليات مثل array.push()

لمعرفة عدد العناصر الموجودة في المصفوفة، استخدم خاصية `length`.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
iceCreamFlavors.length; //5
```

✅ جرب بنفسك! استخدم وحدة التحكم في متصفحك لإنشاء ومعالجة مصفوفة من إنشائك.

## الحلقات

تسمح لنا الحلقات بتنفيذ مهام متكررة أو **تكرارية**، ويمكن أن توفر الكثير من الوقت والشفرة. يمكن أن تختلف كل تكرار في متغيراتها وقيمها وشروطها. هناك أنواع مختلفة من الحلقات في JavaScript، وكلها لها اختلافات صغيرة، لكنها تقوم في الأساس بنفس الشيء: التكرار على البيانات.

### حلقة For

تتطلب حلقة `for` ثلاثة أجزاء للتكرار:
- `counter` متغير يتم تهيئته عادةً برقم يعد عدد التكرارات
- `condition` تعبير يستخدم عوامل المقارنة لإيقاف الحلقة عندما تكون النتيجة `false`
- `iteration-expression` يتم تشغيله في نهاية كل تكرار، ويُستخدم عادةً لتغيير قيمة العداد

```javascript
// Counting up to 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ قم بتشغيل هذا الكود في وحدة التحكم في المتصفح. ماذا يحدث عندما تقوم بإجراء تغييرات صغيرة على العداد أو الشرط أو تعبير التكرار؟ هل يمكنك جعله يعمل بالعكس، لإنشاء عد تنازلي؟

### حلقة While

على عكس صيغة حلقة `for`، تتطلب حلقات `while` فقط شرطًا لإيقاف الحلقة عندما تصبح النتيجة `false`. تعتمد الشروط في الحلقات عادةً على قيم أخرى مثل العدادات، ويجب إدارتها أثناء الحلقة. يجب إنشاء القيم الابتدائية للعدادات خارج الحلقة، وأي تعبيرات لتحقيق شرط، بما في ذلك تغيير العداد، يجب أن تتم داخل الحلقة.

```javascript
//Counting up to 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ لماذا قد تختار استخدام حلقة for بدلاً من while؟ 17 ألف مشاهد كان لديهم نفس السؤال على StackOverflow، وبعض الآراء [قد تكون مثيرة للاهتمام بالنسبة لك](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript).

## الحلقات والمصفوفات

تُستخدم المصفوفات غالبًا مع الحلقات لأن معظم الشروط تتطلب طول المصفوفة لإيقاف الحلقة، ويمكن أن يكون الفهرس أيضًا قيمة العداد.

```javascript
let iceCreamFlavors = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < iceCreamFlavors.length; i++) {
  console.log(iceCreamFlavors[i]);
} //Ends when all flavors are printed
```

✅ جرب التكرار على مصفوفة من إنشائك في وحدة التحكم في المتصفح.

---

## 🚀 التحدي

هناك طرق أخرى للتكرار على المصفوفات غير الحلقات for وwhile. هناك [forEach](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)، [for-of](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/for...of)، و[map](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map). أعد كتابة حلقة المصفوفة الخاصة بك باستخدام واحدة من هذه التقنيات.

## اختبار ما بعد المحاضرة
[اختبار ما بعد المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/14)

## المراجعة والدراسة الذاتية

تحتوي المصفوفات في JavaScript على العديد من الطرق المرتبطة بها، والتي تكون مفيدة للغاية لمعالجة البيانات. [اقرأ عن هذه الطرق](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array) وجرب بعضها (مثل push، pop، slice وsplice) على مصفوفة من إنشائك.

## الواجب

[تكرار مصفوفة](assignment.md)

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.