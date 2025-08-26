<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2e83e38c35dc003f046d7cc0bbfd4920",
  "translation_date": "2025-08-25T22:21:24+00:00",
  "source_file": "6-space-game/4-collision-detection/README.md",
  "language_code": "ar"
}
-->
# بناء لعبة فضاء الجزء 4: إضافة الليزر واكتشاف التصادمات

## اختبار ما قبل المحاضرة

[اختبار ما قبل المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/35)

في هذا الدرس، ستتعلم كيفية إطلاق الليزر باستخدام JavaScript! سنضيف عنصرين إلى لعبتنا:

- **الليزر**: يتم إطلاق هذا الليزر من سفينة البطل ويتحرك عموديًا للأعلى.
- **اكتشاف التصادمات**: كجزء من تنفيذ القدرة على *الإطلاق*، سنضيف بعض القواعد الممتعة للعبة:
   - **الليزر يصيب العدو**: يموت العدو إذا أصيب بالليزر.
   - **الليزر يصيب أعلى الشاشة**: يتم تدمير الليزر إذا أصاب الجزء العلوي من الشاشة.
   - **تصادم العدو مع البطل**: يتم تدمير العدو والبطل إذا اصطدما ببعضهما.
   - **العدو يصيب أسفل الشاشة**: يتم تدمير العدو والبطل إذا وصل العدو إلى أسفل الشاشة.

باختصار، أنت -- *البطل* -- تحتاج إلى إصابة جميع الأعداء بالليزر قبل أن يتمكنوا من الوصول إلى أسفل الشاشة.

✅ قم بإجراء بحث صغير عن أول لعبة كمبيوتر تم إنشاؤها على الإطلاق. ما هي وظيفتها؟

لنكن أبطالًا معًا!

## اكتشاف التصادمات

كيف نقوم باكتشاف التصادمات؟ نحتاج إلى التفكير في كائنات اللعبة كأنها مستطيلات تتحرك. لماذا؟ لأن الصورة المستخدمة لرسم كائن اللعبة هي مستطيل: لها `x`، `y`، `width` و`height`.

إذا تقاطع مستطيلان، مثل البطل والعدو، فهذا يعني حدوث تصادم. ما يجب أن يحدث بعد ذلك يعتمد على قواعد اللعبة. لتنفيذ اكتشاف التصادمات، تحتاج إلى ما يلي:

1. طريقة للحصول على تمثيل مستطيل لكائن اللعبة، مثل هذا:

   ```javascript
   rectFromGameObject() {
     return {
       top: this.y,
       left: this.x,
       bottom: this.y + this.height,
       right: this.x + this.width
     }
   }
   ```

2. وظيفة مقارنة، يمكن أن تبدو هذه الوظيفة كالتالي:

   ```javascript
   function intersectRect(r1, r2) {
     return !(r2.left > r1.right ||
       r2.right < r1.left ||
       r2.top > r1.bottom ||
       r2.bottom < r1.top);
   }
   ```

## كيف ندمر الأشياء

لتدمير الأشياء في اللعبة، تحتاج إلى إعلام اللعبة بعدم رسم هذا العنصر في دورة اللعبة التي يتم تشغيلها على فاصل زمني معين. يمكن القيام بذلك عن طريق وضع علامة على كائن اللعبة كـ *ميت* عندما يحدث شيء ما، مثل:

```javascript
// collision happened
enemy.dead = true
```

ثم يمكنك معالجة الكائنات *الميتة* قبل إعادة رسم الشاشة، مثل:

```javascript
gameObjects = gameObject.filter(go => !go.dead);
```

## كيف نطلق الليزر

إطلاق الليزر يعني الاستجابة لحدث مفتاح وإنشاء كائن يتحرك في اتجاه معين. لذلك، نحتاج إلى تنفيذ الخطوات التالية:

1. **إنشاء كائن ليزر**: من أعلى سفينة البطل، يبدأ في التحرك للأعلى نحو أعلى الشاشة عند إنشائه.
2. **إرفاق كود بحدث مفتاح**: نحتاج إلى اختيار مفتاح على لوحة المفاتيح يمثل إطلاق اللاعب لليزر.
3. **إنشاء كائن لعبة يبدو كأنه ليزر** عند الضغط على المفتاح.

## فترة التهدئة لليزر

