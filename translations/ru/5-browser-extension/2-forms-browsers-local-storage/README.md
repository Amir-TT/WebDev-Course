<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e10f168beac4e7b05e30e0eb5c92bf11",
  "translation_date": "2025-08-25T23:27:35+00:00",
  "source_file": "5-browser-extension/2-forms-browsers-local-storage/README.md",
  "language_code": "ru"
}
-->
# Проект расширения для браузера, часть 2: Вызов API, использование локального хранилища

## Викторина перед лекцией

[Викторина перед лекцией](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/25)

### Введение

В этом уроке вы научитесь вызывать API, отправляя форму вашего расширения для браузера, и отображать результаты прямо в расширении. Кроме того, вы узнаете, как можно сохранять данные в локальном хранилище браузера для дальнейшего использования.

✅ Следуйте пронумерованным сегментам в соответствующих файлах, чтобы понять, куда вставлять код.

### Настройка элементов для работы в расширении:

К этому моменту вы уже создали HTML для формы и `<div>` для отображения результатов в вашем расширении. Теперь вам нужно работать в файле `/src/index.js` и постепенно собирать ваше расширение. Обратитесь к [предыдущему уроку](../1-about-browsers/README.md), чтобы вспомнить, как настроить проект и процесс сборки.

Работая в файле `index.js`, начните с создания нескольких переменных `const`, чтобы сохранить значения, связанные с различными полями:

```JavaScript
// form fields
const form = document.querySelector('.form-data');
const region = document.querySelector('.region-name');
const apiKey = document.querySelector('.api-key');

// results
const errors = document.querySelector('.errors');
const loading = document.querySelector('.loading');
const results = document.querySelector('.result-container');
const usage = document.querySelector('.carbon-usage');
const fossilfuel = document.querySelector('.fossil-fuel');
const myregion = document.querySelector('.my-region');
const clearBtn = document.querySelector('.clear-btn');
```

Все эти поля ссылаются на их CSS-классы, которые вы настроили в HTML в предыдущем уроке.

### Добавление слушателей событий

Далее добавьте слушатели событий для формы и кнопки очистки, которая сбрасывает форму. Это нужно, чтобы при отправке формы или нажатии кнопки сброса происходило определенное действие. Также добавьте вызов функции инициализации приложения в конце файла:

```JavaScript
form.addEventListener('submit', (e) => handleSubmit(e));
clearBtn.addEventListener('click', (e) => reset(e));
init();
```

✅ Обратите внимание на сокращенный синтаксис для прослушивания событий отправки или клика, и как событие передается в функции `handleSubmit` или `reset`. Можете ли вы написать эквивалент этого сокращенного синтаксиса в более длинной форме? Какой вариант вам больше нравится?

### Создание функций init() и reset():

Теперь вы создадите функцию, которая инициализирует расширение, называемую init():

```JavaScript
function init() {
	//if anything is in localStorage, pick it up
	const storedApiKey = localStorage.getItem('apiKey');
	const storedRegion = localStorage.getItem('regionName');

	//set icon to be generic green
	//todo

	if (storedApiKey === null || storedRegion === null) {
		//if we don't have the keys, show the form
		form.style.display = 'block';
		results.style.display = 'none';
		loading.style.display = 'none';
		clearBtn.style.display = 'none';
		errors.textContent = '';
	} else {
        //if we have saved keys/regions in localStorage, show results when they load
        displayCarbonUsage(storedApiKey, storedRegion);
		results.style.display = 'none';
		form.style.display = 'none';
		clearBtn.style.display = 'block';
	}
};

function reset(e) {
	e.preventDefault();
	//clear local storage for region only
	localStorage.removeItem('regionName');
	init();
}

```

В этой функции есть интересная логика. Прочитав ее, можете ли вы понять, что происходит?

- Создаются две переменные `const`, чтобы проверить, сохранил ли пользователь APIKey и код региона в локальном хранилище.
- Если одно из этих значений равно null, форма отображается, изменяя ее стиль на 'block'.
- Скрываются области результатов, загрузки и кнопка очистки, а текст ошибки устанавливается как пустая строка.
- Если ключ и регион существуют, запускается процедура:
  - вызов API для получения данных о выбросах углерода,
  - скрытие области результатов,
  - скрытие формы,
  - отображение кнопки сброса.

