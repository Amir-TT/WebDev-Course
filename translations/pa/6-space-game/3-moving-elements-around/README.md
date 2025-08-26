<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "23f088add24f0f1fa51014a9e27ea280",
  "translation_date": "2025-08-25T22:12:07+00:00",
  "source_file": "6-space-game/3-moving-elements-around/README.md",
  "language_code": "pa"
}
-->
# ਸਪੇਸ ਗੇਮ ਬਣਾਓ ਭਾਗ 3: ਮੋਸ਼ਨ ਸ਼ਾਮਲ ਕਰਨਾ

## ਪ੍ਰੀ-ਲੈਕਚਰ ਕਵਿਜ਼

[ਪ੍ਰੀ-ਲੈਕਚਰ ਕਵਿਜ਼](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/33)

ਗੇਮਾਂ ਤਦ ਤੱਕ ਮਜ਼ੇਦਾਰ ਨਹੀਂ ਹੁੰਦੀਆਂ ਜਦ ਤੱਕ ਸਕਰੀਨ 'ਤੇ ਐਲੀਅਨ ਦੌੜਦੇ ਨਹੀਂ। ਇਸ ਗੇਮ ਵਿੱਚ, ਅਸੀਂ ਦੋ ਕਿਸਮ ਦੇ ਮੋਸ਼ਨ ਵਰਤਾਂਗੇ:

- **ਕੀਬੋਰਡ/ਮਾਊਸ ਮੋਸ਼ਨ**: ਜਦ ਉਪਭੋਗਤਾ ਸਕਰੀਨ 'ਤੇ ਕਿਸੇ ਆਬਜੈਕਟ ਨੂੰ ਹਿਲਾਉਣ ਲਈ ਕੀਬੋਰਡ ਜਾਂ ਮਾਊਸ ਨਾਲ ਇੰਟਰੈਕਟ ਕਰਦਾ ਹੈ।
- **ਗੇਮ ਦੁਆਰਾ ਪ੍ਰੇਰਿਤ ਮੋਸ਼ਨ**: ਜਦ ਗੇਮ ਕਿਸੇ ਨਿਰਧਾਰਤ ਸਮੇਂ ਦੇ ਅੰਤਰਾਲ ਨਾਲ ਕਿਸੇ ਆਬਜੈਕਟ ਨੂੰ ਹਿਲਾਉਂਦਾ ਹੈ।

ਤਾਂ ਅਸੀਂ ਸਕਰੀਨ 'ਤੇ ਚੀਜ਼ਾਂ ਕਿਵੇਂ ਹਿਲਾਉਂਦੇ ਹਾਂ? ਇਹ ਸਾਰਾ ਕਾਰਟੀਸ਼ੀਅਨ ਕੋਆਰਡੀਨੇਟਸ ਬਾਰੇ ਹੈ: ਅਸੀਂ ਆਬਜੈਕਟ ਦੀ ਸਥਿਤੀ (x, y) ਬਦਲਦੇ ਹਾਂ ਅਤੇ ਫਿਰ ਸਕਰੀਨ ਨੂੰ ਦੁਬਾਰਾ ਡਰਾਅ ਕਰਦੇ ਹਾਂ।

ਆਮ ਤੌਰ 'ਤੇ, ਸਕਰੀਨ 'ਤੇ *ਮੋਸ਼ਨ* ਹਾਸਲ ਕਰਨ ਲਈ ਤੁਹਾਨੂੰ ਹੇਠਾਂ ਦਿੱਤੇ ਕਦਮਾਂ ਦੀ ਲੋੜ ਹੁੰਦੀ ਹੈ:

