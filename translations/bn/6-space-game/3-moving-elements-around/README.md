<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "23f088add24f0f1fa51014a9e27ea280",
  "translation_date": "2025-08-25T22:10:44+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "bn"
}
-->
# মহাকাশ গেম তৈরি করুন পার্ট ৩: গতি যোগ করা

## প্রাক-লেকচার কুইজ

[প্রাক-লেকচার কুইজ](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/33)

গেম তখনই মজার হয় যখন পর্দায় এলিয়েনরা ঘুরে বেড়ায়! এই গেমে আমরা দুটি ধরণের গতি ব্যবহার করব:

- **কিবোর্ড/মাউস গতি**: যখন ব্যবহারকারী কিবোর্ড বা মাউস ব্যবহার করে পর্দায় একটি বস্তু সরায়।
- **গেম দ্বারা সৃষ্ট গতি**: যখন গেম একটি নির্দিষ্ট সময় ব্যবধানে একটি বস্তু সরায়।

তাহলে আমরা কীভাবে পর্দায় জিনিস সরাই? এটি সবই কার্টেসিয়ান কোঅর্ডিনেটস নিয়ে: আমরা বস্তুর অবস্থান (x, y) পরিবর্তন করি এবং তারপর পর্দা পুনরায় আঁকি।

সাধারণত পর্দায় *গতি* অর্জনের জন্য আপনাকে নিম্নলিখিত ধাপগুলি অনুসরণ করতে হয়:

1. **নতুন অবস্থান নির্ধারণ করুন** একটি বস্তুর জন্য; এটি প্রয়োজন যাতে বস্তুটি সরানো হয়েছে বলে মনে হয়।
2. **পর্দা পরিষ্কার করুন**, পর্দা পুনরায় আঁকার মধ্যে পরিষ্কার করতে হবে। আমরা এটি একটি ব্যাকগ্রাউন্ড রঙ দিয়ে একটি আয়তক্ষেত্র আঁকার মাধ্যমে পরিষ্কার করতে পারি।
3. **নতুন অবস্থানে বস্তু পুনরায় আঁকুন**। এটি করে আমরা অবশেষে একটি অবস্থান থেকে অন্য অবস্থানে বস্তুটি সরানোর কাজ সম্পন্ন করি।

কোডে এটি দেখতে এমন হতে পারে:

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

✅ আপনি কি ভাবতে পারেন কেন আপনার হিরোকে প্রতি সেকেন্ডে অনেক ফ্রেমে পুনরায় আঁকা পারফরম্যান্স খরচ বাড়াতে পারে? [এই প্যাটার্নের বিকল্পগুলি](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) সম্পর্কে পড়ুন।

## কিবোর্ড ইভেন্ট পরিচালনা করুন

আপনি ইভেন্ট পরিচালনা করেন নির্দিষ্ট ইভেন্টগুলিকে কোডের সাথে সংযুক্ত করে। কিবোর্ড ইভেন্টগুলি পুরো উইন্ডোতে ট্রিগার হয়, যেখানে মাউস ইভেন্ট যেমন `click` একটি নির্দিষ্ট উপাদান ক্লিক করার সাথে সংযুক্ত হতে পারে। আমরা এই প্রকল্পে কিবোর্ড ইভেন্ট ব্যবহার করব।

একটি ইভেন্ট পরিচালনা করতে আপনাকে উইন্ডোর `addEventListener()` পদ্ধতি ব্যবহার করতে হবে এবং এটিকে দুটি ইনপুট প্যারামিটার দিতে হবে। প্রথম প্যারামিটারটি ইভেন্টের নাম, যেমন `keyup`। দ্বিতীয় প্যারামিটারটি সেই ফাংশন যা ইভেন্ট ঘটার ফলে আহ্বান করা উচিত।

এখানে একটি উদাহরণ:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

কী ইভেন্টের জন্য ইভেন্টে দুটি প্রপার্টি রয়েছে যা আপনি দেখতে পারেন কোন কী চাপা হয়েছে:

- `key`, এটি চাপা কী-এর একটি স্ট্রিং উপস্থাপনা, যেমন `ArrowUp`
- `keyCode`, এটি একটি সংখ্যার উপস্থাপনা, যেমন `37`, যা `ArrowLeft` এর সাথে মিলে যায়।

✅ কী ইভেন্ট ম্যানিপুলেশন গেম ডেভেলপমেন্টের বাইরেও কার্যকর। এই কৌশলটির জন্য আপনি আর কী কী ব্যবহার ভাবতে পারেন?

### বিশেষ কী: একটি সতর্কতা

