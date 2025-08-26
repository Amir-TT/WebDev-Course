<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d9da6dc61fb712b29f65e108c79b8a5d",
  "translation_date": "2025-08-25T22:30:58+00:00",
  "source_file": "6-space-game/1-introduction/README.md",
  "language_code": "pa"
}
-->
# ਸਪੇਸ ਗੇਮ ਬਣਾਓ ਭਾਗ 1: ਪਰਿਚਯ

![video](../../../../6-space-game/images/pewpew.gif)

## ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵੀਜ਼

[ਲੈਕਚਰ ਤੋਂ ਪਹਿਲਾਂ ਕਵੀਜ਼](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/29)

### ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਵਿੱਚ ਇਨਹੈਰਿਟੈਂਸ ਅਤੇ ਕੰਪੋਜ਼ੀਸ਼ਨ

ਪਿਛਲੇ ਪਾਠਾਂ ਵਿੱਚ, ਤੁਸੀਂ ਜੋ ਐਪ ਬਣਾਏ ਉਹ ਛੋਟੇ ਪ੍ਰਾਜੈਕਟ ਸਨ, ਇਸ ਲਈ ਡਿਜ਼ਾਈਨ ਆਰਕੀਟੈਕਚਰ ਬਾਰੇ ਜ਼ਿਆਦਾ ਸੋਚਣ ਦੀ ਲੋੜ ਨਹੀਂ ਸੀ। ਪਰ ਜਦੋਂ ਤੁਹਾਡੇ ਐਪਲੀਕੇਸ਼ਨ ਦਾ ਆਕਾਰ ਅਤੇ ਗੁੰਝਲਦਾਰਪਨ ਵਧਦਾ ਹੈ, ਤਾਂ ਆਰਕੀਟੈਕਚਰਲ ਫੈਸਲੇ ਮਹੱਤਵਪੂਰਨ ਹੋ ਜਾਂਦੇ ਹਨ। ਜਾਵਾਸਕ੍ਰਿਪਟ ਵਿੱਚ ਵੱਡੇ ਐਪਲੀਕੇਸ਼ਨ ਬਣਾਉਣ ਦੇ ਦੋ ਮੁੱਖ ਤਰੀਕੇ ਹਨ: *ਕੰਪੋਜ਼ੀਸ਼ਨ* ਜਾਂ *ਇਨਹੈਰਿਟੈਂਸ*। ਦੋਹਾਂ ਦੇ ਫਾਇਦੇ ਅਤੇ ਨੁਕਸਾਨ ਹਨ, ਪਰ ਆਓ ਇਸਨੂੰ ਇੱਕ ਗੇਮ ਦੇ ਸੰਦਰਭ ਵਿੱਚ ਸਮਝੀਏ।

