<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "01336cddd638242e99b133614111ea40",
  "translation_date": "2025-08-25T22:33:52+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "ru"
}
-->
# Создание космической игры. Часть 6: Завершение и перезапуск

## Викторина перед лекцией

[Викторина перед лекцией](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/39)

Существует множество способов задать *условие завершения* игры. Как создатель игры, вы сами решаете, почему игра должна закончиться. Вот несколько возможных причин, если мы говорим о космической игре, которую вы разрабатывали до сих пор:

- **Уничтожено `N` вражеских кораблей**: Это довольно распространенный вариант, если вы делите игру на уровни, где для завершения уровня нужно уничтожить `N` вражеских кораблей.
- **Ваш корабль уничтожен**: Есть игры, где вы проигрываете, если ваш корабль уничтожен. Другой распространенный подход — это концепция жизней. Каждый раз, когда ваш корабль уничтожается, вы теряете одну жизнь. Когда все жизни исчерпаны, игра заканчивается.
- **Вы набрали `N` очков**: Еще одно популярное условие завершения — это набор определенного количества очков. Как именно вы их зарабатываете, зависит от вас, но обычно очки начисляются за различные действия, например, за уничтожение вражеского корабля или сбор предметов, которые выпадают при уничтожении.
- **Завершение уровня**: Это может включать несколько условий, таких как уничтожение `X` вражеских кораблей, сбор `Y` очков или, возможно, нахождение определенного предмета.

## Перезапуск

Если ваша игра понравится игрокам, они, скорее всего, захотят сыграть снова. Когда игра заканчивается, по любой причине, вы должны предложить возможность перезапуска.

✅ Подумайте, при каких условиях игра заканчивается, и как вам предлагают ее перезапустить.

## Что нужно сделать

Вы добавите в игру следующие правила:

1. **Победа в игре**. Когда все вражеские корабли уничтожены, вы выигрываете. Также отобразите сообщение о победе.
1. **Перезапуск**. Когда все жизни потеряны или игра выиграна, предложите возможность перезапуска. Помните! Вам нужно будет заново инициализировать игру, очистив предыдущее состояние.

## Рекомендуемые шаги

Найдите файлы, которые были созданы для вас в папке `your-work`. Она должна содержать следующее:

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

Запустите ваш проект из папки `your_work`, введя:

```bash
cd your-work
npm start
```

Это запустит HTTP-сервер по адресу `http://localhost:5000`. Откройте браузер и введите этот адрес. Ваша игра должна быть в рабочем состоянии.

> совет: чтобы избежать предупреждений в Visual Studio Code, измените функцию `window.onload`, чтобы вызывать `gameLoopId` как есть (без `let`), и объявите `gameLoopId` в начале файла отдельно: `let gameLoopId;`

### Добавление кода

1. **Отслеживание условий завершения**. Добавьте код, который отслеживает количество врагов или уничтожение корабля героя, добавив эти две функции:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Добавьте логику в обработчики сообщений**. Измените `eventEmitter`, чтобы обрабатывать эти условия:

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

1. **Добавьте новые типы сообщений**. Добавьте эти сообщения в объект constants:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Добавьте код перезапуска**. Реализуйте перезапуск игры при нажатии выбранной кнопки.

   1. **Слушайте нажатие клавиши `Enter`**. Измените обработчик событий окна, чтобы слушать это нажатие:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Добавьте сообщение о перезапуске**. Добавьте это сообщение в объект Messages:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Реализуйте игровые правила**. Реализуйте следующие правила:

   1. **Условие победы игрока**. Когда все вражеские корабли уничтожены, отобразите сообщение о победе.

      1. Сначала создайте функцию `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Создайте функцию `endGame()`:

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

   1. **Логика перезапуска**. Когда все жизни потеряны или игрок выиграл, отобразите сообщение о возможности перезапуска. Также перезапустите игру при нажатии клавиши перезапуска (вы можете выбрать, какая клавиша будет использоваться).

      1. Создайте функцию `resetGame()`:

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

     1. Добавьте вызов `eventEmitter` для сброса игры в `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Добавьте функцию `clear()` в EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 Поздравляем, Капитан! Ваша игра завершена! Отличная работа! 🚀 💥 👽

---

## 🚀 Задание

Добавьте звук! Можете ли вы добавить звук, чтобы улучшить игровой процесс? Например, при попадании лазера, гибели героя или победе. Ознакомьтесь с этим [примером](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play), чтобы узнать, как воспроизводить звук с помощью JavaScript.

## Викторина после лекции

[Викторина после лекции](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/40)

## Обзор и самостоятельное изучение

Ваше задание — создать новую пробную игру, поэтому изучите интересные игры, чтобы понять, какую игру вы могли бы разработать.

## Задание

[Создайте пробную игру](assignment.md)

**Отказ от ответственности**:  
Этот документ был переведен с использованием сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Несмотря на наши усилия обеспечить точность, автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникающие в результате использования данного перевода.