Перед тем как двигаться дальше, полезно узнать о важной концепции, доступной в браузерах: [LocalStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage). LocalStorage — это удобный способ хранения строк в браузере в виде пар `ключ-значение`. Этот тип веб-хранилища можно управлять с помощью JavaScript для работы с данными в браузере. LocalStorage не имеет срока действия, в то время как SessionStorage, другой вид веб-хранилища, очищается при закрытии браузера. У каждого типа хранилища есть свои плюсы и минусы.

> Замечание: ваше расширение для браузера имеет собственное локальное хранилище; главное окно браузера — это отдельный экземпляр и работает независимо.

Вы устанавливаете значение APIKey как строку, например, и можете увидеть, что оно установлено в Edge, "инспектируя" веб-страницу (вы можете щелкнуть правой кнопкой мыши в браузере, чтобы открыть инспектор) и перейдя на вкладку Applications, чтобы увидеть хранилище.

![Панель локального хранилища](../../../../translated_images/localstorage.472f8147b6a3f8d141d9551c95a2da610ac9a3c6a73d4a1c224081c98bae09d9.ru.png)

✅ Подумайте о ситуациях, когда вы НЕ захотите сохранять данные в LocalStorage. В общем, хранение API-ключей в LocalStorage — плохая идея! Можете ли вы понять, почему? В нашем случае, поскольку наше приложение предназначено только для обучения и не будет опубликовано в магазине приложений, мы используем этот метод.

Обратите внимание, что вы используете Web API для работы с LocalStorage, используя `getItem()`, `setItem()` или `removeItem()`. Этот API широко поддерживается в браузерах.

Прежде чем создавать функцию `displayCarbonUsage()`, которая вызывается в `init()`, давайте реализуем функциональность для обработки начальной отправки формы.

### Обработка отправки формы

Создайте функцию `handleSubmit`, которая принимает аргумент события `(e)`. Остановите распространение события (в данном случае мы хотим предотвратить обновление браузера) и вызовите новую функцию `setUpUser`, передав ей аргументы `apiKey.value` и `region.value`. Таким образом, вы используете два значения, которые вводятся через начальную форму, когда соответствующие поля заполнены.

```JavaScript
function handleSubmit(e) {
	e.preventDefault();
	setUpUser(apiKey.value, region.value);
}
```

✅ Освежите память: HTML, который вы настроили в прошлом уроке, имеет два поля ввода, значения которых захватываются через `const`, которые вы настроили в начале файла, и оба поля являются `required`, поэтому браузер предотвращает ввод пустых значений.

### Настройка пользователя

Переходя к функции `setUpUser`, здесь вы устанавливаете значения локального хранилища для apiKey и regionName. Добавьте новую функцию:

```JavaScript
function setUpUser(apiKey, regionName) {
	localStorage.setItem('apiKey', apiKey);
	localStorage.setItem('regionName', regionName);
	loading.style.display = 'block';
	errors.textContent = '';
	clearBtn.style.display = 'block';
	//make initial call
	displayCarbonUsage(apiKey, regionName);
}
```

Эта функция отображает сообщение о загрузке, пока вызывается API. На этом этапе вы подошли к созданию самой важной функции этого расширения для браузера!

### Отображение данных о выбросах углерода

Наконец, пришло время сделать запрос к API!

