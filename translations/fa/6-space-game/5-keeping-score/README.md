<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "4e8250db84b027c9ff816b4e4c093457",
  "translation_date": "2025-08-24T12:27:41+00:00",
  "source_file": "6-space-game/5-keeping-score/README.md",
  "language_code": "fa"
}
-->
# ساخت یک بازی فضایی قسمت ۵: امتیازدهی و جان‌ها

## آزمون پیش از درس

[آزمون پیش از درس](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/37)

در این درس، یاد می‌گیرید که چگونه به بازی امتیاز اضافه کنید و جان‌ها را محاسبه کنید.

## نمایش متن روی صفحه

برای نمایش امتیاز بازی روی صفحه، باید بدانید چگونه متن را روی صفحه قرار دهید. پاسخ استفاده از متد `fillText()` روی شیء canvas است. همچنین می‌توانید جنبه‌های دیگر مانند نوع فونت، رنگ متن و حتی تراز آن (چپ، راست، مرکز) را کنترل کنید. در زیر کدی برای نمایش متن روی صفحه آورده شده است.

```javascript
ctx.font = "30px Arial";
ctx.fillStyle = "red";
ctx.textAlign = "right";
ctx.fillText("show this on the screen", 0, 0);
```

✅ درباره [چگونگی افزودن متن به canvas](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_text) بیشتر بخوانید و متن خود را به شکل جذاب‌تری طراحی کنید!

## جان، به عنوان یک مفهوم بازی

مفهوم داشتن جان در یک بازی فقط یک عدد است. در زمینه یک بازی فضایی، معمولاً مجموعه‌ای از جان‌ها اختصاص داده می‌شود که با هر بار آسیب دیدن سفینه شما، یکی از آن‌ها کم می‌شود. بهتر است اگر بتوانید نمایش گرافیکی از این جان‌ها مانند سفینه‌های کوچک یا قلب‌ها به جای یک عدد نشان دهید.

## چه چیزی بسازیم

بیایید موارد زیر را به بازی خود اضافه کنیم:

- **امتیاز بازی**: برای هر سفینه دشمن که نابود می‌شود، به قهرمان باید امتیاز داده شود. پیشنهاد ما ۱۰۰ امتیاز برای هر سفینه است. امتیاز بازی باید در پایین سمت چپ نمایش داده شود.
- **جان**: سفینه شما سه جان دارد. هر بار که یک سفینه دشمن با شما برخورد کند، یک جان از دست می‌دهید. امتیاز جان باید در پایین سمت راست نمایش داده شود و از گرافیک زیر تشکیل شده باشد ![تصویر جان](../../../../6-space-game/5-keeping-score/solution/assets/life.png).

## مراحل پیشنهادی

فایل‌هایی که برای شما ایجاد شده‌اند را در پوشه `your-work` پیدا کنید. این پوشه باید شامل موارد زیر باشد:

```bash
-| assets
  -| enemyShip.png
  -| player.png
  -| laserRed.png
-| index.html
-| app.js
-| package.json
```

پروژه خود را در پوشه `your_work` با تایپ کردن دستور زیر شروع کنید:

```bash
cd your-work
npm start
```

دستور بالا یک سرور HTTP را در آدرس `http://localhost:5000` راه‌اندازی می‌کند. مرورگر خود را باز کنید و این آدرس را وارد کنید. در حال حاضر باید قهرمان و تمام دشمنان را نمایش دهد و وقتی کلیدهای جهت چپ و راست را فشار می‌دهید، قهرمان حرکت می‌کند و می‌تواند دشمنان را نابود کند.

### افزودن کد

1. **کپی کردن دارایی‌های مورد نیاز** از پوشه `solution/assets/` به پوشه `your-work`؛ شما باید دارایی `life.png` را اضافه کنید. `lifeImg` را به تابع window.onload اضافه کنید:

    ```javascript
    lifeImg = await loadTexture("assets/life.png");
    ```

1. `lifeImg` را به لیست دارایی‌ها اضافه کنید:

    ```javascript
    let heroImg,
    ...
    lifeImg,
    ...
    eventEmitter = new EventEmitter();
    ```
  
2. **افزودن متغیرها**. کدی اضافه کنید که امتیاز کل شما (۰) و تعداد جان‌های باقی‌مانده (۳) را نمایش دهد.

