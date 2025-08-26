<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "01336cddd638242e99b133614111ea40",
  "translation_date": "2025-08-25T22:35:57+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "ne"
}
-->
# स्पेस गेम बनाउनुहोस् भाग ६: अन्त्य र पुनः सुरु गर्नुहोस्

## प्रि-लेक्चर क्विज

[प्रि-लेक्चर क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/39)

खेलमा *अन्त्यको अवस्था* व्यक्त गर्ने विभिन्न तरिकाहरू छन्। खेलको सर्जकको रूपमा, खेल किन समाप्त भयो भन्ने कुरा तपाईंले निर्धारण गर्नुहुन्छ। यहाँ केही कारणहरू छन्, यदि हामीले अहिलेसम्म बनाउँदै आएको स्पेस गेमको कुरा गर्यौं भने:

- **`N` दुश्मन जहाजहरू नष्ट भएका छन्**: यदि तपाईंले खेललाई विभिन्न स्तरहरूमा विभाजन गर्नुभएको छ भने, `N` दुश्मन जहाजहरू नष्ट गर्नुपर्ने आवश्यकता सामान्य हुन्छ।
- **तपाईंको जहाज नष्ट भएको छ**: केही खेलहरूमा तपाईंको जहाज नष्ट भएमा खेल हारिन्छ। अर्को सामान्य तरिका भनेको जीवनको अवधारणा राख्नु हो। तपाईंको जहाज नष्ट हुँदा प्रत्येक पटक एउटा जीवन घट्छ। सबै जीवन समाप्त भएपछि खेल हारिन्छ।
- **तपाईंले `N` अंकहरू सङ्कलन गर्नुभएको छ**: अर्को सामान्य अन्त्य अवस्था भनेको अंक सङ्कलन गर्नु हो। कसरी अंक प्राप्त गर्ने भन्ने कुरा तपाईंको हातमा छ, तर सामान्यतया दुश्मन जहाज नष्ट गर्दा वा नष्ट हुँदा वस्तुहरू सङ्कलन गर्दा अंक प्रदान गरिन्छ।
- **स्तर पूरा गर्नुहोस्**: यसमा `X` दुश्मन जहाजहरू नष्ट गर्नु, `Y` अंक सङ्कलन गर्नु, वा कुनै विशेष वस्तु सङ्कलन गर्नु जस्ता विभिन्न अवस्थाहरू समावेश हुन सक्छ।

## पुनः सुरु गर्नुहोस्

यदि मानिसहरूले तपाईंको खेल मन पराउँछन् भने, उनीहरूले यसलाई फेरि खेल्न चाहने सम्भावना छ। खेल कुनै पनि कारणले समाप्त भएपछि, तपाईंले पुनः सुरु गर्ने विकल्प दिनुपर्छ।

✅ सोच्नुहोस्, कुन अवस्थाहरूमा खेल समाप्त हुन्छ, र त्यसपछि कसरी पुनः सुरु गर्न प्रेरित गरिन्छ।

## के निर्माण गर्ने

तपाईंले यी नियमहरू आफ्नो खेलमा थप्नु पर्नेछ:

1. **खेल जित्नुहोस्**। सबै दुश्मन जहाजहरू नष्ट भएपछि, तपाईं खेल जित्नुहुन्छ। साथै, कुनै प्रकारको विजय सन्देश देखाउनुहोस्।
1. **पुनः सुरु गर्नुहोस्**। सबै जीवन समाप्त भएपछि वा खेल जितेपछि, तपाईंले खेल पुनः सुरु गर्ने तरिका दिनुपर्छ। सम्झनुहोस्! तपाईंले खेललाई पुनः आरम्भ गर्नुपर्नेछ र अघिल्लो खेलको अवस्था खाली गर्नुपर्नेछ।

## सिफारिस गरिएका चरणहरू

`your-work` सब फोल्डरमा तपाईंका लागि बनाइएका फाइलहरू खोज्नुहोस्। यसमा निम्न समावेश हुनुपर्छ:

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

तपाईं आफ्नो प्रोजेक्ट `your_work` फोल्डरबाट यसरी सुरु गर्नुहोस्:

```bash
cd your-work
npm start
```

माथिको कमाण्डले `http://localhost:5000` ठेगानामा HTTP सर्भर सुरु गर्नेछ। ब्राउजर खोल्नुहोस् र उक्त ठेगाना प्रविष्ट गर्नुहोस्। तपाईंको खेल खेल्न सकिने अवस्थामा हुनुपर्छ।