1. **ਨਵੀਂ ਸਥਿਤੀ ਸੈੱਟ ਕਰੋ** ਕਿਸੇ ਆਬਜੈਕਟ ਲਈ; ਇਹ ਲੋੜੀਂਦਾ ਹੈ ਤਾਂ ਜੋ ਆਬਜੈਕਟ ਨੂੰ ਹਿਲਦਾ ਹੋਇਆ ਮਹਿਸੂਸ ਕੀਤਾ ਜਾ ਸਕੇ।
2. **ਸਕਰੀਨ ਸਾਫ਼ ਕਰੋ**, ਡਰਾਅਜ਼ ਦੇ ਵਿਚਕਾਰ ਸਕਰੀਨ ਨੂੰ ਸਾਫ਼ ਕਰਨ ਦੀ ਲੋੜ ਹੁੰਦੀ ਹੈ। ਅਸੀਂ ਇਸਨੂੰ ਇੱਕ ਰੈਕਟੈਂਗਲ ਡਰਾਅ ਕਰਕੇ ਸਾਫ਼ ਕਰ ਸਕਦੇ ਹਾਂ ਜਿਸਨੂੰ ਅਸੀਂ ਬੈਕਗ੍ਰਾਊਂਡ ਰੰਗ ਨਾਲ ਭਰਦੇ ਹਾਂ।
3. **ਨਵੀਂ ਸਥਿਤੀ 'ਤੇ ਆਬਜੈਕਟ ਨੂੰ ਦੁਬਾਰਾ ਡਰਾਅ ਕਰੋ**। ਇਸ ਤਰ੍ਹਾਂ ਅਸੀਂ ਆਖਿਰਕਾਰ ਆਬਜੈਕਟ ਨੂੰ ਇੱਕ ਸਥਾਨ ਤੋਂ ਦੂਜੇ ਸਥਾਨ ਤੱਕ ਹਿਲਾਉਣ ਵਿੱਚ ਸਫਲ ਹੁੰਦੇ ਹਾਂ।

ਇਹ ਕੋਡ ਵਿੱਚ ਇਸ ਤਰ੍ਹਾਂ ਲੱਗ ਸਕਦਾ ਹੈ:

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

✅ ਕੀ ਤੁਸੀਂ ਸੋਚ ਸਕਦੇ ਹੋ ਕਿ ਕਿਉਂ ਆਪਣੇ ਹੀਰੋ ਨੂੰ ਹਰ ਸੈਕਿੰਡ ਕਈ ਫਰੇਮਾਂ 'ਤੇ ਦੁਬਾਰਾ ਡਰਾਅ ਕਰਨ ਨਾਲ ਪ੍ਰਦਰਸ਼ਨ ਦੀ ਲਾਗਤ ਵਧ ਸਕਦੀ ਹੈ? [ਇਸ ਪੈਟਰਨ ਦੇ ਵਿਕਲਪਾਂ](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Optimizing_canvas) ਬਾਰੇ ਪੜ੍ਹੋ।

## ਕੀਬੋਰਡ ਇਵੈਂਟਸ ਨੂੰ ਹੈਂਡਲ ਕਰੋ

ਤੁਸੀਂ ਇਵੈਂਟਸ ਨੂੰ ਕੋਡ ਨਾਲ ਖਾਸ ਤੌਰ 'ਤੇ ਜੋੜ ਕੇ ਹੈਂਡਲ ਕਰਦੇ ਹੋ। ਕੀਬੋਰਡ ਇਵੈਂਟਸ ਪੂਰੀ ਵਿੰਡੋ 'ਤੇ ਟ੍ਰਿਗਰ ਹੁੰਦੇ ਹਨ ਜਦਕਿ ਮਾਊਸ ਇਵੈਂਟਸ ਜਿਵੇਂ ਕਿ `ਕਲਿਕ` ਕਿਸੇ ਖਾਸ ਐਲੀਮੈਂਟ 'ਤੇ ਕਲਿਕ ਕਰਨ ਨਾਲ ਜੁੜ ਸਕਦੇ ਹਨ। ਅਸੀਂ ਇਸ ਪ੍ਰੋਜੈਕਟ ਦੌਰਾਨ ਕੀਬੋਰਡ ਇਵੈਂਟਸ ਦੀ ਵਰਤੋਂ ਕਰਾਂਗੇ।