কিছু *বিশেষ* কী রয়েছে যা উইন্ডোকে প্রভাবিত করে। এর মানে হল যে আপনি যদি একটি `keyup` ইভেন্ট শুনছেন এবং এই বিশেষ কী ব্যবহার করে আপনার হিরোকে সরান, এটি অনুভূমিক স্ক্রলিংও করবে। এই কারণে আপনি যখন আপনার গেম তৈরি করবেন তখন এই বিল্ট-ইন ব্রাউজার আচরণটি *বন্ধ* করতে চাইতে পারেন। এর জন্য আপনাকে এমন কোড প্রয়োজন:

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

উপরের কোডটি নিশ্চিত করবে যে অ্যারো-কী এবং স্পেস কী-এর *ডিফল্ট* আচরণ বন্ধ হয়ে গেছে। *বন্ধ* করার প্রক্রিয়া ঘটে যখন আমরা `e.preventDefault()` কল করি।

## গেম দ্বারা সৃষ্ট গতি

আমরা `setTimeout()` বা `setInterval()` ফাংশন ব্যবহার করে টাইমার দিয়ে জিনিসগুলিকে নিজে থেকেই সরাতে পারি, যা প্রতিটি টিক বা সময় ব্যবধানে বস্তুর অবস্থান আপডেট করে। এটি দেখতে এমন হতে পারে:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## গেম লুপ

গেম লুপ একটি ধারণা যা মূলত একটি ফাংশন যা নিয়মিত ব্যবধানে আহ্বান করা হয়। এটি গেম লুপ বলা হয় কারণ ব্যবহারকারীর কাছে দৃশ্যমান হওয়া উচিত এমন সবকিছু লুপে আঁকা হয়। গেম লুপ গেমের অংশ হওয়া সমস্ত গেম অবজেক্ট ব্যবহার করে, তাদের সবাইকে আঁকে যদি না কোনো কারণে তারা আর গেমের অংশ না থাকে। উদাহরণস্বরূপ, যদি একটি অবজেক্ট একটি শত্রু হয় যা লেজার দ্বারা আঘাতপ্রাপ্ত হয় এবং বিস্ফোরিত হয়, এটি আর বর্তমান গেম লুপের অংশ নয় (আপনি পরবর্তী পাঠে এটি সম্পর্কে আরও শিখবেন)।

গেম লুপ সাধারণত কোডে এমন দেখতে পারে:

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

উপরের লুপটি প্রতি `200` মিলিসেকেন্ডে ক্যানভাস পুনরায় আঁকতে আহ্বান করা হয়। আপনার গেমের জন্য সবচেয়ে ভালো সময় ব্যবধান বেছে নেওয়ার ক্ষমতা আপনার রয়েছে।

## মহাকাশ গেম চালিয়ে যাওয়া

আপনি বিদ্যমান কোডটি নিয়ে এটি প্রসারিত করবেন। হয় আপনি পার্ট I-এ সম্পন্ন করা কোড দিয়ে শুরু করুন অথবা [পার্ট II-স্টার্টার](../../../../6-space-game/3-moving-elements-around/your-work) এর কোড ব্যবহার করুন।

- **হিরোকে সরানো**: আপনি কোড যোগ করবেন যাতে আপনি অ্যারো কী ব্যবহার করে হিরোকে সরাতে পারেন।
- **শত্রুদের সরানো**: আপনাকে কোড যোগ করতে হবে যাতে শত্রুরা একটি নির্দিষ্ট হারে উপরে থেকে নিচে সরতে পারে।

## সুপারিশকৃত ধাপ

`your-work` সাব ফোল্ডারে তৈরি করা ফাইলগুলি খুঁজুন। এটি নিম্নলিখিতটি ধারণ করা উচিত:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

আপনার প্রকল্পটি `your_work` ফোল্ডারে শুরু করুন টাইপ করে:

```bash
cd your-work
npm start
```

উপরেরটি ঠিকানা `http://localhost:5000` এ একটি HTTP সার্ভার শুরু করবে। একটি ব্রাউজার খুলুন এবং সেই ঠিকানা ইনপুট করুন, এখন এটি হিরো এবং সমস্ত শত্রুদের রেন্ডার করা উচিত; কিছুই এখনও সরছে না!

### কোড যোগ করুন

1. **নির্দিষ্ট অবজেক্ট যোগ করুন** `hero`, `enemy` এবং `game object` এর জন্য, তাদের `x` এবং `y` প্রপার্টি থাকা উচিত। ([Inheritance or composition](../README.md) অংশটি মনে রাখুন)।

   *ইঙ্গিত* `game object` হওয়া উচিত যার `x` এবং `y` এবং নিজেকে ক্যানভাসে আঁকার ক্ষমতা রয়েছে।

   >টিপ: একটি নতুন GameObject ক্লাস যোগ করে শুরু করুন যার কনস্ট্রাক্টর নিচের মতো নির্ধারিত, এবং তারপর এটি ক্যানভাসে আঁকুন:
  
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

    এখন, এই GameObject প্রসারিত করে Hero এবং Enemy তৈরি করুন।
    
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

