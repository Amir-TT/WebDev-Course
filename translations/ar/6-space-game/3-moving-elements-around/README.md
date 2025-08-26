<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "23f088add24f0f1fa51014a9e27ea280",
  "translation_date": "2025-08-25T22:09:19+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة فضاء الجزء الثالث: إضافة الحركة

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/33)

الألعاب ليست ممتعة كثيرًا حتى تبدأ الكائنات الفضائية بالتحرك على الشاشة! في هذه اللعبة، سنستخدم نوعين من الحركات:

- **حركة لوحة المفاتيح/الماوس**: عندما يتفاعل المستخدم مع لوحة المفاتيح أو الماوس لتحريك كائن على الشاشة.
- **حركة ناتجة عن اللعبة**: عندما تقوم اللعبة بتحريك كائن بفاصل زمني معين.

إذن كيف نحرك الأشياء على الشاشة؟ الأمر كله يتعلق بالإحداثيات الكارتيزية: نقوم بتغيير الموقع (x، y) للكائن ثم نعيد رسم الشاشة.

عادةً تحتاج إلى الخطوات التالية لتحقيق *الحركة* على الشاشة:

1. **تحديد موقع جديد** للكائن؛ هذا ضروري لإدراك أن الكائن قد تحرك.
2. **مسح الشاشة**، يجب مسح الشاشة بين عمليات الرسم. يمكننا مسحها عن طريق رسم مستطيل نملؤه بلون الخلفية.
3. **إعادة رسم الكائن** في الموقع الجديد. من خلال القيام بذلك، نحقق أخيرًا نقل الكائن من موقع إلى آخر.

إليك كيف يمكن أن يبدو ذلك في الكود:

```javascript
//set the hero's location
hero.x += 5;
// clear the rectangle that hosts the hero
ctx.clearRect(0, 0, canvas.width, canvas.height);
// redraw the game background and hero
ctx.fillRect(0, 0, canvas.width, canvas.height)
ctx.fillStyle = "black";
ctx.drawImage(heroImg, hero.x, hero.y);
```

✅ هل يمكنك التفكير في سبب قد يؤدي إلى تكاليف أداء عند إعادة رسم البطل عدة إطارات في الثانية؟ اقرأ عن [بدائل لهذا النمط](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas).

## التعامل مع أحداث لوحة المفاتيح

يمكنك التعامل مع الأحداث عن طريق ربط أحداث محددة بالكود. يتم تشغيل أحداث لوحة المفاتيح على النافذة بأكملها، بينما يمكن ربط أحداث الماوس مثل `click` بالنقر على عنصر معين. سنستخدم أحداث لوحة المفاتيح طوال هذا المشروع.

للتعامل مع حدث، تحتاج إلى استخدام طريقة `addEventListener()` الخاصة بالنافذة وتزويدها بمعاملين. المعامل الأول هو اسم الحدث، مثل `keyup`. المعامل الثاني هو الوظيفة التي يجب استدعاؤها نتيجة لحدوث الحدث.

إليك مثال:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

بالنسبة لأحداث المفاتيح، هناك خاصيتان على الحدث يمكنك استخدامهما لمعرفة المفتاح الذي تم الضغط عليه:

- `key`، وهو تمثيل نصي للمفتاح المضغوط، مثل `ArrowUp`.
- `keyCode`، وهو تمثيل رقمي، مثل `37`، الذي يتوافق مع `ArrowLeft`.

✅ التلاعب بأحداث المفاتيح مفيد خارج تطوير الألعاب. ما الاستخدامات الأخرى التي يمكنك التفكير فيها لهذه التقنية؟

### المفاتيح الخاصة: تحذير

هناك بعض المفاتيح *الخاصة* التي تؤثر على النافذة. هذا يعني أنه إذا كنت تستمع إلى حدث `keyup` واستخدمت هذه المفاتيح الخاصة لتحريك البطل، فستؤدي أيضًا إلى التمرير الأفقي. لهذا السبب قد ترغب في *إيقاف* هذا السلوك الافتراضي للمتصفح أثناء بناء لعبتك. تحتاج إلى كود مثل هذا:

```javascript
let onKeyDown = function (e) {
  console.log(e.keyCode);
  switch (e.keyCode) {
    case 37:
    case 39:
    case 38:
    case 40: // Arrow keys
    case 32:
      e.preventDefault();
      break; // Space
    default:
      break; // do not block other keys
  }
};

window.addEventListener('keydown', onKeyDown);
```

الكود أعلاه سيضمن أن مفاتيح الأسهم ومفتاح المسافة يتم *إيقاف* سلوكها الافتراضي. يحدث آلية *الإيقاف* عندما نستدعي `e.preventDefault()`.

## الحركة الناتجة عن اللعبة

يمكننا جعل الأشياء تتحرك من تلقاء نفسها باستخدام مؤقتات مثل وظيفة `setTimeout()` أو `setInterval()` التي تقوم بتحديث موقع الكائن في كل دورة زمنية. إليك كيف يمكن أن يبدو ذلك:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## حلقة اللعبة