Прежде чем двигаться дальше, стоит обсудить API. API, или [Application Programming Interfaces](https://www.webopedia.com/TERM/A/API.html), — это важный элемент в арсенале веб-разработчика. Они предоставляют стандартные способы взаимодействия и интеграции программ. Например, если вы создаете веб-сайт, который должен делать запросы к базе данных, кто-то мог создать API для использования. Хотя существует множество типов API, одним из самых популярных является [REST API](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/).

✅ Термин 'REST' означает 'Representational State Transfer' и предполагает использование различных URL для получения данных. Проведите небольшое исследование о различных типах API, доступных разработчикам. Какой формат вам кажется наиболее удобным?

Есть важные моменты, которые нужно отметить в этой функции. Во-первых, обратите внимание на ключевое слово [`async`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function). Написание функций так, чтобы они выполнялись асинхронно, означает, что они ждут завершения действия, например, получения данных, прежде чем продолжить.

Вот короткое видео о `async`:

[![Async и Await для управления обещаниями](https://img.youtube.com/vi/YwmlRkrxvkk/0.jpg)](https://youtube.com/watch?v=YwmlRkrxvkk "Async и Await для управления обещаниями")

> 🎥 Нажмите на изображение выше, чтобы посмотреть видео о async/await.

Создайте новую функцию для запроса к API C02Signal:

```JavaScript
import axios from '../node_modules/axios';

async function displayCarbonUsage(apiKey, region) {
	try {
		await axios
			.get('https://api.co2signal.com/v1/latest', {
				params: {
					countryCode: region,
				},
				headers: {
					'auth-token': apiKey,
				},
			})
			.then((response) => {
				let CO2 = Math.floor(response.data.data.carbonIntensity);

				//calculateColor(CO2);

				loading.style.display = 'none';
				form.style.display = 'none';
				myregion.textContent = region;
				usage.textContent =
					Math.round(response.data.data.carbonIntensity) + ' grams (grams C02 emitted per kilowatt hour)';
				fossilfuel.textContent =
					response.data.data.fossilFuelPercentage.toFixed(2) +
					'% (percentage of fossil fuels used to generate electricity)';
				results.style.display = 'block';
			});
	} catch (error) {
		console.log(error);
		loading.style.display = 'none';
		results.style.display = 'none';
		errors.textContent = 'Sorry, we have no data for the region you have requested.';
	}
}
```

Это большая функция. Что здесь происходит?

- Следуя лучшим практикам, вы используете ключевое слово `async`, чтобы функция работала асинхронно. Функция содержит блок `try/catch`, так как она возвращает обещание, когда API возвращает данные. Поскольку вы не контролируете скорость ответа API (он может вообще не ответить!), вам нужно справляться с этой неопределенностью, вызывая его асинхронно.
- Вы делаете запрос к API co2signal, чтобы получить данные о вашем регионе, используя ваш API-ключ. Чтобы использовать этот ключ, необходимо применить тип аутентификации в параметрах заголовка.
- После ответа API вы назначаете различные элементы его данных на части экрана, которые вы настроили для отображения этих данных.
- Если возникает ошибка или результат отсутствует, вы отображаете сообщение об ошибке.

✅ Использование асинхронных шаблонов программирования — еще один полезный инструмент в вашем арсенале. Прочитайте [о различных способах](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) настройки такого кода.

Поздравляем! Если вы соберете ваше расширение (`npm run build`) и обновите его в панели расширений, у вас будет рабочее расширение! Единственное, что пока не работает, — это значок, и вы исправите это в следующем уроке.

---

## 🚀 Задание

Мы обсудили несколько типов API в этих уроках. Выберите веб-API и изучите его более подробно. Например, посмотрите на API, доступные в браузерах, такие как [HTML Drag and Drop API](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API). Что, по вашему мнению, делает API отличным?

## Викторина после лекции

[Викторина после лекции](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/26)

## Обзор и самостоятельное изучение

В этом уроке вы узнали о LocalStorage и API, оба из которых очень полезны для профессионального веб-разработчика. Можете ли вы подумать, как эти две вещи работают вместе? Подумайте, как вы бы спроектировали веб-сайт, который сохраняет элементы для использования API.

## Задание

[Выберите API](assignment.md)

**Отказ от ответственности**:  
Этот документ был переведен с использованием сервиса автоматического перевода [Co-op Translator](https://github.com/Azure/co-op-translator). Несмотря на наши усилия обеспечить точность, автоматические переводы могут содержать ошибки или неточности. Оригинальный документ на его родном языке следует считать авторитетным источником. Для получения критически важной информации рекомендуется профессиональный перевод человеком. Мы не несем ответственности за любые недоразумения или неправильные интерпретации, возникающие в результате использования данного перевода.