2. **কী-ইভেন্ট হ্যান্ডলার যোগ করুন** কী নেভিগেশনের জন্য (হিরোকে উপরে/নিচে, বামে/ডানে সরান)

   *মনে রাখুন* এটি একটি কার্টেসিয়ান সিস্টেম, উপরের-বাম কোণটি `0,0`। এছাড়াও *ডিফল্ট আচরণ* বন্ধ করার কোড যোগ করতে ভুলবেন না।

   >টিপ: আপনার onKeyDown ফাংশন তৈরি করুন এবং এটি উইন্ডোর সাথে সংযুক্ত করুন:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```
    
   এই পর্যায়ে আপনার ব্রাউজার কনসোল পরীক্ষা করুন এবং কীস্ট্রোকগুলি লগ হচ্ছে দেখুন।

3. **প্রয়োগ করুন** [Pub sub pattern](../README.md), এটি আপনার কোড পরিষ্কার রাখবে যখন আপনি বাকি অংশগুলি অনুসরণ করবেন।

   এটি করার জন্য, আপনি:

   1. **একটি ইভেন্ট লিসেনার যোগ করুন** উইন্ডোতে:

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

    1. **একটি EventEmitter ক্লাস তৈরি করুন** বার্তা প্রকাশ এবং সাবস্ক্রাইব করতে:

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

    1. **কনস্ট্যান্ট যোগ করুন** এবং EventEmitter সেট আপ করুন:

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

    1. **গেমটি ইনিশিয়ালাইজ করুন**

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

1. **গেম লুপ সেট আপ করুন**

   window.onload ফাংশনটি রিফ্যাক্টর করুন গেমটি ইনিশিয়ালাইজ করতে এবং একটি ভালো ব্যবধানে একটি গেম লুপ সেট আপ করতে। আপনি একটি লেজার বিমও যোগ করবেন:

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

5. **কোড যোগ করুন** শত্রুদের একটি নির্দিষ্ট ব্যবধানে সরানোর জন্য

    `createEnemies()` ফাংশনটি রিফ্যাক্টর করুন শত্রু তৈরি করতে এবং সেগুলিকে নতুন gameObjects ক্লাসে ঠেলে দিতে:

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
    
    এবং একটি `createHero()` ফাংশন যোগ করুন হিরোর জন্য একই প্রক্রিয়া করতে।
    
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

    এবং অবশেষে, একটি `drawGameObjects()` ফাংশন যোগ করুন আঁকা শুরু করতে:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    আপনার শত্রুরা আপনার হিরো স্পেসশিপের দিকে অগ্রসর হতে শুরু করবে!

---

## 🚀 চ্যালেঞ্জ

যেমনটি আপনি দেখতে পাচ্ছেন, আপনার কোড 'স্প্যাগেটি কোড'-এ পরিণত হতে পারে যখন আপনি ফাংশন, ভেরিয়েবল এবং ক্লাস যোগ করতে শুরু করেন। কীভাবে আপনি আপনার কোড আরও পড়ার যোগ্য করতে আরও ভালোভাবে সংগঠিত করতে পারেন? এমন একটি সিস্টেম স্কেচ করুন যা আপনার কোড সংগঠিত করে, এমনকি যদি এটি এখনও একটি ফাইলেই থাকে।

## পোস্ট-লেকচার কুইজ

[পোস্ট-লেকচার কুইজ](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/34)

## পর্যালোচনা ও স্ব-অধ্যয়ন

যদিও আমরা ফ্রেমওয়ার্ক ব্যবহার না করে আমাদের গেম লিখছি, গেম ডেভেলপমেন্টের জন্য অনেক জাভাস্ক্রিপ্ট-ভিত্তিক ক্যানভাস ফ্রেমওয়ার্ক রয়েছে। [এই সম্পর্কে পড়ার](https://github.com/collections/javascript-game-engines) জন্য কিছু সময় নিন।

## অ্যাসাইনমেন্ট

[আপনার কোডে মন্তব্য যোগ করুন](assignment.md)

**অস্বীকৃতি**:  
এই নথিটি AI অনুবাদ পরিষেবা [Co-op Translator](https://github.com/Azure/co-op-translator) ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসাধ্য সঠিকতা নিশ্চিত করার চেষ্টা করি, তবে অনুগ্রহ করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ত্রুটি বা অসঙ্গতি থাকতে পারে। মূল ভাষায় থাকা নথিটিকে প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য, পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যা হলে আমরা তার জন্য দায়ী থাকব না।