✅ ਸਭ ਤੋਂ ਮਸ਼ਹੂਰ ਪ੍ਰੋਗ੍ਰਾਮਿੰਗ ਕਿਤਾਬਾਂ ਵਿੱਚੋਂ ਇੱਕ [ਡਿਜ਼ਾਈਨ ਪੈਟਰਨਜ਼](https://en.wikipedia.org/wiki/Design_Patterns) ਬਾਰੇ ਹੈ।

ਇੱਕ ਗੇਮ ਵਿੱਚ ਤੁਹਾਡੇ ਕੋਲ `game objects` ਹੁੰਦੇ ਹਨ, ਜੋ ਸਕ੍ਰੀਨ 'ਤੇ ਮੌਜੂਦ ਹੁੰਦੇ ਹਨ। ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਉਹਨਾਂ ਦੀ ਕਾਰਟੀਸ਼ੀਅਨ ਕੋਆਰਡੀਨੇਟ ਸਿਸਟਮ ਵਿੱਚ ਇੱਕ ਸਥਿਤੀ ਹੁੰਦੀ ਹੈ, ਜਿਸਨੂੰ `x` ਅਤੇ `y` ਕੋਆਰਡੀਨੇਟ ਦੁਆਰਾ ਦਰਸਾਇਆ ਜਾਂਦਾ ਹੈ। ਜਦੋਂ ਤੁਸੀਂ ਗੇਮ ਵਿਕਸਿਤ ਕਰਦੇ ਹੋ, ਤਾਂ ਤੁਸੀਂ ਦੇਖੋਗੇ ਕਿ ਤੁਹਾਡੇ ਸਾਰੇ ਗੇਮ ਆਬਜੈਕਟਾਂ ਵਿੱਚ ਕੁਝ ਸਧਾਰਨ ਗੁਣ ਹੁੰਦੇ ਹਨ, ਜੋ ਹਰ ਗੇਮ ਵਿੱਚ ਆਮ ਹੁੰਦੇ ਹਨ:

- **ਸਥਿਤੀ-ਅਧਾਰਿਤ** ਜ਼ਿਆਦਾਤਰ, ਜੇਕਰ ਸਾਰੇ ਨਹੀਂ, ਗੇਮ ਦੇ ਤੱਤ ਸਥਿਤੀ-ਅਧਾਰਿਤ ਹੁੰਦੇ ਹਨ। ਇਸਦਾ ਮਤਲਬ ਹੈ ਕਿ ਉਹਨਾਂ ਦੀ ਇੱਕ ਸਥਿਤੀ ਹੁੰਦੀ ਹੈ, `x` ਅਤੇ `y`।
- **ਚਲਣਯੋਗ** ਇਹ ਉਹ ਆਬਜੈਕਟ ਹੁੰਦੇ ਹਨ ਜੋ ਨਵੀਂ ਸਥਿਤੀ 'ਤੇ ਚੱਲ ਸਕਦੇ ਹਨ। ਇਹ ਆਮ ਤੌਰ 'ਤੇ ਇੱਕ ਹੀਰੋ, ਰਾਕਸ਼ਸ ਜਾਂ NPC (ਨਾਨ ਪਲੇਅਰ ਕਿਰਦਾਰ) ਹੁੰਦੇ ਹਨ, ਪਰ ਉਦਾਹਰਣ ਲਈ, ਇੱਕ ਸਥਿਰ ਆਬਜੈਕਟ ਜਿਵੇਂ ਕਿ ਦਰੱਖਤ ਨਹੀਂ।
- **ਸਵੈ-ਵਿਨਾਸ਼ੀ** ਇਹ ਆਬਜੈਕਟ ਸਿਰਫ਼ ਇੱਕ ਨਿਰਧਾਰਤ ਸਮੇਂ ਲਈ ਮੌਜੂਦ ਰਹਿੰਦੇ ਹਨ ਅਤੇ ਫਿਰ ਮਿਟਾਉਣ ਲਈ ਤਿਆਰ ਹੋ ਜਾਂਦੇ ਹਨ। ਆਮ ਤੌਰ 'ਤੇ ਇਹ ਇੱਕ `dead` ਜਾਂ `destroyed` ਬੂਲੀਅਨ ਦੁਆਰਾ ਦਰਸਾਇਆ ਜਾਂਦਾ ਹੈ ਜੋ ਗੇਮ ਇੰਜਨ ਨੂੰ ਸੂਚਿਤ ਕਰਦਾ ਹੈ ਕਿ ਇਹ ਆਬਜੈਕਟ ਹੁਣ ਨਹੀਂ ਦਿਖਾਇਆ ਜਾਣਾ ਚਾਹੀਦਾ।
- **ਕੂਲ-ਡਾਊਨ** 'ਕੂਲ-ਡਾਊਨ' ਛੋਟੇ ਸਮੇਂ ਲਈ ਮੌਜੂਦ ਆਬਜੈਕਟਾਂ ਵਿੱਚ ਇੱਕ ਆਮ ਗੁਣ ਹੈ। ਇੱਕ ਆਮ ਉਦਾਹਰਣ ਇੱਕ ਟੈਕਸਟ ਜਾਂ ਗ੍ਰਾਫਿਕਲ ਪ੍ਰਭਾਵ ਜਿਵੇਂ ਕਿ ਧਮਾਕਾ ਹੈ ਜੋ ਸਿਰਫ ਕੁਝ ਮਿਲੀਸੈਕੰਡਾਂ ਲਈ ਦਿਖਾਈ ਦੇਣਾ ਚਾਹੀਦਾ ਹੈ।

✅ ਪੈਕ-ਮੈਨ ਵਰਗੇ ਗੇਮ ਬਾਰੇ ਸੋਚੋ। ਕੀ ਤੁਸੀਂ ਇਸ ਗੇਮ ਵਿੱਚ ਉਪਰੋਕਤ ਚਾਰ ਆਬਜੈਕਟ ਪ੍ਰਕਾਰਾਂ ਦੀ ਪਛਾਣ ਕਰ ਸਕਦੇ ਹੋ?

### ਵਿਵਹਾਰ ਨੂੰ ਪ੍ਰਗਟ ਕਰਨਾ

ਉਪਰ ਦਿੱਤੇ ਗਏ ਸਾਰੇ ਗੁਣ ਉਹ ਵਿਵਹਾਰ ਹਨ ਜੋ ਗੇਮ ਆਬਜੈਕਟਾਂ ਵਿੱਚ ਹੋ ਸਕਦੇ ਹਨ। ਤਾਂ ਅਸੀਂ ਇਹਨਾਂ ਨੂੰ ਕਿਵੇਂ ਕੋਡ ਕਰੀਏ? ਅਸੀਂ ਇਹ ਵਿਵਹਾਰ ਕਲਾਸਾਂ ਜਾਂ ਆਬਜੈਕਟਾਂ ਨਾਲ ਜੁੜੇ ਹੋਏ ਮੈਥਡਾਂ ਵਜੋਂ ਪ੍ਰਗਟ ਕਰ ਸਕਦੇ ਹਾਂ।

**ਕਲਾਸਾਂ**

ਵਿਚਾਰ ਇਹ ਹੈ ਕਿ `ਕਲਾਸਾਂ` ਨੂੰ `ਇਨਹੈਰਿਟੈਂਸ` ਦੇ ਨਾਲ ਵਰਤ ਕੇ ਇੱਕ ਕਲਾਸ ਵਿੱਚ ਵਿਸ਼ੇਸ਼ ਵਿਵਹਾਰ ਸ਼ਾਮਲ ਕੀਤਾ ਜਾਵੇ।

✅ ਇਨਹੈਰਿਟੈਂਸ ਇੱਕ ਮਹੱਤਵਪੂਰਨ ਸੰਕਲਪ ਹੈ। [MDN ਦੇ ਲੇਖ ਬਾਰੇ ਇਨਹੈਰਿਟੈਂਸ](https://developer.mozilla.org/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) 'ਤੇ ਹੋਰ ਜਾਣੋ।

ਕੋਡ ਦੁਆਰਾ ਪ੍ਰਗਟ ਕੀਤਾ ਗਿਆ, ਇੱਕ ਗੇਮ ਆਬਜੈਕਟ ਆਮ ਤੌਰ 'ਤੇ ਇਸ ਤਰ੍ਹਾਂ ਲੱਗ ਸਕਦਾ ਹੈ:

```javascript

//set up the class GameObject
class GameObject {
  constructor(x, y, type) {
    this.x = x;
    this.y = y;
    this.type = type;
  }
}

//this class will extend the GameObject's inherent class properties
class Movable extends GameObject {
  constructor(x,y, type) {
    super(x,y, type)
  }

//this movable object can be moved on the screen
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}

//this is a specific class that extends the Movable class, so it can take advantage of all the properties that it inherits
class Hero extends Movable {
  constructor(x,y) {
    super(x,y, 'Hero')
  }
}

//this class, on the other hand, only inherits the GameObject properties
class Tree extends GameObject {
  constructor(x,y) {
    super(x,y, 'Tree')
  }
}

//a hero can move...
const hero = new Hero();
hero.moveTo(5,5);

//but a tree cannot
const tree = new Tree();
```

✅ ਕੁਝ ਮਿੰਟ ਲਓ ਅਤੇ ਪੈਕ-ਮੈਨ ਹੀਰੋ (ਉਦਾਹਰਣ ਲਈ, ਇੰਕੀ, ਪਿੰਕੀ ਜਾਂ ਬਲਿੰਕੀ) ਨੂੰ ਦੁਬਾਰਾ ਸੋਚੋ ਅਤੇ ਇਹ ਕਿਵੇਂ ਜਾਵਾਸਕ੍ਰਿਪਟ ਵਿੱਚ ਲਿਖਿਆ ਜਾਵੇਗਾ।

**ਕੰਪੋਜ਼ੀਸ਼ਨ**

ਆਬਜੈਕਟ ਇਨਹੈਰਿਟੈਂਸ ਨੂੰ ਸੰਭਾਲਣ ਦਾ ਇੱਕ ਵੱਖਰਾ ਤਰੀਕਾ *ਕੰਪੋਜ਼ੀਸ਼ਨ* ਹੈ। ਫਿਰ, ਆਬਜੈਕਟ ਇਸ ਤਰ੍ਹਾਂ ਆਪਣੇ ਵਿਵਹਾਰ ਨੂੰ ਪ੍ਰਗਟ ਕਰਦੇ ਹਨ:

```javascript
//create a constant gameObject
const gameObject = {
  x: 0,
  y: 0,
  type: ''
};

//...and a constant movable
const movable = {
  moveTo(x, y) {
    this.x = x;
    this.y = y;
  }
}
//then the constant movableObject is composed of the gameObject and movable constants
const movableObject = {...gameObject, ...movable};

//then create a function to create a new Hero who inherits the movableObject properties
function createHero(x, y) {
  return {
    ...movableObject,
    x,
    y,
    type: 'Hero'
  }
}
//...and a static object that inherits only the gameObject properties
function createStatic(x, y, type) {
  return {
    ...gameObject
    x,
    y,
    type
  }
}
//create the hero and move it
const hero = createHero(10,10);
hero.moveTo(5,5);
//and create a static tree which only stands around
const tree = createStatic(0,0, 'Tree'); 
```

**ਮੈਨੂੰ ਕਿਹੜਾ ਪੈਟਰਨ ਵਰਤਣਾ ਚਾਹੀਦਾ ਹੈ?**

ਇਹ ਤੁਹਾਡੇ ਉੱਤੇ ਨਿਰਭਰ ਕਰਦਾ ਹੈ ਕਿ ਤੁਸੀਂ ਕਿਹੜਾ ਪੈਟਰਨ ਚੁਣਦੇ ਹੋ। ਜਾਵਾਸਕ੍ਰਿਪਟ ਦੋਹਾਂ ਪੈਰਾਡਾਈਮਾਂ ਦਾ ਸਮਰਥਨ ਕਰਦਾ ਹੈ।

---

ਗੇਮ ਡਿਵੈਲਪਮੈਂਟ ਵਿੱਚ ਇੱਕ ਹੋਰ ਆਮ ਪੈਟਰਨ ਗੇਮ ਦੇ ਯੂਜ਼ਰ ਅਨੁਭਵ ਅਤੇ ਪ੍ਰਦਰਸ਼ਨ ਨੂੰ ਸੰਭਾਲਣ ਦੀ ਸਮੱਸਿਆ ਨੂੰ ਹੱਲ ਕਰਦਾ ਹੈ।

## ਪਬ/ਸਬ ਪੈਟਰਨ

✅ ਪਬ/ਸਬ ਦਾ ਮਤਲਬ ਹੈ 'ਪਬਲਿਸ਼-ਸਬਸਕ੍ਰਾਈਬ'

ਇਹ ਪੈਟਰਨ ਇਸ ਵਿਚਾਰ ਨੂੰ ਹੱਲ ਕਰਦਾ ਹੈ ਕਿ ਤੁਹਾਡੇ ਐਪਲੀਕੇਸ਼ਨ ਦੇ ਵੱਖ-ਵੱਖ ਹਿੱਸਿਆਂ ਨੂੰ ਇੱਕ ਦੂਜੇ ਬਾਰੇ ਜਾਣਨ ਦੀ ਲੋੜ ਨਹੀਂ ਹੋਣੀ ਚਾਹੀਦੀ। ਕਿਉਂ? ਇਹ ਸਮਝਣਾ ਬਹੁਤ ਆਸਾਨ ਬਣਾਉਂਦਾ ਹੈ ਕਿ ਕੁੱਲ ਮਿਲਾ ਕੇ ਕੀ ਚੱਲ ਰਿਹਾ ਹੈ ਜੇਕਰ ਵੱਖ-ਵੱਖ ਹਿੱਸੇ ਵੱਖਰੇ ਹਨ। ਇਹ ਇਸਨੂੰ ਅਚਾਨਕ ਵਿਵਹਾਰ ਬਦਲਣ ਲਈ ਵੀ ਆਸਾਨ ਬਣਾਉਂਦਾ ਹੈ ਜੇ ਤੁਹਾਨੂੰ ਲੋੜ ਹੋਵੇ। ਅਸੀਂ ਇਹ ਕਿਵੇਂ ਹਾਸਲ ਕਰਦੇ ਹਾਂ? ਅਸੀਂ ਕੁਝ ਸੰਕਲਪ ਸਥਾਪਿਤ ਕਰਕੇ ਇਹ ਕਰਦੇ ਹਾਂ:

- **ਸੁਨੇਹਾ**: ਇੱਕ ਸੁਨੇਹਾ ਆਮ ਤੌਰ 'ਤੇ ਇੱਕ ਟੈਕਸਟ ਸਟ੍ਰਿੰਗ ਹੁੰਦਾ ਹੈ ਜੋ ਇੱਕ ਵਿਕਲਪਿਕ ਪੇਲੋਡ (ਡਾਟਾ ਦਾ ਇੱਕ ਟੁਕੜਾ ਜੋ ਦੱਸਦਾ ਹੈ ਕਿ ਸੁਨੇਹਾ ਕਿਉਂ ਹੈ) ਨਾਲ ਹੁੰਦਾ ਹੈ। ਗੇਮ ਵਿੱਚ ਇੱਕ ਆਮ ਸੁਨੇਹਾ ਹੋ ਸਕਦਾ ਹੈ `KEY_PRESSED_ENTER`।
- **ਪਬਲਿਸ਼ਰ**: ਇਹ ਤੱਤ ਇੱਕ ਸੁਨੇਹਾ *ਪਬਲਿਸ਼* ਕਰਦਾ ਹੈ ਅਤੇ ਇਸਨੂੰ ਸਾਰੇ ਸਬਸਕ੍ਰਾਈਬਰਾਂ ਨੂੰ ਭੇਜਦਾ ਹੈ।
- **ਸਬਸਕ੍ਰਾਈਬਰ**: ਇਹ ਤੱਤ ਖਾਸ ਸੁਨੇਹਿਆਂ ਨੂੰ *ਸੁਣਦਾ* ਹੈ ਅਤੇ ਇਸ ਸੁਨੇਹੇ ਨੂੰ ਪ੍ਰਾਪਤ ਕਰਨ ਦੇ ਨਤੀਜੇ ਵਜੋਂ ਕੁਝ ਕੰਮ ਕਰਦਾ ਹੈ, ਜਿਵੇਂ ਕਿ ਲੇਜ਼ਰ ਚਲਾਉਣਾ।

ਇਸਦੀ ਇੰਪਲੀਮੈਂਟੇਸ਼ਨ ਆਕਾਰ ਵਿੱਚ ਬਹੁਤ ਛੋਟੀ ਹੁੰਦੀ ਹੈ ਪਰ ਇਹ ਬਹੁਤ ਸ਼ਕਤੀਸ਼ਾਲੀ ਪੈਟਰਨ ਹੈ। ਇਹ ਇਸ ਤਰ੍ਹਾਂ ਲਾਗੂ ਕੀਤਾ ਜਾ ਸਕਦਾ ਹੈ:

```javascript
//set up an EventEmitter class that contains listeners
class EventEmitter {
  constructor() {
    this.listeners = {};
  }
//when a message is received, let the listener to handle its payload
  on(message, listener) {
    if (!this.listeners[message]) {
      this.listeners[message] = [];
    }
    this.listeners[message].push(listener);
  }
//when a message is sent, send it to a listener with some payload
  emit(message, payload = null) {
    if (this.listeners[message]) {
      this.listeners[message].forEach(l => l(message, payload))
    }
  }
}

```

ਉਪਰੋਕਤ ਕੋਡ ਨੂੰ ਵਰਤਣ ਲਈ ਅਸੀਂ ਇੱਕ ਬਹੁਤ ਛੋਟੀ ਇੰਪਲੀਮੈਂਟੇਸ਼ਨ ਬਣਾ ਸਕਦੇ ਹਾਂ:

```javascript
//set up a message structure
const Messages = {
  HERO_MOVE_LEFT: 'HERO_MOVE_LEFT'
};
//invoke the eventEmitter you set up above
const eventEmitter = new EventEmitter();
//set up a hero
const hero = createHero(0,0);
//let the eventEmitter know to watch for messages pertaining to the hero moving left, and act on it
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});

//set up the window to listen for the keyup event, specifically if the left arrow is hit, emit a message to move the hero left
window.addEventListener('keyup', (evt) => {
  if (evt.key === 'ArrowLeft') {
    eventEmitter.emit(Messages.HERO_MOVE_LEFT)
  }
});
```

ਉਪਰ ਅਸੀਂ ਇੱਕ ਕੀਬੋਰਡ ਇਵੈਂਟ, `ArrowLeft` ਨੂੰ ਜੋੜਿਆ ਅਤੇ `HERO_MOVE_LEFT` ਸੁਨੇਹਾ ਭੇਜਿਆ। ਅਸੀਂ ਉਸ ਸੁਨੇਹੇ ਨੂੰ ਸੁਣਦੇ ਹਾਂ ਅਤੇ ਨਤੀਜੇ ਵਜੋਂ `hero` ਨੂੰ ਹਿਲਾਉਂਦੇ ਹਾਂ। ਇਸ ਪੈਟਰਨ ਦੀ ਤਾਕਤ ਇਹ ਹੈ ਕਿ ਇਵੈਂਟ ਲਿਸਨਰ ਅਤੇ ਹੀਰੋ ਇੱਕ ਦੂਜੇ ਬਾਰੇ ਨਹੀਂ ਜਾਣਦੇ। ਤੁਸੀਂ `ArrowLeft` ਨੂੰ `A` ਕੀ ਨਾਲ ਰੀਮੈਪ ਕਰ ਸਕਦੇ ਹੋ। ਇਸ ਤੋਂ ਇਲਾਵਾ, ਇਹ ਸੰਭਵ ਹੋਵੇਗਾ ਕਿ `ArrowLeft` 'ਤੇ ਕੁਝ ਪੂਰੀ ਤਰ੍ਹਾਂ ਵੱਖਰਾ ਕੀਤਾ ਜਾਵੇ, ਸਿਰਫ਼ eventEmitter ਦੇ `on` ਫੰਕਸ਼ਨ ਵਿੱਚ ਕੁਝ ਸੋਧਾਂ ਕਰਕੇ:

```javascript
eventEmitter.on(Messages.HERO_MOVE_LEFT, () => {
  hero.move(5,0);
});
```

ਜਿਵੇਂ ਜਿਵੇਂ ਤੁਹਾਡੀ ਗੇਮ ਵਧਦੀ ਹੈ ਅਤੇ ਗੁੰਝਲਦਾਰ ਹੁੰਦੀ ਹੈ, ਇਹ ਪੈਟਰਨ ਇੱਕੋ ਜਿਹਾ ਰਹਿੰਦਾ ਹੈ ਅਤੇ ਤੁਹਾਡਾ ਕੋਡ ਸਾਫ ਰਹਿੰਦਾ ਹੈ। ਇਸ ਪੈਟਰਨ ਨੂੰ ਅਪਨਾਉਣਾ ਵਾਕਈ ਸਿਫਾਰਸ਼ੀ ਹੈ।

---

## 🚀 ਚੁਣੌਤੀ

ਸੋਚੋ ਕਿ ਪਬ-ਸਬ ਪੈਟਰਨ ਕਿਸ ਤਰ੍ਹਾਂ ਗੇਮ ਨੂੰ ਬਿਹਤਰ ਬਣਾ ਸਕਦਾ ਹੈ। ਕਿਹੜੇ ਹਿੱਸੇ ਇਵੈਂਟ ਜਾਰੀ ਕਰਨੇ ਚਾਹੀਦੇ ਹਨ, ਅਤੇ ਗੇਮ ਨੂੰ ਉਹਨਾਂ 'ਤੇ ਕਿਵੇਂ ਪ੍ਰਤੀਕਿਰਿਆ ਕਰਨੀ ਚਾਹੀਦੀ ਹੈ? ਹੁਣ ਤੁਹਾਡੇ ਕੋਲ ਇੱਕ ਨਵੀਂ ਗੇਮ ਬਾਰੇ ਸੋਚਣ ਅਤੇ ਇਸਦੇ ਹਿੱਸਿਆਂ ਦੇ ਵਿਵਹਾਰ ਬਾਰੇ ਰਚਨਾਤਮਕ ਹੋਣ ਦਾ ਮੌਕਾ ਹੈ।

## ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵੀਜ਼

[ਲੈਕਚਰ ਤੋਂ ਬਾਅਦ ਕਵੀਜ਼](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/30)

## ਸਮੀਖਿਆ ਅਤੇ ਸਵੈ ਅਧਿਐਨ

ਪਬ/ਸਬ ਬਾਰੇ ਹੋਰ ਜਾਣੋ [ਇਸ ਬਾਰੇ ਪੜ੍ਹ ਕੇ](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber/?WT.mc_id=academic-77807-sagibbon)।

## ਅਸਾਈਨਮੈਂਟ

[ਗੇਮ ਦਾ ਮੌਕ-ਅੱਪ ਬਣਾਓ](assignment.md)

**ਅਸਵੀਕਾਰਨਾ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀ ਹੋਣ ਦੀ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਦਿਓ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸੁਚਨਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਨੂੰ ਇਸਦੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਅਧਿਕਾਰਤ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਪੈਦਾ ਹੋਣ ਵਾਲੇ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।