3. **گسترش تابع `updateGameObjects()`**. تابع `updateGameObjects()` را برای مدیریت برخوردهای دشمن گسترش دهید:

    ```javascript
    enemies.forEach(enemy => {
        const heroRect = hero.rectFromGameObject();
        if (intersectRect(heroRect, enemy.rectFromGameObject())) {
          eventEmitter.emit(Messages.COLLISION_ENEMY_HERO, { enemy });
        }
      })
    ```

4. **افزودن `life` و `points`**. 
   1. **مقداردهی اولیه متغیرها**. زیر `this.cooldown = 0` در کلاس `Hero`، جان و امتیاز را تنظیم کنید:

        ```javascript
        this.life = 3;
        this.points = 0;
        ```

   1. **نمایش متغیرها روی صفحه**. این مقادیر را روی صفحه نمایش دهید:

        ```javascript
        function drawLife() {
          // TODO, 35, 27
          const START_POS = canvas.width - 180;
          for(let i=0; i < hero.life; i++ ) {
            ctx.drawImage(
              lifeImg, 
              START_POS + (45 * (i+1) ), 
              canvas.height - 37);
          }
        }
        
        function drawPoints() {
          ctx.font = "30px Arial";
          ctx.fillStyle = "red";
          ctx.textAlign = "left";
          drawText("Points: " + hero.points, 10, canvas.height-20);
        }
        
        function drawText(message, x, y) {
          ctx.fillText(message, x, y);
        }

        ```

   1. **افزودن متدها به حلقه بازی**. مطمئن شوید که این توابع را به تابع window.onload زیر `updateGameObjects()` اضافه کرده‌اید:

        ```javascript
        drawPoints();
        drawLife();
        ```

1. **پیاده‌سازی قوانین بازی**. قوانین زیر را پیاده‌سازی کنید:

   1. **برای هر برخورد قهرمان و دشمن**، یک جان کم کنید.
   
      کلاس `Hero` را برای انجام این کاهش گسترش دهید:

        ```javascript
        decrementLife() {
          this.life--;
          if (this.life === 0) {
            this.dead = true;
          }
        }
        ```

   2. **برای هر لیزری که به دشمن برخورد کند**، امتیاز بازی را ۱۰۰ امتیاز افزایش دهید.

      کلاس Hero را برای انجام این افزایش گسترش دهید:
    
        ```javascript
          incrementPoints() {
            this.points += 100;
          }
        ```

        این توابع را به Event Emitters برخورد اضافه کنید:

        ```javascript
        eventEmitter.on(Messages.COLLISION_ENEMY_LASER, (_, { first, second }) => {
           first.dead = true;
           second.dead = true;
           hero.incrementPoints();
        })

        eventEmitter.on(Messages.COLLISION_ENEMY_HERO, (_, { enemy }) => {
           enemy.dead = true;
           hero.decrementLife();
        });
        ```

✅ کمی تحقیق کنید تا بازی‌های دیگری که با استفاده از JavaScript/Canvas ساخته شده‌اند را کشف کنید. ویژگی‌های مشترک آن‌ها چیست؟

در پایان این کار، باید سفینه‌های کوچک 'جان' را در پایین سمت راست، امتیازها را در پایین سمت چپ ببینید و باید مشاهده کنید که تعداد جان‌ها با برخورد با دشمنان کاهش می‌یابد و امتیازها با نابود کردن دشمنان افزایش می‌یابد. آفرین! بازی شما تقریباً کامل شده است.

---

## 🚀 چالش

کد شما تقریباً کامل است. آیا می‌توانید مراحل بعدی خود را تصور کنید؟

## آزمون پس از درس

[آزمون پس از درس](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/38)

## مرور و مطالعه شخصی

روش‌هایی را تحقیق کنید که می‌توانید امتیازها و جان‌های بازی را افزایش و کاهش دهید. موتورهای بازی جالبی مانند [PlayFab](https://playfab.com) وجود دارند. چگونه استفاده از یکی از این‌ها می‌تواند بازی شما را بهبود بخشد؟

## تکلیف

[ساخت یک بازی امتیازدهی](assignment.md)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم دقت را حفظ کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است حاوی خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما هیچ مسئولیتی در قبال سوءتفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.