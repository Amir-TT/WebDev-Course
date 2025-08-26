<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "01336cddd638242e99b133614111ea40",
  "translation_date": "2025-08-25T22:35:35+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "mr"
}
-->
# स्पेस गेम तयार करा भाग 6: शेवट आणि पुन्हा सुरू करा

## पूर्व-व्याख्यान प्रश्नमंजुषा

[पूर्व-व्याख्यान प्रश्नमंजुषा](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/39)

एखाद्या गेममध्ये *शेवटाची अट* व्यक्त करण्याचे वेगवेगळे मार्ग असतात. गेम तयार करणाऱ्या व्यक्तीवर अवलंबून असते की गेम का संपला आहे हे सांगणे. जर आपण आतापर्यंत तयार केलेल्या स्पेस गेमबद्दल बोलत असू, तर खालील काही कारणे असू शकतात:

- **`N` शत्रू जहाजे नष्ट झाली आहेत**: जर तुम्ही गेम वेगवेगळ्या स्तरांमध्ये विभागला असेल, तर `N` शत्रू जहाजे नष्ट करणे हा स्तर पूर्ण करण्याचा सामान्य नियम असतो.
- **तुमचे जहाज नष्ट झाले आहे**: असे अनेक गेम्स आहेत जिथे तुमचे जहाज नष्ट झाले तर तुम्ही गेम हरता. आणखी एक सामान्य पद्धत म्हणजे "जीव" ही संकल्पना असते. प्रत्येक वेळी तुमचे जहाज नष्ट झाले की एक जीव कमी होतो. सर्व जीव संपल्यावर तुम्ही गेम हरता.
- **तुम्ही `N` गुण मिळवले आहेत**: आणखी एक सामान्य शेवटाची अट म्हणजे गुण गोळा करणे. गुण कसे मिळवायचे हे तुमच्यावर अवलंबून आहे, परंतु शत्रू जहाज नष्ट करणे किंवा नष्ट झाल्यावर वस्तू गोळा करणे यासारख्या क्रियांना गुण देणे सामान्य आहे.
- **स्तर पूर्ण करा**: यामध्ये `X` शत्रू जहाजे नष्ट करणे, `Y` गुण गोळा करणे किंवा विशिष्ट वस्तू गोळा करणे यासारख्या अनेक अटींचा समावेश असू शकतो.

## पुन्हा सुरू करणे

जर लोकांना तुमचा गेम आवडला, तर ते तो पुन्हा खेळण्याची शक्यता आहे. कोणत्याही कारणाने गेम संपल्यावर तुम्ही पुन्हा सुरू करण्याचा पर्याय द्यायला हवा.

✅ विचार करा की कोणत्या अटींवर गेम संपतो आणि तुम्हाला पुन्हा सुरू करण्यासाठी कसे प्रोत्साहित केले जाते.

## काय तयार करायचे

तुम्ही तुमच्या गेममध्ये खालील नियम जोडणार आहात:

1. **गेम जिंकणे**. सर्व शत्रू जहाजे नष्ट झाल्यावर तुम्ही गेम जिंकता. याशिवाय, विजयाचा संदेश दाखवा.
1. **पुन्हा सुरू करा**. सर्व जीव संपल्यावर किंवा गेम जिंकल्यावर, गेम पुन्हा सुरू करण्याचा पर्याय द्या. लक्षात ठेवा! तुम्हाला गेम पुन्हा सुरू करावा लागेल आणि मागील गेमची स्थिती साफ करावी लागेल.

## शिफारस केलेली पावले

`your-work` उपफोल्डरमध्ये तयार केलेल्या फाइल्स शोधा. त्यामध्ये खालील गोष्टी असाव्यात:

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

तुमचा प्रकल्प `your_work` फोल्डरमध्ये सुरू करण्यासाठी खालील टाइप करा:

```bash
cd your-work
npm start
```

वरील आदेश `http://localhost:5000` या पत्त्यावर HTTP सर्व्हर सुरू करेल. ब्राउझर उघडा आणि हा पत्ता टाका. तुमचा गेम खेळण्यायोग्य स्थितीत असावा.

