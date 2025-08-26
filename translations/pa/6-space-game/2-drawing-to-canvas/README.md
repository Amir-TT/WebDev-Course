<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "41be8d35e7f30aa9dad10773c35e89c4",
  "translation_date": "2025-08-25T22:18:11+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "pa"
}
-->
# ਸਪੇਸ ਗੇਮ ਬਣਾਓ ਭਾਗ 2: ਹੀਰੋ ਅਤੇ ਮਾਨਸਟਰਜ਼ ਨੂੰ ਕੈਨਵਸ 'ਤੇ ਡਰਾਅ ਕਰੋ

## ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵਿਜ਼

[ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵਿਜ਼](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/31)

## ਕੈਨਵਸ

ਕੈਨਵਸ ਇੱਕ HTML ਤੱਤ ਹੈ ਜਿਸਦਾ ਮੂਲ ਰੂਪ ਵਿੱਚ ਕੋਈ ਸਮੱਗਰੀ ਨਹੀਂ ਹੁੰਦੀ; ਇਹ ਇੱਕ ਖਾਲੀ ਸਲੇਟ ਹੈ। ਤੁਹਾਨੂੰ ਇਸ 'ਤੇ ਡਰਾਇੰਗ ਕਰਕੇ ਇਸ ਵਿੱਚ ਕੁਝ ਸ਼ਾਮਲ ਕਰਨਾ ਪਵੇਗਾ।