ਇੱਕ ਇਵੈਂਟ ਨੂੰ ਹੈਂਡਲ ਕਰਨ ਲਈ ਤੁਹਾਨੂੰ ਵਿੰਡੋ ਦੇ `addEventListener()` ਮੈਥਡ ਦੀ ਵਰਤੋਂ ਕਰਨੀ ਪਵੇਗੀ ਅਤੇ ਇਸਨੂੰ ਦੋ ਇਨਪੁਟ ਪੈਰਾਮੀਟਰ ਦੇਣੇ ਪੈਣਗੇ। ਪਹਿਲਾ ਪੈਰਾਮੀਟਰ ਇਵੈਂਟ ਦਾ ਨਾਮ ਹੈ, ਉਦਾਹਰਣ ਲਈ `keyup`। ਦੂਜਾ ਪੈਰਾਮੀਟਰ ਉਹ ਫੰਕਸ਼ਨ ਹੈ ਜੋ ਇਵੈਂਟ ਹੋਣ ਦੇ ਨਤੀਜੇ ਵਜੋਂ ਚਲਾਇਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ।

ਇਹ ਰਿਹਾ ਇੱਕ ਉਦਾਹਰਣ:

```javascript
window.addEventListener('keyup', (evt) => {
  // `evt.key` = string representation of the key
  if (evt.key === 'ArrowUp') {
    // do something
  }
})
```

ਕੀ ਇਵੈਂਟਸ ਲਈ, ਇਵੈਂਟ 'ਤੇ ਦੋ ਪ੍ਰਾਪਰਟੀਜ਼ ਹਨ ਜੋ ਤੁਸੀਂ ਵੇਖਣ ਲਈ ਵਰਤ ਸਕਦੇ ਹੋ ਕਿ ਕਿਹੜੀ ਕੁੰਜੀ ਦਬਾਈ ਗਈ ਸੀ:

- `key`, ਇਹ ਦਬਾਈ ਗਈ ਕੁੰਜੀ ਦਾ ਸਟਰਿੰਗ ਪ੍ਰਦਰਸ਼ਨ ਹੈ, ਉਦਾਹਰਣ ਲਈ `ArrowUp`
- `keyCode`, ਇਹ ਇੱਕ ਨੰਬਰ ਪ੍ਰਦਰਸ਼ਨ ਹੈ, ਉਦਾਹਰਣ ਲਈ `37`, ਜੋ `ArrowLeft` ਦੇ ਅਨੁਕੂਲ ਹੈ।

✅ ਕੀ ਇਵੈਂਟ ਮੈਨਿਪੂਲੇਸ਼ਨ ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਤੋਂ ਬਾਹਰ ਵੀ ਲਾਭਦਾਇਕ ਹੈ। ਇਸ ਤਕਨੀਕ ਲਈ ਤੁਸੀਂ ਹੋਰ ਕੀ ਉਪਯੋਗ ਸੋਚ ਸਕਦੇ ਹੋ?

### ਖਾਸ ਕੁੰਜੀਆਂ: ਇੱਕ ਚੇਤਾਵਨੀ

ਕੁਝ *ਖਾਸ* ਕੁੰਜੀਆਂ ਹਨ ਜੋ ਵਿੰਡੋ ਨੂੰ ਪ੍ਰਭਾਵਿਤ ਕਰਦੀਆਂ ਹਨ। ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਜੇ ਤੁਸੀਂ ਇੱਕ `keyup` ਇਵੈਂਟ ਸੁਣ ਰਹੇ ਹੋ ਅਤੇ ਤੁਸੀਂ ਆਪਣੇ ਹੀਰੋ ਨੂੰ ਹਿਲਾਉਣ ਲਈ ਇਹ ਖਾਸ ਕੁੰਜੀਆਂ ਵਰਤਦੇ ਹੋ ਤਾਂ ਇਹ ਹੋਰਿਜ਼ਾਂਟਲ ਸਕ੍ਰੋਲਿੰਗ ਵੀ ਕਰੇਗਾ। ਇਸ ਕਾਰਨ, ਜਦ ਤੁਸੀਂ ਆਪਣੀ ਗੇਮ ਬਣਾਉਂਦੇ ਹੋ ਤਾਂ ਤੁਸੀਂ ਇਸ ਬਿਲਟ-ਇਨ ਬ੍ਰਾਊਜ਼ਰ ਵਿਹਾਰ ਨੂੰ *ਬੰਦ* ਕਰਨਾ ਚਾਹੋਗੇ। ਤੁਹਾਨੂੰ ਇਸ ਤਰ੍ਹਾਂ ਦਾ ਕੋਡ ਲੋੜੀਂਦਾ ਹੈ:

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

