<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "01336cddd638242e99b133614111ea40",
  "translation_date": "2025-08-25T22:34:25+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "ur"
}
-->
# اسپیس گیم بنائیں حصہ 6: اختتام اور دوبارہ شروع کریں

## لیکچر سے پہلے کا کوئز

[لیکچر سے پہلے کا کوئز](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/39)

کسی گیم میں *اختتام کی حالت* کو ظاہر کرنے کے مختلف طریقے ہیں۔ یہ آپ پر منحصر ہے کہ آپ گیم کے تخلیق کار کے طور پر یہ طے کریں کہ گیم کیوں ختم ہوا۔ اگر ہم اس اسپیس گیم کی بات کریں جو آپ اب تک بنا رہے ہیں، تو یہاں کچھ وجوہات ہیں:

- **`N` دشمن جہاز تباہ ہو چکے ہیں**: یہ کافی عام ہے کہ اگر آپ گیم کو مختلف لیولز میں تقسیم کریں تو آپ کو ایک لیول مکمل کرنے کے لیے `N` دشمن جہاز تباہ کرنے ہوں گے۔
- **آپ کا جہاز تباہ ہو گیا ہے**: کچھ گیمز میں آپ گیم ہار جاتے ہیں اگر آپ کا جہاز تباہ ہو جائے۔ ایک اور عام طریقہ یہ ہے کہ آپ کے پاس "زندگیوں" کا تصور ہو۔ ہر بار جب آپ کا جہاز تباہ ہوتا ہے تو ایک زندگی کم ہو جاتی ہے۔ جب تمام زندگیاں ختم ہو جائیں تو آپ گیم ہار جاتے ہیں۔
- **آپ نے `N` پوائنٹس جمع کر لیے ہیں**: ایک اور عام اختتام کی حالت یہ ہے کہ آپ پوائنٹس جمع کریں۔ پوائنٹس کیسے حاصل کیے جائیں یہ آپ پر منحصر ہے، لیکن عام طور پر دشمن جہاز کو تباہ کرنے یا ان اشیاء کو جمع کرنے پر پوائنٹس دیے جاتے ہیں جو تباہ ہونے پر گرتی ہیں۔
- **ایک لیول مکمل کریں**: اس میں کئی شرائط شامل ہو سکتی ہیں جیسے `X` دشمن جہاز تباہ کرنا، `Y` پوائنٹس جمع کرنا یا شاید کوئی خاص شے حاصل کرنا۔

## دوبارہ شروع کرنا

اگر لوگ آپ کے گیم سے لطف اندوز ہوتے ہیں تو وہ اسے دوبارہ کھیلنا چاہیں گے۔ گیم کسی بھی وجہ سے ختم ہونے کے بعد آپ کو دوبارہ شروع کرنے کا آپشن دینا چاہیے۔

✅ ذرا سوچیں کہ کن حالات میں آپ کو لگتا ہے کہ گیم ختم ہو جاتا ہے، اور پھر آپ کو دوبارہ شروع کرنے کے لیے کیسے کہا جاتا ہے۔

## کیا بنانا ہے

آپ کو اپنے گیم میں یہ اصول شامل کرنے ہوں گے:

1. **گیم جیتنا**۔ جب تمام دشمن جہاز تباہ ہو جائیں، تو آپ گیم جیت جاتے ہیں۔ اس کے ساتھ ہی کوئی فتح کا پیغام بھی دکھائیں۔
1. **دوبارہ شروع کریں**۔ جب آپ کی تمام زندگیاں ختم ہو جائیں یا گیم جیت لیا جائے، تو آپ کو گیم دوبارہ شروع کرنے کا طریقہ فراہم کرنا چاہیے۔ یاد رکھیں! آپ کو گیم کو دوبارہ شروع کرنے کی ضرورت ہوگی اور پچھلی گیم کی حالت کو صاف کرنا ہوگا۔

## تجویز کردہ مراحل

`your-work` سب فولڈر میں وہ فائلیں تلاش کریں جو آپ کے لیے بنائی گئی ہیں۔ اس میں درج ذیل شامل ہونا چاہیے:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
  -| life.png
-| index.html
-| app.js
-| package.json
```

اپنا پروجیکٹ `your_work` فولڈر میں شروع کرنے کے لیے درج ذیل ٹائپ کریں:

```bash
cd your-work
npm start
```

اوپر دیا گیا کمانڈ ایک HTTP سرور ایڈریس `http://localhost:5000` پر شروع کرے گا۔ ایک براؤزر کھولیں اور یہ ایڈریس درج کریں۔ آپ کا گیم کھیلنے کے قابل حالت میں ہونا چاہیے۔

> ٹپ: Visual Studio Code میں وارننگز سے بچنے کے لیے، `window.onload` فنکشن میں `gameLoopId` کو ویسا ہی کال کریں (بغیر `let` کے)، اور فائل کے شروع میں `let gameLoopId;` کو الگ سے ڈکلیئر کریں۔

### کوڈ شامل کریں

