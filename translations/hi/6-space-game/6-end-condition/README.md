<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "01336cddd638242e99b133614111ea40",
  "translation_date": "2025-08-24T12:43:45+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "hi"
}
-->
# स्पेस गेम बनाएं भाग 6: समाप्ति और पुनः प्रारंभ

## प्री-लेक्चर क्विज़

[प्री-लेक्चर क्विज़](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/39)

किसी गेम में *समाप्ति की स्थिति* व्यक्त करने के कई तरीके होते हैं। यह गेम के निर्माता के रूप में आप पर निर्भर करता है कि आप तय करें कि गेम क्यों समाप्त हुआ। यदि हम अब तक बनाए गए स्पेस गेम की बात करें, तो यहां कुछ संभावित कारण दिए गए हैं:

- **`N` दुश्मन जहाज नष्ट हो गए हैं**: यह काफी सामान्य है, खासकर यदि आप गेम को विभिन्न स्तरों में विभाजित करते हैं, तो आपको एक स्तर पूरा करने के लिए `N` दुश्मन जहाजों को नष्ट करना होगा।
- **आपका जहाज नष्ट हो गया है**: ऐसे कई गेम होते हैं जहां आपका जहाज नष्ट होने पर आप गेम हार जाते हैं। एक और सामान्य तरीका यह है कि गेम में "लाइव्स" की अवधारणा हो। हर बार जब आपका जहाज नष्ट होता है, तो एक जीवन कम हो जाता है। जब सभी जीवन समाप्त हो जाते हैं, तो आप गेम हार जाते हैं।
- **आपने `N` अंक एकत्र किए हैं**: एक और सामान्य समाप्ति की स्थिति यह है कि आप अंक एकत्र करें। अंक कैसे प्राप्त किए जाते हैं, यह आप पर निर्भर करता है, लेकिन आमतौर पर दुश्मन जहाज को नष्ट करने या उन वस्तुओं को एकत्र करने पर अंक दिए जाते हैं जो नष्ट होने पर गिरती हैं।
- **एक स्तर पूरा करें**: इसमें कई स्थितियां शामिल हो सकती हैं, जैसे `X` दुश्मन जहाज नष्ट करना, `Y` अंक एकत्र करना, या शायद कोई विशेष वस्तु एकत्र करना।

## पुनः प्रारंभ करना

यदि लोग आपके गेम का आनंद लेते हैं, तो वे इसे फिर से खेलना चाहेंगे। किसी भी कारण से गेम समाप्त होने के बाद, आपको इसे पुनः प्रारंभ करने का विकल्प देना चाहिए।

✅ सोचें कि किन स्थितियों में आपको लगता है कि कोई गेम समाप्त होता है, और फिर आपको इसे पुनः प्रारंभ करने के लिए कैसे प्रेरित किया जाता है।

## क्या बनाना है

आपको अपने गेम में ये नियम जोड़ने होंगे:

1. **गेम जीतना**। जब सभी दुश्मन जहाज नष्ट हो जाते हैं, तो आप गेम जीत जाते हैं। इसके अतिरिक्त, किसी प्रकार का विजय संदेश प्रदर्शित करें।
2. **पुनः प्रारंभ**। जब आपके सभी जीवन समाप्त हो जाते हैं या गेम जीत लिया जाता है, तो आपको गेम को पुनः प्रारंभ करने का विकल्प देना चाहिए। याद रखें! आपको गेम को फिर से प्रारंभ करना होगा और पिछले गेम की स्थिति को साफ़ करना होगा।

## अनुशंसित चरण

`your-work` सब फोल्डर में आपके लिए बनाए गए फाइल्स को ढूंढें। इसमें निम्नलिखित फाइल्स होनी चाहिए:

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

आप अपने प्रोजेक्ट को `your_work` फोल्डर में इस कमांड से शुरू करें:

```bash
cd your-work
npm start
```

उपरोक्त कमांड एक HTTP सर्वर को `http://localhost:5000` पते पर शुरू करेगा। एक ब्राउज़र खोलें और इस पते को दर्ज करें। आपका गेम खेलने योग्य स्थिति में होना चाहिए।