يحتاج الليزر إلى الإطلاق في كل مرة تضغط فيها على مفتاح، مثل *المسافة* على سبيل المثال. لمنع اللعبة من إنتاج عدد كبير جدًا من الليزرات في وقت قصير، نحتاج إلى إصلاح ذلك. يتم ذلك عن طريق تنفيذ ما يسمى بـ *فترة التهدئة*، وهو مؤقت يضمن أن الليزر يمكن إطلاقه فقط بفاصل زمني معين. يمكنك تنفيذ ذلك بالطريقة التالية:

```javascript
class Cooldown {
  constructor(time) {
    this.cool = false;
    setTimeout(() => {
      this.cool = true;
    }, time)
  }
}

class Weapon {
  constructor {
  }
  fire() {
    if (!this.cooldown || this.cooldown.cool) {
      // produce a laser
      this.cooldown = new Cooldown(500);
    } else {
      // do nothing - it hasn't cooled down yet.
    }
  }
}
```

✅ ارجع إلى الدرس الأول في سلسلة لعبة الفضاء لتذكير نفسك بـ *فترات التهدئة*.

## ما الذي سنبنيه

ستأخذ الكود الموجود (الذي يجب أن تكون قد قمت بتنظيفه وإعادة تنظيمه) من الدرس السابق، وتقوم بتوسيعه. يمكنك البدء بالكود من الجزء الثاني أو استخدام الكود في [الجزء الثالث - البداية](../../../../../../../../../your-work).

> نصيحة: الليزر الذي ستعمل عليه موجود بالفعل في مجلد الأصول الخاص بك ومُشار إليه في الكود.

- **إضافة اكتشاف التصادمات**، عندما يصطدم الليزر بشيء ما، يجب أن تنطبق القواعد التالية:
   1. **الليزر يصيب العدو**: يموت العدو إذا أصيب بالليزر.
   2. **الليزر يصيب أعلى الشاشة**: يتم تدمير الليزر إذا أصاب الجزء العلوي من الشاشة.
   3. **تصادم العدو مع البطل**: يتم تدمير العدو والبطل إذا اصطدما ببعضهما.
   4. **العدو يصيب أسفل الشاشة**: يتم تدمير العدو والبطل إذا وصل العدو إلى أسفل الشاشة.

## الخطوات الموصى بها

حدد الملفات التي تم إنشاؤها لك في مجلد `your-work`. يجب أن تحتوي على ما يلي:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

ابدأ مشروعك في مجلد `your_work` بكتابة:

```bash
cd your-work
npm start
```

سيؤدي ذلك إلى تشغيل خادم HTTP على العنوان `http://localhost:5000`. افتح متصفحًا وأدخل هذا العنوان، في الوقت الحالي يجب أن يعرض البطل وجميع الأعداء، ولكن لا شيء يتحرك - حتى الآن :).

### إضافة الكود

1. **إعداد تمثيل مستطيل لكائن اللعبة للتعامل مع التصادمات**. يتيح لك الكود أدناه الحصول على تمثيل مستطيل لـ `GameObject`. قم بتحرير فئة GameObject لتوسيعها:

    ```javascript
    rectFromGameObject() {
        return {
          top: this.y,
          left: this.x,
          bottom: this.y + this.height,
          right: this.x + this.width,
        };
      }
    ```

2. **إضافة كود يتحقق من التصادم**. ستكون هذه وظيفة جديدة تختبر ما إذا كان مستطيلان يتقاطعان:

    ```javascript
    function intersectRect(r1, r2) {
      return !(
        r2.left > r1.right ||
        r2.right < r1.left ||
        r2.top > r1.bottom ||
        r2.bottom < r1.top
      );
    }
    ```