ਉਪਰੋਕਤ ਕੋਡ ਇਹ ਯਕੀਨੀ ਬਣਾਏਗਾ ਕਿ ਐਰੋ-ਕੀਜ਼ ਅਤੇ ਸਪੇਸ ਕੀ ਦੀਆਂ *ਡਿਫਾਲਟ* ਵਿਹਾਰ ਬੰਦ ਹੋ ਜਾਣ। *ਬੰਦ ਕਰਨ* ਦਾ ਮਕੈਨਿਜ਼ਮ `e.preventDefault()` ਕਾਲ ਕਰਨ ਨਾਲ ਹੁੰਦਾ ਹੈ।

## ਗੇਮ ਦੁਆਰਾ ਪ੍ਰੇਰਿਤ ਮੋਸ਼ਨ

ਅਸੀਂ ਚੀਜ਼ਾਂ ਨੂੰ ਆਪਣੇ ਆਪ ਹਿਲਾ ਸਕਦੇ ਹਾਂ ਜਦ ਅਸੀਂ ਟਾਈਮਰ ਵਰਤਦੇ ਹਾਂ ਜਿਵੇਂ ਕਿ `setTimeout()` ਜਾਂ `setInterval()` ਫੰਕਸ਼ਨ ਜੋ ਹਰ ਟਿਕ ਜਾਂ ਸਮੇਂ ਦੇ ਅੰਤਰਾਲ 'ਤੇ ਆਬਜੈਕਟ ਦੀ ਸਥਿਤੀ ਨੂੰ ਅਪਡੇਟ ਕਰਦੇ ਹਨ। ਇਹ ਇਸ ਤਰ੍ਹਾਂ ਲੱਗ ਸਕਦਾ ਹੈ:

```javascript
let id = setInterval(() => {
  //move the enemy on the y axis
  enemy.y += 10;
})
```

## ਗੇਮ ਲੂਪ

ਗੇਮ ਲੂਪ ਇੱਕ ਸੰਕਲਪ ਹੈ ਜੋ ਅਸਲ ਵਿੱਚ ਇੱਕ ਫੰਕਸ਼ਨ ਹੈ ਜੋ ਨਿਯਮਿਤ ਅੰਤਰਾਲ 'ਤੇ ਚਲਾਇਆ ਜਾਂਦਾ ਹੈ। ਇਸਨੂੰ ਗੇਮ ਲੂਪ ਕਿਹਾ ਜਾਂਦਾ ਹੈ ਕਿਉਂਕਿ ਜੋ ਕੁਝ ਵੀ ਉਪਭੋਗਤਾ ਨੂੰ ਦਿਖਾਈ ਦੇਣਾ ਚਾਹੀਦਾ ਹੈ ਉਹ ਲੂਪ ਵਿੱਚ ਡਰਾਅ ਕੀਤਾ ਜਾਂਦਾ ਹੈ। ਗੇਮ ਲੂਪ ਗੇਮ ਦੇ ਸਾਰੇ ਆਬਜੈਕਟਸ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ ਜੋ ਗੇਮ ਦਾ ਹਿੱਸਾ ਹੁੰਦੇ ਹਨ, ਸਾਰੇ ਨੂੰ ਡਰਾਅ ਕਰਦਾ ਹੈ ਜਦ ਤੱਕ ਕਿ ਕਿਸੇ ਕਾਰਨ ਕਰਕੇ ਉਹ ਹੁਣ ਗੇਮ ਦਾ ਹਿੱਸਾ ਨਹੀਂ ਰਹਿੰਦੇ। ਉਦਾਹਰਣ ਲਈ, ਜੇਕਰ ਕੋਈ ਆਬਜੈਕਟ ਇੱਕ ਦੁਸ਼ਮਣ ਹੈ ਜਿਸਨੂੰ ਲੇਜ਼ਰ ਨਾਲ ਮਾਰਿਆ ਗਿਆ ਅਤੇ ਉਹ ਫਟ ਜਾਂਦਾ ਹੈ, ਤਾਂ ਇਹ ਹੁਣ ਮੌਜੂਦਾ ਗੇਮ ਲੂਪ ਦਾ ਹਿੱਸਾ ਨਹੀਂ ਹੁੰਦਾ (ਤੁਸੀਂ ਇਸ ਬਾਰੇ ਹੋਰ ਅਗਲੇ ਪਾਠਾਂ ਵਿੱਚ ਸਿੱਖੋਗੇ)।