1. **اختتام کی حالت کا ٹریک رکھیں**۔ ایسا کوڈ شامل کریں جو دشمنوں کی تعداد یا ہیرو جہاز کے تباہ ہونے کا حساب رکھے، ان دو فنکشنز کو شامل کر کے:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **پیغام ہینڈلرز میں لاجک شامل کریں**۔ `eventEmitter` کو ان حالات کو ہینڈل کرنے کے لیے ایڈٹ کریں:

    ```javascript
    eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
        first.dead = true;
        second.dead = true;
        hero.incrementPoints();

        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });

    eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
        enemy.dead = true;
        hero.decrementLife();
        if (isHeroDead())  {
          eventEmitter.emit(Messages.GAME_END_LOSS);
          return; // loss before victory
        }
        if (isEnemiesDead()) {
          eventEmitter.emit(Messages.GAME_END_WIN);
        }
    });
    
    eventEmitter.on(Messages.GAME_END_WIN, () => {
        endGame(true);
    });
      
    eventEmitter.on(Messages.GAME_END_LOSS, () => {
      endGame(false);
    });
    ```

1. **نئے پیغام کی اقسام شامل کریں**۔ ان پیغامات کو constants آبجیکٹ میں شامل کریں:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **دوبارہ شروع کرنے کا کوڈ**۔ ایسا کوڈ شامل کریں جو منتخب کردہ بٹن دبانے پر گیم کو دوبارہ شروع کرے۔

   1. **کلید `Enter` دبانے کو سنیں**۔ اپنے ونڈو کے eventListener کو اس کلید کو سننے کے لیے ایڈٹ کریں:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **دوبارہ شروع کرنے کا پیغام شامل کریں**۔ اس پیغام کو اپنے Messages constant میں شامل کریں:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **گیم کے اصول نافذ کریں**۔ درج ذیل گیم کے اصول نافذ کریں:

   1. **کھلاڑی کی جیت کی حالت**۔ جب تمام دشمن جہاز تباہ ہو جائیں، تو ایک فتح کا پیغام دکھائیں۔

      1. پہلے، ایک `displayMessage()` فنکشن بنائیں:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. ایک `endGame()` فنکشن بنائیں:

        ```javascript
        function endGame(win) {
          clearInterval(gameLoopId);
        
          // set a delay so we are sure any paints have finished
          setTimeout(() => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "black";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            if (win) {
              displayMessage(
                "Victory!!! Pew Pew... - Press [Enter] to start a new game Captain Pew Pew",
                "green"
              );
            } else {
              displayMessage(
                "You died !!! Press [Enter] to start a new game Captain Pew Pew"
              );
            }
          }, 200)  
        }
        ```

   1. **دوبارہ شروع کرنے کی لاجک**۔ جب تمام زندگیاں ختم ہو جائیں یا کھلاڑی گیم جیت جائے، تو دکھائیں کہ گیم دوبارہ شروع کیا جا سکتا ہے۔ اس کے علاوہ، جب *دوبارہ شروع کرنے* کی کلید دبائی جائے تو گیم دوبارہ شروع کریں (آپ فیصلہ کر سکتے ہیں کہ کون سی کلید دوبارہ شروع کرنے کے لیے میپ کی جائے)۔

      1. `resetGame()` فنکشن بنائیں:

        ```javascript
        function resetGame() {
          if (gameLoopId) {
            clearInterval(gameLoopId);
            eventEmitter.clear();
            initGame();
            gameLoopId = setInterval(() => {
              ctx.clearRect(0, 0, canvas.width, canvas.height);
              ctx.fillStyle = "black";
              ctx.fillRect(0, 0, canvas.width, canvas.height);
              drawPoints();
              drawLife();
              updateGameObjects();
              drawGameObjects(ctx);
            }, 100);
          }
        }
        ```

     1. `initGame()` میں گیم کو ری سیٹ کرنے کے لیے `eventEmitter` کو کال شامل کریں:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter میں ایک `clear()` فنکشن شامل کریں:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 مبارک ہو، کپتان! آپ کا گیم مکمل ہو گیا ہے! شاندار کام! 🚀 💥 👽

---

## 🚀 چیلنج

ایک آواز شامل کریں! کیا آپ گیم پلے کو بہتر بنانے کے لیے کوئی آواز شامل کر سکتے ہیں، مثلاً جب لیزر ہٹ کرے، یا ہیرو مر جائے یا جیت جائے؟ یہ دیکھیں [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) کہ جاوا اسکرپٹ کا استعمال کرتے ہوئے آواز کیسے چلائی جائے۔

## لیکچر کے بعد کا کوئز

[لیکچر کے بعد کا کوئز](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/40)

## جائزہ اور خود مطالعہ

آپ کا اسائنمنٹ ایک نیا نمونہ گیم بنانا ہے، تو کچھ دلچسپ گیمز کو دریافت کریں تاکہ آپ دیکھ سکیں کہ آپ کس قسم کا گیم بنا سکتے ہیں۔

## اسائنمنٹ

[ایک نمونہ گیم بنائیں](assignment.md)

**ڈسکلیمر**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ ہم درستگی کے لیے کوشش کرتے ہیں، لیکن براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا غیر درستیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