3. **إضافة قدرة إطلاق الليزر**
   1. **إضافة رسالة حدث مفتاح**. يجب أن يقوم مفتاح *المسافة* بإنشاء ليزر فوق سفينة البطل. أضف ثلاث ثوابت في كائن Messages:

       ```javascript
        KEY_EVENT_SPACE: "KEY_EVENT_SPACE",
        COLLISION_ENEMY_LASER: "COLLISION_ENEMY_LASER",
        COLLISION_ENEMY_HERO: "COLLISION_ENEMY_HERO",
       ```

   1. **التعامل مع مفتاح المسافة**. قم بتحرير وظيفة `window.addEventListener` الخاصة بـ keyup للتعامل مع مفتاح المسافة:

      ```javascript
        } else if(evt.keyCode === 32) {
          eventEmitter.emit(Messages.KEY_EVENT_SPACE);
        }
      ```

    1. **إضافة مستمعين**. قم بتحرير وظيفة `initGame()` للتأكد من أن البطل يمكنه الإطلاق عند الضغط على مفتاح المسافة:

       ```javascript
       eventEmitter.on(Messages.KEY_EVENT_SPACE, () => {
        if (hero.canFire()) {
          hero.fire();
        }
       ```

       وأضف وظيفة جديدة `eventEmitter.on()` لضمان السلوك عند اصطدام العدو بالليزر:

          ```javascript
          eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
            first.dead = true;
            second.dead = true;
          })
          ```

   1. **تحريك الكائن**. تأكد من أن الليزر يتحرك تدريجيًا إلى أعلى الشاشة. ستقوم بإنشاء فئة Laser جديدة تمتد من `GameObject`، كما فعلت من قبل:

      ```javascript
        class Laser extends GameObject {
        constructor(x, y) {
          super(x,y);
          (this.width = 9), (this.height = 33);
          this.type = 'Laser';
          this.img = laserImg;
          let id = setInterval(() => {
            if (this.y > 0) {
              this.y -= 15;
            } else {
              this.dead = true;
              clearInterval(id);
            }
          }, 100)
        }
      }
      ```

   1. **التعامل مع التصادمات**. قم بتنفيذ قواعد التصادم لليزر. أضف وظيفة `updateGameObjects()` التي تختبر الكائنات المتصادمة:

      ```javascript
      function updateGameObjects() {
        const enemies = gameObjects.filter(go => go.type === 'Enemy');
        const lasers = gameObjects.filter((go) => go.type === "Laser");
      // laser hit something
        lasers.forEach((l) => {
          enemies.forEach((m) => {
            if (intersectRect(l.rectFromGameObject(), m.rectFromGameObject())) {
            eventEmitter.emit(Messages.COLLISION_ENEMY_LASER, {
              first: l,
              second: m,
            });
          }
         });
      });

        gameObjects = gameObjects.filter(go => !go.dead);
      }  
      ```

      تأكد من إضافة `updateGameObjects()` إلى دورة اللعبة في `window.onload`.

   4. **تنفيذ فترة التهدئة** لليزر، بحيث يمكن إطلاقه فقط بفاصل زمني معين.

      أخيرًا، قم بتحرير فئة Hero بحيث يمكنها التعامل مع فترة التهدئة:

       ```javascript
      class Hero extends GameObject {
        constructor(x, y) {
          super(x, y);
          (this.width = 99), (this.height = 75);
          this.type = "Hero";
          this.speed = { x: 0, y: 0 };
          this.cooldown = 0;
        }
        fire() {
          gameObjects.push(new Laser(this.x + 45, this.y - 10));
          this.cooldown = 500;
    
          let id = setInterval(() => {
            if (this.cooldown > 0) {
              this.cooldown -= 100;
            } else {
              clearInterval(id);
            }
          }, 200);
        }
        canFire() {
          return this.cooldown === 0;
        }
      }
      ```

في هذه المرحلة، أصبحت لعبتك تحتوي على بعض الوظائف! يمكنك التنقل باستخدام مفاتيح الأسهم، إطلاق الليزر باستخدام مفتاح المسافة، واختفاء الأعداء عند إصابتهم. عمل رائع!

---

## 🚀 التحدي

أضف انفجارًا! ألقِ نظرة على أصول اللعبة في [مستودع Space Art](../../../../6-space-game/solution/spaceArt/readme.txt) وحاول إضافة انفجار عندما يصيب الليزر كائنًا فضائيًا.

## اختبار ما بعد المحاضرة

[اختبار ما بعد المحاضرة](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/36)

## المراجعة والدراسة الذاتية

جرّب تغيير الفواصل الزمنية في لعبتك حتى الآن. ماذا يحدث عند تغييرها؟ اقرأ المزيد عن [أحداث توقيت JavaScript](https://www.freecodecamp.org/news/javascript-timing-events-settimeout-and-setinterval/).

## الواجب

[استكشاف التصادمات](assignment.md)

**إخلاء المسؤولية**:  
تم ترجمة هذا المستند باستخدام خدمة الترجمة بالذكاء الاصطناعي [Co-op Translator](https://github.com/Azure/co-op-translator). بينما نسعى لتحقيق الدقة، يرجى العلم أن الترجمات الآلية قد تحتوي على أخطاء أو معلومات غير دقيقة. يجب اعتبار المستند الأصلي بلغته الأصلية المصدر الرسمي. للحصول على معلومات حاسمة، يُوصى بالاستعانة بترجمة بشرية احترافية. نحن غير مسؤولين عن أي سوء فهم أو تفسيرات خاطئة تنشأ عن استخدام هذه الترجمة.