ਇਹ ਰਿਹਾ ਇੱਕ ਗੇਮ ਲੂਪ ਆਮ ਤੌਰ 'ਤੇ ਕਿਵੇਂ ਲੱਗ ਸਕਦਾ ਹੈ, ਕੋਡ ਵਿੱਚ ਪ੍ਰਗਟ ਕੀਤਾ:

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

ਉਪਰੋਕਤ ਲੂਪ ਹਰ `200` ਮਿਲੀਸੈਕਿੰਡ ਵਿੱਚ ਕੈਨਵਸ ਨੂੰ ਦੁਬਾਰਾ ਡਰਾਅ ਕਰਨ ਲਈ ਚਲਾਇਆ ਜਾਂਦਾ ਹੈ। ਤੁਹਾਡੇ ਕੋਲ ਆਪਣੇ ਗੇਮ ਲਈ ਸਭ ਤੋਂ ਵਧੀਆ ਅੰਤਰਾਲ ਚੁਣਨ ਦੀ ਯੋਗਤਾ ਹੈ।

## ਸਪੇਸ ਗੇਮ ਜਾਰੀ ਰੱਖਣਾ

ਤੁਸੀਂ ਮੌਜੂਦਾ ਕੋਡ ਲੈ ਕੇ ਇਸਨੂੰ ਵਧਾਓਗੇ। ਜਾਂ ਤਾਂ ਉਸ ਕੋਡ ਨਾਲ ਸ਼ੁਰੂ ਕਰੋ ਜੋ ਤੁਸੀਂ ਭਾਗ I ਦੌਰਾਨ ਪੂਰਾ ਕੀਤਾ ਸੀ ਜਾਂ [ਭਾਗ II- ਸ਼ੁਰੂਆਤੀ](../../../../6-space-game/3-moving-elements-around/your-work) ਵਿੱਚ ਦਿੱਤੇ ਕੋਡ ਦੀ ਵਰਤੋਂ ਕਰੋ।

- **ਹੀਰੋ ਨੂੰ ਹਿਲਾਉਣਾ**: ਤੁਸੀਂ ਕੋਡ ਸ਼ਾਮਲ ਕਰੋਗੇ ਤਾਂ ਜੋ ਤੁਸੀਂ ਐਰੋ ਕੀਜ਼ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਹੀਰੋ ਨੂੰ ਹਿਲਾ ਸਕੋ।
- **ਦੁਸ਼ਮਣਾਂ ਨੂੰ ਹਿਲਾਉਣਾ**: ਤੁਸੀਂ ਇਹ ਵੀ ਯਕੀਨੀ ਬਣਾਉਣ ਲਈ ਕੋਡ ਸ਼ਾਮਲ ਕਰਨਾ ਹੋਵੇਗਾ ਕਿ ਦੁਸ਼ਮਣ ਇੱਕ ਨਿਰਧਾਰਤ ਦਰ 'ਤੇ ਉੱਪਰ ਤੋਂ ਹੇਠਾਂ ਹਿਲਦੇ ਹਨ।

## ਸਿਫਾਰਸ਼ੀ ਕਦਮ