> टिप: Visual Studio Code में चेतावनियों से बचने के लिए, `window.onload` फ़ंक्शन को `gameLoopId` को वैसे ही कॉल करने के लिए संपादित करें (बिना `let` के), और फ़ाइल के शीर्ष पर स्वतंत्र रूप से `let gameLoopId;` घोषित करें।

### कोड जोड़ें

1. **समाप्ति की स्थिति को ट्रैक करें**। कोड जोड़ें जो दुश्मनों की संख्या को ट्रैक करता है, या यदि हीरो जहाज नष्ट हो गया है, तो इन दो फ़ंक्शन्स को जोड़ें:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **संदेश हैंडलर्स में लॉजिक जोड़ें**। `eventEmitter` को संपादित करें ताकि ये स्थितियां संभाली जा सकें:

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

1. **नए संदेश प्रकार जोड़ें**। इन संदेशों को constants ऑब्जेक्ट में जोड़ें:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **पुनः प्रारंभ कोड जोड़ें**। एक चयनित बटन दबाने पर गेम को पुनः प्रारंभ करने का कोड जोड़ें।

   1. **कुंजी दबाव `Enter` सुनें**। अपने विंडो के eventListener को इस दबाव को सुनने के लिए संपादित करें:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **पुनः प्रारंभ संदेश जोड़ें**। इस संदेश को अपने Messages constant में जोड़ें:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **गेम नियम लागू करें**। निम्नलिखित गेम नियम लागू करें:

   1. **प्लेयर जीतने की स्थिति**। जब सभी दुश्मन जहाज नष्ट हो जाते हैं, तो एक विजय संदेश प्रदर्शित करें।

      1. पहले, एक `displayMessage()` फ़ंक्शन बनाएं:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. एक `endGame()` फ़ंक्शन बनाएं:

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

   1. **पुनः प्रारंभ लॉजिक**। जब सभी जीवन समाप्त हो जाते हैं या खिलाड़ी गेम जीत जाता है, तो प्रदर्शित करें कि गेम को पुनः प्रारंभ किया जा सकता है। इसके अतिरिक्त, जब *पुनः प्रारंभ* कुंजी दबाई जाती है, तो गेम को पुनः प्रारंभ करें (आप तय कर सकते हैं कि कौन सी कुंजी पुनः प्रारंभ के लिए मैप की जाए)।

      1. `resetGame()` फ़ंक्शन बनाएं:

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

     1. `initGame()` में गेम को रीसेट करने के लिए `eventEmitter` को कॉल जोड़ें:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter में एक `clear()` फ़ंक्शन जोड़ें:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 बधाई हो, कप्तान! आपका गेम पूरा हो गया है! बहुत अच्छा काम किया! 🚀 💥 👽

---

## 🚀 चुनौती

एक ध्वनि जोड़ें! क्या आप अपने गेम में ध्वनि जोड़ सकते हैं ताकि गेमप्ले को और बेहतर बनाया जा सके, जैसे लेज़र हिट होने पर, या हीरो के मरने या जीतने पर? यह जानने के लिए कि जावास्क्रिप्ट का उपयोग करके ध्वनि कैसे चलाई जाती है, इस [सैंडबॉक्स](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) को देखें।

## पोस्ट-लेक्चर क्विज़

[पोस्ट-लेक्चर क्विज़](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/40)

## समीक्षा और स्व-अध्ययन

आपका असाइनमेंट एक नया सैंपल गेम बनाना है, इसलिए वहां मौजूद कुछ दिलचस्प गेम्स का पता लगाएं ताकि आप देख सकें कि आप किस प्रकार का गेम बना सकते हैं।

## असाइनमेंट

[सैंपल गेम बनाएं](assignment.md)

**अस्वीकरण**:  
यह दस्तावेज़ AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) का उपयोग करके अनुवादित किया गया है। जबकि हम सटीकता के लिए प्रयासरत हैं, कृपया ध्यान दें कि स्वचालित अनुवाद में त्रुटियां या अशुद्धियां हो सकती हैं। मूल भाषा में उपलब्ध मूल दस्तावेज़ को प्रामाणिक स्रोत माना जाना चाहिए। महत्वपूर्ण जानकारी के लिए, पेशेवर मानव अनुवाद की सिफारिश की जाती है। इस अनुवाद के उपयोग से उत्पन्न किसी भी गलतफहमी या गलत व्याख्या के लिए हम उत्तरदायी नहीं हैं।