حلقة اللعبة هي مفهوم يتمثل في وظيفة يتم استدعاؤها على فترات منتظمة. تُسمى حلقة اللعبة لأن كل ما يجب أن يكون مرئيًا للمستخدم يتم رسمه داخل الحلقة. تستخدم حلقة اللعبة جميع الكائنات التي تشكل جزءًا من اللعبة، وترسمها جميعًا إلا إذا كان هناك سبب يجعلها لا تكون جزءًا من اللعبة بعد الآن. على سبيل المثال، إذا كان الكائن عدوًا تم ضربه بواسطة شعاع ليزر وانفجر، فإنه لم يعد جزءًا من حلقة اللعبة الحالية (ستتعلم المزيد عن هذا في الدروس اللاحقة).

إليك كيف يمكن أن تبدو حلقة اللعبة عادةً، معبرًا عنها بالكود:

```javascript
let gameLoopId = setInterval(() =>
  function gameLoop() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "black";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    drawHero();
    drawEnemies();
    drawStaticObjects();
}, 200);
```

يتم استدعاء الحلقة أعلاه كل `200` ميلي ثانية لإعادة رسم اللوحة. لديك القدرة على اختيار الفاصل الزمني الأفضل الذي يناسب لعبتك.

## متابعة لعبة الفضاء

ستأخذ الكود الموجود وتقوم بتوسيعه. إما أن تبدأ بالكود الذي أكملته خلال الجزء الأول أو تستخدم الكود في [الجزء الثاني - البداية](../../../../6-space-game/3-moving-elements-around/your-work).

- **تحريك البطل**: ستضيف كودًا لضمان إمكانية تحريك البطل باستخدام مفاتيح الأسهم.
- **تحريك الأعداء**: ستحتاج أيضًا إلى إضافة كود لضمان تحرك الأعداء من الأعلى إلى الأسفل بمعدل معين.

## الخطوات الموصى بها

حدد الملفات التي تم إنشاؤها لك في مجلد `your-work`. يجب أن تحتوي على ما يلي:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

ابدأ مشروعك في مجلد `your_work` عن طريق كتابة:

```bash
cd your-work
npm start
```

سيبدأ ذلك خادم HTTP على العنوان `http://localhost:5000`. افتح متصفحًا وأدخل هذا العنوان، في الوقت الحالي يجب أن يعرض البطل وجميع الأعداء؛ لا شيء يتحرك - بعد!

### إضافة الكود

1. **إضافة كائنات مخصصة** للبطل والعدو وكائن اللعبة، يجب أن تحتوي على خصائص `x` و `y`. (تذكر الجزء الخاص بـ [الوراثة أو التركيب](../README.md)).

   *تلميح*: يجب أن يكون كائن اللعبة هو الذي يحتوي على `x` و `y` والقدرة على رسم نفسه على اللوحة.

   >تلميح: ابدأ بإضافة فئة GameObject مع منشئها كما هو موضح أدناه، ثم ارسمها على اللوحة:

    ```javascript
        
    class GameObject {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.dead = false;
        this.type = "";
        this.width = 0;
        this.height = 0;
        this.img = undefined;
      }
    
      draw(ctx) {
        ctx.drawImage(this.img, this.x, this.y, this.width, this.height);
      }
    }
    ```

    الآن، قم بتمديد هذا GameObject لإنشاء البطل والعدو.

    ```javascript
    class Hero extends GameObject {
      constructor(x, y) {
        ...it needs an x, y, type, and speed
      }
    }
    ```

    ```javascript
    class Enemy extends GameObject {
      constructor(x, y) {
        super(x, y);
        (this.width = 98), (this.height = 50);
        this.type = "Enemy";
        let id = setInterval(() => {
          if (this.y < canvas.height - this.height) {
            this.y += 5;
          } else {
            console.log('Stopped at', this.y)
            clearInterval(id);
          }
        }, 300)
      }
    }
    ```

2. **إضافة معالجات أحداث المفاتيح** للتعامل مع التنقل بالمفاتيح (تحريك البطل لأعلى/أسفل/يسار/يمين).

   *تذكر*: إنه نظام كارتيزي، أعلى اليسار هو `0،0`. أيضًا تذكر إضافة كود لإيقاف *السلوك الافتراضي*.

   >تلميح: قم بإنشاء وظيفة onKeyDown واربطها بالنافذة:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   تحقق من وحدة التحكم في المتصفح في هذه المرحلة، وشاهد ضغطات المفاتيح التي يتم تسجيلها.