`your-work` ਸਬ ਫੋਲਡਰ ਵਿੱਚ ਬਣਾਈਆਂ ਗਈਆਂ ਫਾਈਲਾਂ ਨੂੰ ਲੱਭੋ। ਇਸ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤੇ ਹੋਣੇ ਚਾਹੀਦੇ ਹਨ:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

ਤੁਸੀਂ ਆਪਣਾ ਪ੍ਰੋਜੈਕਟ `your_work` ਫੋਲਡਰ ਵਿੱਚ ਇਸ ਤਰ੍ਹਾਂ ਸ਼ੁਰੂ ਕਰੋ:

```bash
cd your-work
npm start
```

ਉਪਰੋਕਤ HTTP ਸਰਵਰ ਪਤਾ `http://localhost:5000` 'ਤੇ ਸ਼ੁਰੂ ਕਰੇਗਾ। ਇੱਕ ਬ੍ਰਾਊਜ਼ਰ ਖੋਲ੍ਹੋ ਅਤੇ ਉਹ ਪਤਾ ਦਰਜ ਕਰੋ, ਇਸ ਸਮੇਂ ਇਹ ਹੀਰੋ ਅਤੇ ਸਾਰੇ ਦੁਸ਼ਮਣਾਂ ਨੂੰ ਰੈਂਡਰ ਕਰਨਾ ਚਾਹੀਦਾ ਹੈ; ਕੁਝ ਵੀ ਹਿਲ ਨਹੀਂ ਰਿਹਾ - ਅਜੇ ਤੱਕ!

### ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ

1. **ਹੀਰੋ**, **ਦੁਸ਼ਮਣ**, ਅਤੇ **ਗੇਮ ਆਬਜੈਕਟ** ਲਈ ਸਮਰਪਿਤ ਆਬਜੈਕਟਸ ਸ਼ਾਮਲ ਕਰੋ, ਇਹਨਾਂ ਵਿੱਚ `x` ਅਤੇ `y` ਪ੍ਰਾਪਰਟੀਜ਼ ਹੋਣੀਆਂ ਚਾਹੀਦੀਆਂ ਹਨ। (ਯਾਦ ਕਰੋ [ਵਿਰਾਸਤ ਜਾਂ ਰਚਨਾ](../README.md) ਬਾਰੇ ਭਾਗ)।

   *ਸੁਝਾਅ*: ਇੱਕ ਨਵੀਂ GameObject ਕਲਾਸ ਸ਼ੁਰੂ ਕਰੋ ਜਿਸਦਾ ਕੰਸਟ੍ਰਕਟਰ ਹੇਠਾਂ ਦਿੱਤੇ ਤਰੀਕੇ ਨਾਲ ਬਣਾਇਆ ਗਿਆ ਹੋਵੇ, ਅਤੇ ਫਿਰ ਇਸਨੂੰ ਕੈਨਵਸ 'ਤੇ ਡਰਾਅ ਕਰੋ:

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

    ਹੁਣ, ਇਸ GameObject ਨੂੰ ਵਧਾ ਕੇ ਹੀਰੋ ਅਤੇ ਦੁਸ਼ਮਣ ਬਣਾਓ।

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

2. **ਕੀ-ਇਵੈਂਟ ਹੈਂਡਲਰ ਸ਼ਾਮਲ ਕਰੋ** ਤਾਂ ਜੋ ਕੀ ਨੈਵੀਗੇਸ਼ਨ (ਹੀਰੋ ਨੂੰ ਉੱਪਰ/ਹੇਠਾਂ, ਖੱਬੇ/ਸੱਜੇ ਹਿਲਾਉਣਾ) ਸੰਭਾਲਿਆ ਜਾ ਸਕੇ।

   *ਯਾਦ ਰੱਖੋ*: ਇਹ ਕਾਰਟੀਸ਼ੀਅਨ ਸਿਸਟਮ ਹੈ, ਟੌਪ-ਲੇਫਟ `0,0` ਹੈ। ਡਿਫਾਲਟ ਵਿਹਾਰ ਨੂੰ ਰੋਕਣ ਲਈ ਕੋਡ ਸ਼ਾਮਲ ਕਰਨਾ ਵੀ ਯਾਦ ਰੱਖੋ।

   *ਸੁਝਾਅ*: ਆਪਣਾ onKeyDown ਫੰਕਸ਼ਨ ਬਣਾਓ ਅਤੇ ਇਸਨੂੰ ਵਿੰਡੋ ਨਾਲ ਜੋੜੋ:

   ```javascript
    let onKeyDown = function (e) {
	      console.log(e.keyCode);
	        ...add the code from the lesson above to stop default behavior
	      }
    };

    window.addEventListener("keydown", onKeyDown);
   ```

   ਇਸ ਪੜਾਅ 'ਤੇ ਆਪਣੇ ਬ੍ਰਾਊਜ਼ਰ ਕਨਸੋਲ ਦੀ ਜਾਂਚ ਕਰੋ, ਅਤੇ ਕੀਸਟ੍ਰੋਕਸ ਨੂੰ ਲੌਗ ਹੋਦੇ ਵੇਖੋ।

