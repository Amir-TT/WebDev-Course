<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "01336cddd638242e99b133614111ea40",
  "translation_date": "2025-08-24T12:42:08+00:00",
  "source_file": "6-space-game/6-end-condition/README.md",
  "language_code": "pt"
}
-->
# Construir um Jogo Espacial Parte 6: Fim e Reinício

## Questionário Pré-Aula

[Questionário pré-aula](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/39)

Existem várias formas de expressar uma *condição de fim* num jogo. Cabe a ti, como criador do jogo, decidir por que motivo o jogo termina. Aqui estão algumas razões, assumindo que estamos a falar do jogo espacial que tens vindo a construir até agora:

- **`N` Naves inimigas foram destruídas**: É bastante comum, se dividires o jogo em diferentes níveis, que seja necessário destruir `N` naves inimigas para completar um nível.
- **A tua nave foi destruída**: Existem jogos em que perdes se a tua nave for destruída. Outra abordagem comum é ter o conceito de vidas. Sempre que a tua nave é destruída, perdes uma vida. Quando todas as vidas se esgotam, perdes o jogo.
- **Colecionaste `N` pontos**: Outra condição de fim comum é colecionar pontos. Como obténs pontos depende de ti, mas é habitual atribuir pontos a várias atividades, como destruir uma nave inimiga ou talvez colecionar itens que *caem* quando são destruídos.
- **Completaste um nível**: Isto pode envolver várias condições, como `X` naves inimigas destruídas, `Y` pontos colecionados ou talvez a recolha de um item específico.

## Reiniciar

Se as pessoas gostarem do teu jogo, é provável que queiram jogá-lo novamente. Assim que o jogo terminar, por qualquer motivo, deves oferecer uma opção para reiniciar.

✅ Pensa um pouco sobre as condições em que achas que um jogo termina e como és incentivado a reiniciá-lo.

## O que construir

Vais adicionar estas regras ao teu jogo:

1. **Vencer o jogo**. Assim que todas as naves inimigas forem destruídas, ganhas o jogo. Além disso, exibe uma mensagem de vitória.
1. **Reiniciar**. Quando todas as vidas forem perdidas ou o jogo for ganho, deves oferecer uma forma de reiniciar o jogo. Lembra-te! Precisarás de reinicializar o jogo e limpar o estado anterior.

## Passos recomendados

Localiza os ficheiros que foram criados para ti na subpasta `your-work`. Deve conter o seguinte:

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

Inicia o teu projeto na pasta `your_work` digitando:

```bash
cd your-work
npm start
```

O comando acima iniciará um servidor HTTP no endereço `http://localhost:5000`. Abre um navegador e insere esse endereço. O teu jogo deve estar num estado jogável.

> dica: para evitar avisos no Visual Studio Code, edita a função `window.onload` para chamar `gameLoopId` como está (sem `let`), e declara o gameLoopId no topo do ficheiro, independentemente: `let gameLoopId;`

### Adicionar código

1. **Acompanhar a condição de fim**. Adiciona código que acompanhe o número de inimigos ou se a nave do herói foi destruída, adicionando estas duas funções:

    ```javascript
    function isHeroDead() {
      return hero.life <= 0;
    }

    function isEnemiesDead() {
      const enemies = gameObjects.filter((go) => go.type === "Enemy" && !go.dead);
      return enemies.length === 0;
    }
    ```

1. **Adicionar lógica aos manipuladores de mensagens**. Edita o `eventEmitter` para lidar com estas condições:

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

1. **Adicionar novos tipos de mensagens**. Adiciona estas Mensagens ao objeto de constantes:

    ```javascript
    GAME_END_LOSS: "GAME_END_LOSS",
    GAME_END_WIN: "GAME_END_WIN",
    ```

2. **Adicionar código de reinício** que reinicie o jogo ao pressionar um botão selecionado.

   1. **Ouvir a tecla `Enter`**. Edita o eventListener da tua janela para ouvir esta tecla:

    ```javascript
     else if(evt.key === "Enter") {
        eventEmitter.emit(Messages.KEY_EVENT_ENTER);
      }
    ```

   1. **Adicionar mensagem de reinício**. Adiciona esta Mensagem às constantes de Mensagens:

        ```javascript
        KEY_EVENT_ENTER: "KEY_EVENT_ENTER",
        ```

1. **Implementar regras do jogo**. Implementa as seguintes regras do jogo:

   1. **Condição de vitória do jogador**. Quando todas as naves inimigas forem destruídas, exibe uma mensagem de vitória.

      1. Primeiro, cria uma função `displayMessage()`:

        ```javascript
        function displayMessage(message, color = "red") {
          ctx.font = "30px Arial";
          ctx.fillStyle = color;
          ctx.textAlign = "center";
          ctx.fillText(message, canvas.width / 2, canvas.height / 2);
        }
        ```

      1. Cria uma função `endGame()`:

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

   1. **Lógica de reinício**. Quando todas as vidas forem perdidas ou o jogador vencer o jogo, exibe que o jogo pode ser reiniciado. Além disso, reinicia o jogo quando a tecla de *reinício* for pressionada (podes decidir qual tecla será mapeada para reiniciar).

      1. Cria a função `resetGame()`:

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

     1. Adiciona uma chamada ao `eventEmitter` para reiniciar o jogo em `initGame()`:

        ```javascript
        eventEmitter.on(Messages.KEY_EVENT_ENTER, () => {
          resetGame();
        });
        ```

     1. Adiciona uma função `clear()` ao EventEmitter:

        ```javascript
        clear() {
          this.listeners = {};
        }
        ```

👽 💥 🚀 Parabéns, Capitão! O teu jogo está completo! Muito bem! 🚀 💥 👽

---

## 🚀 Desafio

Adiciona um som! Consegues adicionar um som para melhorar a experiência do jogo, talvez quando um laser acerta, ou quando o herói morre ou vence? Dá uma olhada neste [sandbox](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_audio_play) para aprenderes a tocar som usando JavaScript.

## Questionário Pós-Aula

[Questionário pós-aula](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/40)

## Revisão e Autoestudo

A tua tarefa é criar um novo jogo de exemplo, por isso explora alguns jogos interessantes por aí para veres que tipo de jogo podes construir.

## Tarefa

[Construir um Jogo de Exemplo](assignment.md)

**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos pela precisão, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original na sua língua nativa deve ser considerado a fonte autoritária. Para informações críticas, recomenda-se a tradução profissional realizada por humanos. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes do uso desta tradução.