> टीप: Visual Studio Code मध्ये चेतावणी टाळण्यासाठी, `window.onload` फंक्शन संपादित करून `gameLoopId` फक्त कॉल करा (त्याआधी `let` न लावता), आणि फाइलच्या वर `let gameLoopId;` स्वतंत्रपणे जाहीर करा.

### कोड जोडा

1. **शेवटाची अट ट्रॅक करा**. शत्रूंची संख्या किंवा हिरो जहाज नष्ट झाले आहे का हे ट्रॅक करण्यासाठी खालील दोन फंक्शन्स जोडा:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **संदेश हँडलर्समध्ये लॉजिक जोडा**. `eventEmitter` संपादित करून या अटी हाताळा:

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

1. **नवीन संदेश प्रकार जोडा**. हे Messages constants ऑब्जेक्टमध्ये जोडा:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **पुन्हा सुरू करण्याचा कोड जोडा**. निवडलेल्या बटणावर दाबल्यावर गेम पुन्हा सुरू होईल.

   1. **`Enter` की प्रेस ऐका**. तुमच्या विंडोच्या eventListener मध्ये ही की प्रेस ऐकण्यासाठी संपादन करा:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **पुन्हा सुरू करण्याचा संदेश जोडा**. हा Message तुमच्या Messages constant मध्ये जोडा:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **गेम नियम लागू करा**. खालील गेम नियम लागू करा:

   1. **प्लेयर जिंकण्याची अट**. सर्व शत्रू जहाजे नष्ट झाल्यावर विजयाचा संदेश दाखवा.

      1. प्रथम, `displayMessage()` फंक्शन तयार करा:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. `endGame()` फंक्शन तयार करा:

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

   1. **पुन्हा सुरू करण्याचे लॉजिक**. सर्व जीव संपल्यावर किंवा खेळाडूने गेम जिंकल्यावर, गेम पुन्हा सुरू करता येईल हे दाखवा. याशिवाय, *पुन्हा सुरू करण्याची* की दाबल्यावर गेम पुन्हा सुरू करा (तुम्ही कोणती की वापरायची ते ठरवू शकता).

      1. `resetGame()` फंक्शन तयार करा:

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

     1. `initGame()` मध्ये `eventEmitter` कॉल जोडा जेणेकरून गेम रीसेट होईल:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. EventEmitter मध्ये `clear()` फंक्शन जोडा:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 अभिनंदन, कॅप्टन! तुमचा गेम पूर्ण झाला आहे! खूप छान काम केले! 🚀 💥 👽

---

## 🚀 आव्हान

आवाज जोडा! गेमप्ले सुधारण्यासाठी आवाज जोडू शकता का? जसे की लेझर हिट झाल्यावर, हिरो मरण पावल्यावर किंवा जिंकल्यावर? JavaScript वापरून आवाज कसा प्ले करायचा हे शिकण्यासाठी [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) पहा.

## व्याख्यानानंतरची प्रश्नमंजुषा

[व्याख्यानानंतरची प्रश्नमंजुषा](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/40)

## पुनरावलोकन आणि स्व-अभ्यास

तुमचे काम म्हणजे एक नवीन नमुना गेम तयार करणे, त्यामुळे तुम्ही कोणता गेम तयार करू शकता हे पाहण्यासाठी काही मनोरंजक गेम्स एक्सप्लोर करा.

## असाइनमेंट

[नमुना गेम तयार करा](assignment.md)

**अस्वीकरण**:  
हा दस्तऐवज AI भाषांतर सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून भाषांतरित करण्यात आला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी कृपया लक्षात ठेवा की स्वयंचलित भाषांतरे त्रुटी किंवा अचूकतेच्या अभावाने युक्त असू शकतात. मूळ भाषेतील दस्तऐवज हा अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी भाषांतराची शिफारस केली जाते. या भाषांतराचा वापर करून उद्भवलेल्या कोणत्याही गैरसमज किंवा चुकीच्या अर्थासाठी आम्ही जबाबदार नाही.