3. **ਪਬ-ਸਬ ਪੈਟਰਨ ਲਾਗੂ ਕਰੋ** (Pub sub pattern), ਇਹ ਤੁਹਾਡੇ ਕੋਡ ਨੂੰ ਸਾਫ਼ ਰੱਖੇਗਾ ਜਦ ਤੁਸੀਂ ਬਾਕੀ ਭਾਗਾਂ ਦੀ ਪਾਲਣਾ ਕਰੋਗੇ।

   ਇਸ ਆਖਰੀ ਭਾਗ ਨੂੰ ਕਰਨ ਲਈ, ਤੁਸੀਂ ਇਹ ਕਰ ਸਕਦੇ ਹੋ:

   1. **ਵਿੰਡੋ 'ਤੇ ਇੱਕ ਇਵੈਂਟ ਲਿਸਨਰ ਸ਼ਾਮਲ ਕਰੋ**:

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

    1. **ਇੱਕ EventEmitter ਕਲਾਸ ਬਣਾਓ** ਜੋ ਸੁਨੇਹੇ ਪ੍ਰਕਾਸ਼ਿਤ ਅਤੇ ਸਬਸਕ੍ਰਾਈਬ ਕਰ ਸਕੇ:

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

    1. **ਕਾਂਸਟੈਂਟਸ ਸ਼ਾਮਲ ਕਰੋ** ਅਤੇ EventEmitter ਸੈਟ ਕਰੋ:

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

    1. **ਗੇਮ ਸ਼ੁਰੂ ਕਰੋ**

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

1. **ਗੇਮ ਲੂਪ ਸੈਟ ਕਰੋ**

   ਵਿੰਡੋ.onload ਫੰਕਸ਼ਨ ਨੂੰ ਰੀਫੈਕਟਰ ਕਰੋ ਤਾਂ ਜੋ ਗੇਮ ਸ਼ੁਰੂ ਕੀਤੀ ਜਾ ਸਕੇ ਅਤੇ ਇੱਕ ਵਧੀਆ ਅੰਤਰਾਲ 'ਤੇ ਗੇਮ ਲੂਪ ਸੈਟ ਕੀਤਾ ਜਾ ਸਕੇ। ਤੁਸੀਂ ਇੱਕ ਲੇਜ਼ਰ ਬੀਮ ਵੀ ਸ਼ਾਮਲ ਕਰੋਗੇ:

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