✅ [ਕੈਨਵਸ API ਬਾਰੇ ਹੋਰ ਪੜ੍ਹੋ](https://developer.mozilla.org/docs/Web/API/Canvas_API) MDN 'ਤੇ।

ਇਹ ਆਮ ਤੌਰ 'ਤੇ ਪੰਨੇ ਦੇ ਬਾਡੀ ਦੇ ਹਿੱਸੇ ਵਜੋਂ ਇਸ ਤਰ੍ਹਾਂ ਘੋਸ਼ਿਤ ਕੀਤਾ ਜਾਂਦਾ ਹੈ:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

ਉਪਰੋਕਤ ਵਿੱਚ ਅਸੀਂ `id`, `width` ਅਤੇ `height` ਸੈਟ ਕਰ ਰਹੇ ਹਾਂ।

- `id`: ਇਸ ਨੂੰ ਸੈਟ ਕਰੋ ਤਾਂ ਜੋ ਜਦੋਂ ਤੁਹਾਨੂੰ ਇਸ ਨਾਲ ਇੰਟਰੈਕਟ ਕਰਨ ਦੀ ਲੋੜ ਹੋਵੇ ਤਾਂ ਤੁਸੀਂ ਇਸ ਦਾ ਹਵਾਲਾ ਪ੍ਰਾਪਤ ਕਰ ਸਕੋ।
- `width`: ਇਹ ਤੱਤ ਦੀ ਚੌੜਾਈ ਹੈ।
- `height`: ਇਹ ਤੱਤ ਦੀ ਉਚਾਈ ਹੈ।

## ਸਧਾਰਨ ਜਾਮਿਤੀ ਆਕਾਰ ਡਰਾਅ ਕਰਨਾ

ਕੈਨਵਸ ਚੀਜ਼ਾਂ ਡਰਾਅ ਕਰਨ ਲਈ ਕਾਰਟੀਸ਼ੀਅਨ ਕੋਆਰਡੀਨੇਟ ਸਿਸਟਮ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ। ਇਸ ਲਈ ਇਹ ਕਿਸੇ ਚੀਜ਼ ਦੇ ਸਥਾਨ ਨੂੰ ਦਰਸਾਉਣ ਲਈ x-ਅਕਸ ਅਤੇ y-ਅਕਸ ਦੀ ਵਰਤੋਂ ਕਰਦਾ ਹੈ। ਸਥਾਨ `0,0` ਸਿਖਰ ਦੇ ਖੱਬੇ ਪਾਸੇ ਹੈ ਅਤੇ ਹੇਠਾਂ ਸੱਜਾ ਉਹ ਹੈ ਜੋ ਤੁਸੀਂ ਕੈਨਵਸ ਦੀ ਚੌੜਾਈ ਅਤੇ ਉਚਾਈ ਸੈਟ ਕੀਤੀ ਹੈ।

![ਕੈਨਵਸ ਦਾ ਗ੍ਰਿਡ](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.pa.png)  
> ਚਿੱਤਰ [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes) ਤੋਂ

ਕੈਨਵਸ ਤੱਤ 'ਤੇ ਡਰਾਅ ਕਰਨ ਲਈ ਤੁਹਾਨੂੰ ਹੇਠਾਂ ਦਿੱਤੇ ਕਦਮਾਂ ਦੀ ਪਾਲਣਾ ਕਰਨੀ ਪਵੇਗੀ:

1. **ਕੈਨਵਸ ਤੱਤ ਦਾ ਹਵਾਲਾ ਪ੍ਰਾਪਤ ਕਰੋ।**  
1. **ਕੈਨਵਸ ਤੱਤ 'ਤੇ ਮੌਜੂਦ ਕੌਂਟੈਕਸਟ ਤੱਤ ਦਾ ਹਵਾਲਾ ਪ੍ਰਾਪਤ ਕਰੋ।**  
1. **ਕੌਂਟੈਕਸਟ ਤੱਤ ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਡਰਾਇੰਗ ਆਪਰੇਸ਼ਨ ਕਰੋ।**

ਉਪਰੋਕਤ ਕਦਮਾਂ ਲਈ ਕੋਡ ਆਮ ਤੌਰ 'ਤੇ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦਾ ਹੈ:

```javascript
// draws a red rectangle
//1. get the canvas reference
canvas = document.getElementById("myCanvas");

//2. set the context to 2D to draw basic shapes
ctx = canvas.getContext("2d");

//3. fill it with the color red
ctx.fillStyle = 'red';

//4. and draw a rectangle with these parameters, setting location and size
ctx.fillRect(0,0, 200, 200) // x,y,width, height
```

✅ ਕੈਨਵਸ API ਮੁੱਖ ਤੌਰ 'ਤੇ 2D ਆਕਾਰਾਂ 'ਤੇ ਧਿਆਨ ਕੇਂਦਰਿਤ ਕਰਦਾ ਹੈ, ਪਰ ਤੁਸੀਂ ਵੈੱਬਸਾਈਟ 'ਤੇ 3D ਤੱਤ ਵੀ ਡਰਾਅ ਕਰ ਸਕਦੇ ਹੋ; ਇਸ ਲਈ ਤੁਸੀਂ [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) ਦੀ ਵਰਤੋਂ ਕਰ ਸਕਦੇ ਹੋ।

ਤੁਸੀਂ ਕੈਨਵਸ API ਨਾਲ ਕਈ ਤਰ੍ਹਾਂ ਦੀਆਂ ਚੀਜ਼ਾਂ ਡਰਾਅ ਕਰ ਸਕਦੇ ਹੋ ਜਿਵੇਂ:

- **ਜਾਮਿਤੀ ਆਕਾਰ**, ਅਸੀਂ ਪਹਿਲਾਂ ਹੀ ਦਿਖਾਇਆ ਹੈ ਕਿ ਕਿਵੇਂ ਇੱਕ ਆਯਤਕਾਰ ਡਰਾਅ ਕਰਨਾ ਹੈ, ਪਰ ਤੁਸੀਂ ਹੋਰ ਬਹੁਤ ਕੁਝ ਡਰਾਅ ਕਰ ਸਕਦੇ ਹੋ।  
- **ਪਾਠ**, ਤੁਸੀਂ ਕਿਸੇ ਵੀ ਫੌਂਟ ਅਤੇ ਰੰਗ ਨਾਲ ਪਾਠ ਡਰਾਅ ਕਰ ਸਕਦੇ ਹੋ।  
- **ਚਿੱਤਰ**, ਤੁਸੀਂ ਇੱਕ ਚਿੱਤਰ ਜਿਵੇਂ ਕਿ .jpg ਜਾਂ .png ਆਦਿ ਦੇ ਆਧਾਰ 'ਤੇ ਡਰਾਅ ਕਰ ਸਕਦੇ ਹੋ।  

✅ ਇਸਨੂੰ ਅਜ਼ਮਾਓ! ਤੁਸੀਂ ਜਾਣਦੇ ਹੋ ਕਿ ਕਿਵੇਂ ਇੱਕ ਆਯਤਕਾਰ ਡਰਾਅ ਕਰਨਾ ਹੈ, ਕੀ ਤੁਸੀਂ ਇੱਕ ਗੋਲਾ ਪੰਨੇ 'ਤੇ ਡਰਾਅ ਕਰ ਸਕਦੇ ਹੋ? CodePen 'ਤੇ ਕੁਝ ਦਿਲਚਸਪ ਕੈਨਵਸ ਡਰਾਇੰਗਾਂ ਵੇਖੋ। ਇੱਥੇ ਇੱਕ [ਖਾਸ ਤੌਰ 'ਤੇ ਪ੍ਰਭਾਵਸ਼ਾਲੀ ਉਦਾਹਰਨ](https://codepen.io/dissimulate/pen/KrAwx) ਹੈ।

## ਚਿੱਤਰ ਐਸੈਟ ਲੋਡ ਕਰੋ ਅਤੇ ਡਰਾਅ ਕਰੋ

ਤੁਸੀਂ ਇੱਕ ਚਿੱਤਰ ਐਸੈਟ ਨੂੰ `Image` ਆਬਜੈਕਟ ਬਣਾਕੇ ਅਤੇ ਇਸ ਦੀ `src` ਪ੍ਰਾਪਰਟੀ ਸੈਟ ਕਰਕੇ ਲੋਡ ਕਰਦੇ ਹੋ। ਫਿਰ ਤੁਸੀਂ `load` ਇਵੈਂਟ ਨੂੰ ਸੁਣਦੇ ਹੋ ਤਾਂ ਜੋ ਪਤਾ ਲੱਗੇ ਕਿ ਇਹ ਵਰਤਣ ਲਈ ਤਿਆਰ ਹੈ। ਕੋਡ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦਿੰਦਾ ਹੈ:

### ਐਸੈਟ ਲੋਡ ਕਰੋ

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### ਐਸੈਟ ਲੋਡ ਪੈਟਰਨ

ਉਪਰੋਕਤ ਨੂੰ ਇਸ ਤਰ੍ਹਾਂ ਦੇ ਸੰਰਚਨਾ ਵਿੱਚ ਲਪੇਟਣ ਦੀ ਸਿਫਾਰਿਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ, ਤਾਂ ਜੋ ਇਸਨੂੰ ਵਰਤਣਾ ਆਸਾਨ ਹੋਵੇ ਅਤੇ ਤੁਸੀਂ ਇਸਨੂੰ ਸਿਰਫ਼ ਤਦ ਹੀ ਮੈਨਿਪੂਲੇਟ ਕਰੋ ਜਦੋਂ ਇਹ ਪੂਰੀ ਤਰ੍ਹਾਂ ਲੋਡ ਹੋ ਜਾਵੇ:

```javascript
function loadAsset(path) {
  return new Promise((resolve) => {
    const img = new Image();
    img.src = path;
    img.onload = () => {
      // image loaded and ready to be used
      resolve(img);
    }
  })
}

// use like so

async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')
}

```

ਗੇਮ ਐਸੈਟਸ ਨੂੰ ਸਕ੍ਰੀਨ 'ਤੇ ਡਰਾਅ ਕਰਨ ਲਈ, ਤੁਹਾਡਾ ਕੋਡ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦੇਵੇਗਾ:

```javascript
async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')

  canvas = document.getElementById("myCanvas");
  ctx = canvas.getContext("2d");
  ctx.drawImage(heroImg, canvas.width/2,canvas.height/2);
  ctx.drawImage(monsterImg, 0,0);
}
```

## ਹੁਣ ਆਪਣਾ ਗੇਮ ਬਣਾਉਣ ਦੀ ਸ਼ੁਰੂਆਤ ਕਰੋ

### ਕੀ ਬਣਾਉਣਾ ਹੈ

ਤੁਸੀਂ ਇੱਕ ਵੈੱਬ ਪੰਨਾ ਬਣਾਉਣ ਜਾ ਰਹੇ ਹੋ ਜਿਸ ਵਿੱਚ ਇੱਕ ਕੈਨਵਸ ਤੱਤ ਹੋਵੇ। ਇਹ ਇੱਕ ਕਾਲੇ ਬੈਕਗ੍ਰਾਊਂਡ ਵਾਲੀ ਸਕ੍ਰੀਨ `1024*768` ਰੇਂਡਰ ਕਰੇਗਾ। ਅਸੀਂ ਤੁਹਾਨੂੰ ਦੋ ਚਿੱਤਰ ਦਿੱਤੇ ਹਨ:

- ਹੀਰੋ ਜਹਾਜ਼  

   ![ਹੀਰੋ ਜਹਾਜ਼](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.pa.png)

- 5*5 ਮਾਨਸਟਰ  

   ![ਮਾਨਸਟਰ ਜਹਾਜ਼](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.pa.png)

### ਵਿਕਾਸ ਸ਼ੁਰੂ ਕਰਨ ਲਈ ਸਿਫਾਰਿਸ਼ ਕੀਤੇ ਕਦਮ

ਉਹ ਫਾਈਲਾਂ ਲੱਭੋ ਜੋ ਤੁਹਾਡੇ ਲਈ `your-work` ਸਬ ਫੋਲਡਰ ਵਿੱਚ ਬਣਾਈ ਗਈਆਂ ਹਨ। ਇਸ ਵਿੱਚ ਹੇਠਾਂ ਦਿੱਤੇ ਹੋਣੇ ਚਾਹੀਦੇ ਹਨ:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Visual Studio Code ਵਿੱਚ ਇਸ ਫੋਲਡਰ ਦੀ ਕਾਪੀ ਖੋਲ੍ਹੋ। ਤੁਹਾਨੂੰ ਇੱਕ ਸਥਾਨਕ ਵਿਕਾਸ ਵਾਤਾਵਰਣ ਸੈਟਅੱਪ ਕਰਨ ਦੀ ਲੋੜ ਹੈ, ਵਧੀਆ Visual Studio Code ਦੇ ਨਾਲ NPM ਅਤੇ Node ਇੰਸਟਾਲ ਹੋਣੇ ਚਾਹੀਦੇ ਹਨ। ਜੇ ਤੁਹਾਡੇ ਕੰਪਿਊਟਰ 'ਤੇ `npm` ਸੈਟਅੱਪ ਨਹੀਂ ਹੈ, [ਇੱਥੇ ਕਿਵੇਂ ਕਰਨਾ ਹੈ](https://www.npmjs.com/get-npm)।

ਆਪਣੇ ਪ੍ਰੋਜੈਕਟ ਨੂੰ `your_work` ਫੋਲਡਰ ਵਿੱਚ ਨੈਵੀਗੇਟ ਕਰਕੇ ਸ਼ੁਰੂ ਕਰੋ:

```bash
cd your-work
npm start
```

ਉਪਰੋਕਤ HTTP ਸਰਵਰ ਪਤਾ `http://localhost:5000` 'ਤੇ ਸ਼ੁਰੂ ਕਰੇਗਾ। ਇੱਕ ਬ੍ਰਾਊਜ਼ਰ ਖੋਲ੍ਹੋ ਅਤੇ ਉਹ ਪਤਾ ਦਰਜ ਕਰੋ। ਇਹ ਇਸ ਸਮੇਂ ਇੱਕ ਖਾਲੀ ਪੰਨਾ ਹੈ, ਪਰ ਇਹ ਬਦਲ ਜਾਵੇਗਾ।

> ਨੋਟ: ਆਪਣੀ ਸਕ੍ਰੀਨ 'ਤੇ ਬਦਲਾਅ ਵੇਖਣ ਲਈ, ਆਪਣੇ ਬ੍ਰਾਊਜ਼ਰ ਨੂੰ ਰਿਫ੍ਰੈਸ਼ ਕਰੋ।

### ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ

`your-work/app.js` ਵਿੱਚ ਲੋੜੀਂਦਾ ਕੋਡ ਸ਼ਾਮਲ ਕਰੋ ਤਾਂ ਜੋ ਹੇਠਾਂ ਦਿੱਤੇ ਹੱਲ ਕੀਤੇ ਜਾ ਸਕਣ:

1. **ਕੈਨਵਸ ਡਰਾਅ ਕਰੋ** ਕਾਲੇ ਬੈਕਗ੍ਰਾਊਂਡ ਨਾਲ  
   > ਟਿਪ: `/app.js` ਵਿੱਚ ਸਹੀ TODO ਦੇ ਹੇਠਾਂ ਦੋ ਲਾਈਨਾਂ ਸ਼ਾਮਲ ਕਰੋ, `ctx` ਤੱਤ ਨੂੰ ਕਾਲਾ ਸੈਟ ਕਰੋ ਅਤੇ ਸਿਖਰ/ਖੱਬੇ ਕੋਆਰਡੀਨੇਟ 0,0 ਤੇ ਅਤੇ ਉਚਾਈ ਅਤੇ ਚੌੜਾਈ ਕੈਨਵਸ ਦੇ ਬਰਾਬਰ ਸੈਟ ਕਰੋ।  
2. **ਟੈਕਸਚਰ ਲੋਡ ਕਰੋ**  
   > ਟਿਪ: ਖਿਡਾਰੀ ਅਤੇ ਦੁਸ਼ਮਣ ਦੇ ਚਿੱਤਰ `await loadTexture` ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਤੇ ਚਿੱਤਰ ਦੇ ਰਸਤੇ ਪਾਸ ਕਰਕੇ ਸ਼ਾਮਲ ਕਰੋ। ਤੁਸੀਂ ਇਹਨਾਂ ਨੂੰ ਸਕ੍ਰੀਨ 'ਤੇ ਅਜੇ ਨਹੀਂ ਵੇਖੋਗੇ!  
3. **ਹੀਰੋ ਨੂੰ ਸਕ੍ਰੀਨ ਦੇ ਕੇਂਦਰ ਵਿੱਚ ਡਰਾਅ ਕਰੋ** ਹੇਠਲੇ ਅੱਧੇ ਵਿੱਚ  
   > ਟਿਪ: `drawImage` API ਦੀ ਵਰਤੋਂ ਕਰਕੇ `heroImg` ਨੂੰ ਸਕ੍ਰੀਨ 'ਤੇ ਡਰਾਅ ਕਰੋ, `canvas.width / 2 - 45` ਅਤੇ `canvas.height - canvas.height / 4)` ਸੈਟ ਕਰੋ।  
4. **5*5 ਮਾਨਸਟਰ ਡਰਾਅ ਕਰੋ**  
   > ਟਿਪ: ਹੁਣ ਤੁਸੀਂ ਦੁਸ਼ਮਣਾਂ ਨੂੰ ਸਕ੍ਰੀਨ 'ਤੇ ਡਰਾਅ ਕਰਨ ਲਈ ਕੋਡ ਨੂੰ ਅਨਕਮੈਂਟ ਕਰ ਸਕਦੇ ਹੋ। ਅਗਲੇ, `createEnemies` ਫੰਕਸ਼ਨ 'ਤੇ ਜਾਓ ਅਤੇ ਇਸਨੂੰ ਬਣਾਓ।  

   ਪਹਿਲਾਂ ਕੁਝ ਕਾਂਸਟੈਂਟਸ ਸੈਟ ਕਰੋ:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    ਫਿਰ, ਮਾਨਸਟਰਜ਼ ਦੀ ਐਰੇ ਨੂੰ ਸਕ੍ਰੀਨ 'ਤੇ ਡਰਾਅ ਕਰਨ ਲਈ ਇੱਕ ਲੂਪ ਬਣਾਓ:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## ਨਤੀਜਾ

ਅੰਤਮ ਨਤੀਜਾ ਇਸ ਤਰ੍ਹਾਂ ਦਿਖਾਈ ਦੇਣਾ ਚਾਹੀਦਾ ਹੈ:

![ਕਾਲੀ ਸਕ੍ਰੀਨ ਜਿਸ 'ਤੇ ਹੀਰੋ ਅਤੇ 5*5 ਮਾਨਸਟਰ ਹਨ](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.pa.png)

## ਹੱਲ

ਕਿਰਪਾ ਕਰਕੇ ਪਹਿਲਾਂ ਇਸਨੂੰ ਖੁਦ ਹੱਲ ਕਰਨ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰੋ ਪਰ ਜੇ ਤੁਸੀਂ ਫਸ ਜਾਓ, ਤਾਂ ਇੱਕ [ਹੱਲ](../../../../6-space-game/2-drawing-to-canvas/solution/app.js) ਵੇਖੋ।

---

## 🚀 ਚੁਣੌਤੀ

ਤੁਸੀਂ 2D-ਕੇਂਦਰਿਤ ਕੈਨਵਸ API ਨਾਲ ਡਰਾਇੰਗ ਬਾਰੇ ਸਿੱਖਿਆ ਹੈ; [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) ਬਾਰੇ ਵੇਖੋ ਅਤੇ ਇੱਕ 3D ਆਬਜੈਕਟ ਡਰਾਅ ਕਰਨ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰੋ।

## ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵਿਜ਼

[ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵਿਜ਼](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/32)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ ਅਧਿਐਨ

ਕੈਨਵਸ API ਬਾਰੇ ਹੋਰ ਜਾਣਕਾਰੀ ਪ੍ਰਾਪਤ ਕਰੋ [ਇਸਨੂੰ ਪੜ੍ਹ ਕੇ](https://developer.mozilla.org/docs/Web/API/Canvas_API)।

## ਅਸਾਈਨਮੈਂਟ

[ਕੈਨਵਸ API ਨਾਲ ਖੇਡੋ](assignment.md)

**ਅਸਵੀਕਾਰਨ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਯਤਨਸ਼ੀਲ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚੱਜੇਪਣ ਹੋ ਸਕਦੇ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼, ਜੋ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਹੈ, ਨੂੰ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।