> टिप: Visual Studio Code मा चेतावनीहरू रोक्न, `window.onload` फङ्सनलाई `gameLoopId` (बिना `let`) कल गर्न सम्पादन गर्नुहोस्, र फाइलको माथि `let gameLoopId;` स्वतन्त्र रूपमा घोषणा गर्नुहोस्।

### कोड थप्नुहोस्

1. **अन्त्यको अवस्था ट्र्याक गर्नुहोस्**। दुश्मनहरूको संख्या ट्र्याक गर्ने वा नायक जहाज नष्ट भएको छ कि छैन भनेर ट्र्याक गर्न निम्न दुई फङ्सनहरू थप्नुहोस्:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **सन्देश ह्यान्डलरहरूमा तर्क थप्नुहोस्**। `eventEmitter` सम्पादन गरेर यी अवस्थाहरू ह्यान्डल गर्नुहोस्:

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

1. **नयाँ सन्देश प्रकारहरू थप्नुहोस्**। यी सन्देशहरू constants object मा थप्नुहोस्:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **पुनः सुरु गर्ने कोड थप्नुहोस्**। चयन गरिएको बटन थिच्दा खेल पुनः सुरु गर्ने कोड थप्नुहोस्।

   1. **कुञ्जी थिच्ने `Enter` सुन्नुहोस्**। तपाईंको विन्डोको eventListener सम्पादन गरेर यो थिचाइ सुन्नुहोस्:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **पुनः सुरु सन्देश थप्नुहोस्**। यो सन्देश तपाईंको Messages constant मा थप्नुहोस्:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **खेलका नियमहरू कार्यान्वयन गर्नुहोस्**। निम्न खेलका नियमहरू कार्यान्वयन गर्नुहोस्:

   1. **खेल जित्ने अवस्था**। सबै दुश्मन जहाजहरू नष्ट भएपछि, विजय सन्देश देखाउनुहोस्।

      1. पहिले, `displayMessage()` फङ्सन बनाउनुहोस्:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. `endGame()` फङ्सन बनाउनुहोस्:

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

   1. **पुनः सुरु गर्ने तर्क**। सबै जीवन समाप्त भएपछि वा खेल जितेपछि, खेल पुनः सुरु गर्न सकिन्छ भन्ने देखाउनुहोस्। साथै, *पुनः सुरु* कुञ्जी थिच्दा खेल पुनः सुरु गर्नुहोस् (कुन कुञ्जी पुनः सुरु गर्न म्याप गरिने हो, तपाईंले निर्णय गर्न सक्नुहुन्छ)।

      1. `resetGame()` फङ्सन बनाउनुहोस्:

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

     1. `initGame()` मा `eventEmitter` लाई खेल पुनः सेट गर्न कल थप्नुहोस्:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter मा `clear()` फङ्सन थप्नुहोस्:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 बधाई छ, कप्तान! तपाईंको खेल पूरा भयो! राम्रो काम! 🚀 💥 👽

---

## 🚀 चुनौती

ध्वनि थप्नुहोस्! के तपाईं आफ्नो खेलमा ध्वनि थप्न सक्नुहुन्छ, जस्तै लेजर हिट हुँदा, नायक मर्दा वा जित्दा? JavaScript प्रयोग गरेर ध्वनि कसरी प्ले गर्ने भनेर सिक्न [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) हेर्नुहोस्।

## पोस्ट-लेक्चर क्विज

[पोस्ट-लेक्चर क्विज](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/40)

## समीक्षा र आत्म-अध्ययन

तपाईंको असाइनमेन्ट भनेको नयाँ नमूना खेल बनाउनु हो, त्यसैले केही रोचक खेलहरूको अन्वेषण गर्नुहोस् र तपाईंले कस्तो प्रकारको खेल बनाउन सक्नुहुन्छ भनेर हेर्नुहोस्।

## असाइनमेन्ट

[नमूना खेल बनाउनुहोस्](assignment.md)

**अस्वीकरण**:  
यो दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरेर अनुवाद गरिएको छ। हामी शुद्धताको लागि प्रयास गर्छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादहरूमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छ। यसको मूल भाषा मा रहेको मूल दस्तावेज़लाई आधिकारिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीको लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।