5. **ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ** ਤਾਂ ਜੋ ਦੁਸ਼ਮਣ ਇੱਕ ਨਿਰਧਾਰਤ ਅੰਤਰਾਲ 'ਤੇ ਹਿਲ ਸਕਣ।

    `createEnemies()` ਫੰਕਸ਼ਨ ਨੂੰ ਰੀਫੈਕਟਰ ਕਰੋ ਤਾਂ ਜੋ ਦੁਸ਼ਮਣ ਬਣਾਏ ਜਾ ਸਕਣ ਅਤੇ ਨਵੇਂ gameObjects ਕਲਾਸ ਵਿੱਚ ਪੁਸ਼ ਕੀਤੇ ਜਾ ਸਕਣ:

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
    
    ਅਤੇ ਇੱਕ `createHero()` ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰੋ ਜੋ ਹੀਰੋ ਲਈ ਇਸੇ ਪ੍ਰਕਿਰਿਆ ਨੂੰ ਪੂਰਾ ਕਰੇ।

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

    ਅਤੇ ਆਖਿਰ ਵਿੱਚ, ਇੱਕ `drawGameObjects()` ਫੰਕਸ਼ਨ ਸ਼ਾਮਲ ਕਰੋ ਤਾਂ ਜੋ ਡਰਾਇੰਗ ਸ਼ੁਰੂ ਕੀਤੀ ਜਾ ਸਕੇ:

    ```javascript
    function drawGameObjects(ctx) {
      gameObjects.forEach(go => go.draw(ctx));
    }
    ```

    ਤੁਹਾਡੇ ਦੁਸ਼ਮਣ ਤੁਹਾਡੇ ਹੀਰੋ ਸਪੇਸਸ਼ਿਪ 'ਤੇ ਅਗੇ ਵਧਣੇ ਸ਼ੁਰੂ ਹੋ ਜਾਣੇ ਚਾਹੀਦੇ ਹਨ!

---

## 🚀 ਚੁਣੌਤੀ

ਜਿਵੇਂ ਤੁਸੀਂ ਵੇਖ ਸਕਦੇ ਹੋ, ਜਦ ਤੁਸੀਂ ਫੰਕਸ਼ਨ, ਵੈਰੀਏਬਲ ਅਤੇ ਕਲਾਸਾਂ ਸ਼ਾਮਲ ਕਰਦੇ ਹੋ, ਤੁਹਾਡਾ ਕੋਡ 'ਸਪੈਗੇਟੀ ਕੋਡ' ਵਿੱਚ ਬਦਲ ਸਕਦਾ ਹੈ। ਤੁਸੀਂ ਆਪਣੇ ਕੋਡ ਨੂੰ ਹੋਰ ਪੜ੍ਹਨਯੋਗ ਬਣਾਉਣ ਲਈ ਇਸਨੂੰ ਕਿਵੇਂ ਵਧੀਆ ਢੰਗ ਨਾਲ ਸੰਗਠਿਤ ਕਰ ਸਕਦੇ ਹੋ? ਇੱਕ ਸਿਸਟਮ ਦਾ ਖਾਕਾ ਬਣਾਓ ਜੋ ਤੁਹਾਡੇ ਕੋਡ ਨੂੰ ਸੰਗਠਿਤ ਕਰੇ, ਭਾਵੇਂ ਇਹ ਅਜੇ ਵੀ ਇੱਕ ਫਾਈਲ ਵਿੱਚ ਹੋਵੇ।

## ਪੋਸਟ-ਲੈਕਚਰ ਕਵਿਜ਼

[ਪੋਸਟ-ਲੈਕਚਰ ਕਵਿਜ਼](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/34)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ ਅਧਿਐਨ

ਜਦਕਿ ਅਸੀਂ ਆਪਣੀ ਗੇਮ ਬਿਨਾਂ ਫਰੇਮਵਰਕ ਦੀ ਵਰਤੋਂ ਕੀਤੇ ਲਿਖ ਰਹੇ ਹਾਂ, ਜਾਵਾਸਕ੍ਰਿਪਟ-ਅਧਾਰਿਤ ਕੈਨਵਸ ਫਰੇਮਵਰਕ ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਲਈ ਬਹੁਤ ਹਨ। [ਇਨ੍ਹਾਂ ਬਾਰੇ ਪੜ੍ਹਨ](https://github.com/collections/javascript-game-engines) ਲਈ ਕੁਝ ਸਮਾਂ ਲਓ।

## ਅਸਾਈਨਮੈਂਟ

[ਆਪਣੇ ਕੋਡ 'ਤੇ ਟਿੱਪਣੀ ਕਰੋ](assignment.md)

**ਅਸਵੀਕਾਰਨ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਨਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼, ਜੋ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਹੈ, ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।