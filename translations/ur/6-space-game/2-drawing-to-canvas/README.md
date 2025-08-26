<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "41be8d35e7f30aa9dad10773c35e89c4",
  "translation_date": "2025-08-25T22:16:10+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "ur"
}
-->
# اسپیس گیم بنائیں حصہ 2: ہیرو اور مونسٹرز کو کینوس پر ڈرائنگ کریں

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/31)

## کینوس

کینوس ایک HTML عنصر ہے جو ڈیفالٹ میں کوئی مواد نہیں رکھتا؛ یہ ایک خالی تختی کی طرح ہے۔ آپ کو اس پر ڈرائنگ کر کے مواد شامل کرنا ہوگا۔

✅ [کینوس API کے بارے میں مزید پڑھیں](https://developer.mozilla.org/docs/Web/API/Canvas_API) MDN پر۔

یہ عام طور پر صفحے کے باڈی کا حصہ ہوتے ہوئے اس طرح ڈکلیئر کیا جاتا ہے:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

اوپر ہم نے `id`, `width` اور `height` سیٹ کیے ہیں۔

- `id`: یہ سیٹ کریں تاکہ آپ اس کا حوالہ حاصل کر سکیں جب آپ کو اس کے ساتھ تعامل کرنا ہو۔
- `width`: یہ عنصر کی چوڑائی ہے۔
- `height`: یہ عنصر کی اونچائی ہے۔

## سادہ جیومیٹری ڈرائنگ کرنا

کینوس کارٹیزین کوآرڈینیٹ سسٹم کا استعمال کرتا ہے چیزوں کو ڈرائنگ کرنے کے لیے۔ اس لیے یہ x-axis اور y-axis کا استعمال کرتا ہے یہ ظاہر کرنے کے لیے کہ کچھ کہاں واقع ہے۔ مقام `0,0` اوپر بائیں کونے میں ہے اور نیچے دائیں کونا وہ ہے جو آپ نے کینوس کی چوڑائی اور اونچائی کے طور پر مقرر کیا ہے۔

![کینوس کا گرڈ](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.ur.png)  
> تصویر [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes) سے

کینوس عنصر پر ڈرائنگ کرنے کے لیے آپ کو درج ذیل مراحل سے گزرنا ہوگا:

1. **حوالہ حاصل کریں** کینوس عنصر کا۔
2. **حوالہ حاصل کریں** کینوس عنصر پر موجود کانٹیکسٹ عنصر کا۔
3. **ڈرائنگ آپریشن انجام دیں** کانٹیکسٹ عنصر کا استعمال کرتے ہوئے۔

اوپر دیے گئے مراحل کے لیے کوڈ عام طور پر اس طرح نظر آتا ہے:

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

✅ کینوس API زیادہ تر 2D اشکال پر مرکوز ہے، لیکن آپ ویب سائٹ پر 3D عناصر بھی ڈرائنگ کر سکتے ہیں؛ اس کے لیے آپ [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) استعمال کر سکتے ہیں۔

آپ کینوس API کے ساتھ مختلف چیزیں ڈرائنگ کر سکتے ہیں جیسے:

- **جیومیٹریکل اشکال**، ہم نے پہلے ہی دکھایا کہ ایک مستطیل کیسے ڈرائنگ کی جاتی ہے، لیکن آپ اور بھی بہت کچھ ڈرائنگ کر سکتے ہیں۔
- **متن**، آپ کسی بھی فونٹ اور رنگ کے ساتھ متن ڈرائنگ کر سکتے ہیں۔
- **تصاویر**، آپ کسی تصویر کے اثاثے جیسے .jpg یا .png کی بنیاد پر تصویر ڈرائنگ کر سکتے ہیں۔

✅ آزمائیں! آپ جانتے ہیں کہ مستطیل کیسے ڈرائنگ کی جاتی ہے، کیا آپ صفحے پر دائرہ ڈرائنگ کر سکتے ہیں؟ CodePen پر کچھ دلچسپ کینوس ڈرائنگز دیکھیں۔ یہاں ایک [خاص طور پر متاثر کن مثال](https://codepen.io/dissimulate/pen/KrAwx) ہے۔

## ایک تصویر کے اثاثے کو لوڈ کریں اور ڈرائنگ کریں

آپ ایک تصویر کے اثاثے کو `Image` آبجیکٹ بنا کر اور اس کی `src` پراپرٹی سیٹ کر کے لوڈ کرتے ہیں۔ پھر آپ `load` ایونٹ کو سنتے ہیں تاکہ معلوم ہو سکے کہ یہ استعمال کے لیے تیار ہے۔ کوڈ اس طرح نظر آتا ہے:

### اثاثہ لوڈ کریں

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### اثاثہ لوڈ کرنے کا پیٹرن

اوپر دیے گئے کوڈ کو اس طرح کے کنسٹرکٹ میں لپیٹنے کی سفارش کی جاتی ہے تاکہ اسے استعمال کرنا آسان ہو اور آپ صرف اس وقت اس میں تبدیلی کریں جب یہ مکمل طور پر لوڈ ہو:

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

اسکرین پر گیم کے اثاثے ڈرائنگ کرنے کے لیے، آپ کا کوڈ اس طرح نظر آئے گا:

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

## اب وقت ہے کہ آپ اپنا گیم بنانا شروع کریں

### کیا بنانا ہے

آپ کو ایک ویب صفحہ بنانا ہوگا جس میں کینوس عنصر ہو۔ یہ ایک سیاہ اسکرین `1024*768` رینڈر کرے۔ ہم نے آپ کو دو تصاویر فراہم کی ہیں:

- ہیرو شپ

   ![ہیرو شپ](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.ur.png)

- 5*5 مونسٹر

   ![مونسٹر شپ](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.ur.png)

### ترقی شروع کرنے کے لیے تجویز کردہ مراحل

ان فائلوں کو تلاش کریں جو آپ کے لیے `your-work` سب فولڈر میں بنائی گئی ہیں۔ اس میں درج ذیل شامل ہونا چاہیے:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Visual Studio Code میں اس فولڈر کی کاپی کھولیں۔ آپ کو ایک مقامی ترقیاتی ماحول ترتیب دینا ہوگا، ترجیحاً Visual Studio Code کے ساتھ NPM اور Node انسٹال ہو۔ اگر آپ کے کمپیوٹر پر `npm` سیٹ اپ نہیں ہے، تو [یہاں دیکھیں کہ اسے کیسے کریں](https://www.npmjs.com/get-npm)۔

اپنے پروجیکٹ کو `your_work` فولڈر میں نیویگیٹ کر کے شروع کریں:

```bash
cd your-work
npm start
```

اوپر دیا گیا کوڈ HTTP سرور کو ایڈریس `http://localhost:5000` پر شروع کرے گا۔ ایک براؤزر کھولیں اور اس ایڈریس کو درج کریں۔ یہ ابھی ایک خالی صفحہ ہے، لیکن یہ جلد ہی بدل جائے گا۔

> نوٹ: اسکرین پر تبدیلیاں دیکھنے کے لیے، اپنے براؤزر کو ریفریش کریں۔

### کوڈ شامل کریں

`your-work/app.js` میں درج ذیل کو حل کرنے کے لیے ضروری کوڈ شامل کریں:

1. **کینوس ڈرائنگ کریں** سیاہ پس منظر کے ساتھ  
   > ٹپ: `/app.js` میں مناسب TODO کے تحت دو لائنیں شامل کریں، `ctx` عنصر کو سیاہ سیٹ کریں اور اوپر/بائیں کوآرڈینیٹس کو 0,0 پر سیٹ کریں اور کینوس کی اونچائی اور چوڑائی کے برابر سیٹ کریں۔
2. **ٹیکسچرز لوڈ کریں**  
   > ٹپ: `await loadTexture` کا استعمال کرتے ہوئے کھلاڑی اور دشمن کی تصاویر شامل کریں اور تصویر کا راستہ پاس کریں۔ آپ انہیں ابھی اسکرین پر نہیں دیکھیں گے!
3. **ہیرو کو اسکرین کے مرکز میں نیچے کے نصف حصے میں ڈرائنگ کریں**  
   > ٹپ: `drawImage` API کا استعمال کریں ہیرو کی تصویر کو اسکرین پر ڈرائنگ کرنے کے لیے، `canvas.width / 2 - 45` اور `canvas.height - canvas.height / 4)` سیٹ کریں۔
4. **5*5 مونسٹرز ڈرائنگ کریں**  
   > ٹپ: اب آپ دشمنوں کو اسکرین پر ڈرائنگ کرنے کے لیے کوڈ کو ان کومنٹ کر سکتے ہیں۔ اس کے بعد، `createEnemies` فنکشن پر جائیں اور اسے مکمل کریں۔

   پہلے، کچھ کانسٹنٹس سیٹ کریں:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    پھر، مونسٹرز کی صف کو اسکرین پر ڈرائنگ کرنے کے لیے ایک لوپ بنائیں:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## نتیجہ

مکمل نتیجہ اس طرح نظر آنا چاہیے:

![سیاہ اسکرین جس میں ایک ہیرو اور 5*5 مونسٹرز ہیں](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.ur.png)

## حل

براہ کرم پہلے خود اسے حل کرنے کی کوشش کریں، لیکن اگر آپ پھنس جائیں تو [حل](../../../../6-space-game/2-drawing-to-canvas/solution/app.js) دیکھیں۔

---

## 🚀 چیلنج

آپ نے 2D پر مرکوز کینوس API کے بارے میں سیکھا؛ [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) پر ایک نظر ڈالیں، اور 3D آبجیکٹ ڈرائنگ کرنے کی کوشش کریں۔

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/32)

## جائزہ اور خود مطالعہ

کینوس API کے بارے میں مزید جاننے کے لیے [اسے پڑھیں](https://developer.mozilla.org/docs/Web/API/Canvas_API)۔

## اسائنمنٹ

[کینوس API کے ساتھ کھیلیں](assignment.md)

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