3. **تنفيذ** [نمط النشر والاشتراك](../README.md)، سيحافظ هذا على نظافة الكود الخاص بك أثناء متابعة الأجزاء المتبقية.

   للقيام بهذا الجزء الأخير، يمكنك:

   1. **إضافة مستمع حدث** على النافذة:

       ```javascript
        window.addEventListener("keyup", (evt) => {
          if (evt.key === "ArrowUp") {
            eventEmitter.emit(Messages.KEY_EVENT_UP);
          } else if (evt.key === "ArrowDown") {
            eventEmitter.emit(Messages.KEY_EVENT_DOWN);
          } else if (evt.key === "ArrowLeft") {
            eventEmitter.emit(Messages.KEY_EVENT_LEFT);
          } else if (evt.key === "ArrowRight") {
            eventEmitter.emit(Messages.KEY_EVENT_RIGHT);
          }
        });
        ```

    1. **إنشاء فئة EventEmitter** لنشر الرسائل والاشتراك فيها:

        ```javascript
        class EventEmitter {
          constructor() {
            this.listeners = {};
          }
        
          on(message, listener) {
            if (!this.listeners[message]) {
              this.listeners[message] = [];
            }
            this.listeners[message].push(listener);
          }
        
          emit(message, payload = null) {
            if (this.listeners[message]) {
              this.listeners[message].forEach((l) => l(message, payload));
            }
          }
        }
        ```

    1. **إضافة ثوابت** وإعداد EventEmitter:

        ```javascript
        const Messages = {
          KEY_EVENT_UP: "KEY_EVENT_UP",
          KEY_EVENT_DOWN: "KEY_EVENT_DOWN",
          KEY_EVENT_LEFT: "KEY_EVENT_LEFT",
          KEY_EVENT_RIGHT: "KEY_EVENT_RIGHT",
        };
        
        let heroImg, 
            enemyImg, 
            laserImg,
            canvas, ctx, 
            gameObjects = [], 
            hero, 
            eventEmitter = new EventEmitter();
        ```

    1. **تهيئة اللعبة**

    ```javascript
    function initGame() {
      gameObjects = [];
      createEnemies();
      createHero();
    
      eventEmitter.on(Messages.KEY_EVENT_UP, () => {
        hero.y -=5 ;
      })
    
      eventEmitter.on(Messages.KEY_EVENT_DOWN, () => {
        hero.y += 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_LEFT, () => {
        hero.x -= 5;
      });
    
      eventEmitter.on(Messages.KEY_EVENT_RIGHT, () => {
        hero.x += 5;
      });
    }
    ```

1. **إعداد حلقة اللعبة**

   قم بإعادة صياغة وظيفة window.onload لتهيئة اللعبة وإعداد حلقة اللعبة على فاصل زمني جيد. ستضيف أيضًا شعاع ليزر:

    ```javascript
    window.onload = async () => {
      canvas = document.getElementById("canvas");
      ctx = canvas.getContext("2d");
      heroImg = await loadTexture("assets/player.png");
      enemyImg = await loadTexture("assets/enemyShip.png");
      laserImg = await loadTexture("assets/laserRed.png");
    
      initGame();
      let gameLoopId = setInterval(() => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        drawGameObjects(ctx);
      }, 100)
      
    };
    ```

5. **إضافة كود** لتحريك الأعداء بفاصل زمني معين

    قم بإعادة صياغة وظيفة `createEnemies()` لإنشاء الأعداء ودفعهم إلى فئة gameObjects الجديدة:

    ```javascript
    function createEnemies() {
      const MONSTER_TOTAL = 5;
      const MONSTER_WIDTH = MONSTER_TOTAL * 98;
      const START_X = (canvas.width - MONSTER_WIDTH) / 2;
      const STOP_X = START_X + MONSTER_WIDTH;
    
      for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          const enemy = new Enemy(x, y);
          enemy.img = enemyImg;
          gameObjects.push(enemy);
        }
      }
    }
    ```
    
    وأضف وظيفة `createHero()` للقيام بعملية مشابهة للبطل.

    ```javascript
    function createHero() {
      hero = new Hero(
        canvas.width / 2 - 45,
        canvas.height - canvas.height / 4
      );
      hero.img = heroImg;
      gameObjects.push(hero);
    }
    ```

    وأخيرًا، أضف وظيفة `drawGameObjects()` لبدء الرسم:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    يجب أن يبدأ الأعداء بالتقدم نحو سفينة البطل الفضائية!

---

## 🚀 التحدي

كما ترى، يمكن أن يتحول الكود الخاص بك إلى "كود سباغيتي" عندما تبدأ في إضافة وظائف ومتغيرات وفئات. كيف يمكنك تنظيم الكود الخاص بك بشكل أفضل بحيث يكون أكثر قابلية للقراءة؟ قم برسم نظام لتنظيم الكود الخاص بك، حتى لو كان لا يزال موجودًا في ملف واحد.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/34)

## المراجعة والدراسة الذاتية

بينما نكتب لعبتنا بدون استخدام أطر عمل، هناك العديد من أطر العمل القائمة على JavaScript لتطوير الألعاب باستخدام اللوحة. خذ بعض الوقت للقيام ببعض [القراءة عن هذه](https://github.com/collections/javascript-game-engines).

## الواجب

[قم بتعليق الكود الخاص بك](assignment.md)

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.