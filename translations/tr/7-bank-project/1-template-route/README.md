<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8da1b5e2c63f749808858c53f37b8ce7",
  "translation_date": "2025-08-26T00:36:46+00:00",
  "source_file": "7-bank-project/1-template-route/README.md",
  "language_code": "tr"
}
-->
# Bir Bankacılık Uygulaması Oluşturma Bölüm 1: Web Uygulamasında HTML Şablonları ve Yönlendirmeler

## Ders Öncesi Test

[Ders öncesi test](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/41)

### Giriş

JavaScript'in tarayıcılarda kullanılmaya başlanmasından bu yana, web siteleri her zamankinden daha etkileşimli ve karmaşık hale geldi. Web teknolojileri artık doğrudan tarayıcıda çalışan ve [web uygulamaları](https://en.wikipedia.org/wiki/Web_application) olarak adlandırılan tam işlevsel uygulamalar oluşturmak için yaygın olarak kullanılmaktadır. Web uygulamaları oldukça etkileşimli olduğundan, kullanıcılar bir işlem gerçekleştirildiğinde her seferinde sayfanın tamamen yeniden yüklenmesini beklemek istemez. Bu nedenle, JavaScript, HTML'yi doğrudan DOM kullanarak güncellemek ve daha akıcı bir kullanıcı deneyimi sağlamak için kullanılır.

Bu derste, bir banka web uygulaması oluşturmak için temel adımları atacağız. HTML şablonlarını kullanarak, tüm HTML sayfasını yeniden yüklemek zorunda kalmadan görüntülenebilen ve güncellenebilen birden fazla ekran oluşturacağız.

### Ön Koşul

Bu derste oluşturacağımız web uygulamasını test etmek için yerel bir web sunucusuna ihtiyacınız var. Eğer bir web sunucunuz yoksa, [Node.js](https://nodejs.org) yükleyebilir ve proje klasörünüzden `npx lite-server` komutunu kullanabilirsiniz. Bu, yerel bir web sunucusu oluşturur ve uygulamanızı bir tarayıcıda açar.

### Hazırlık

Bilgisayarınızda `bank` adında bir klasör oluşturun ve içine `index.html` adında bir dosya ekleyin. Bu HTML [şablon kodu](https://en.wikipedia.org/wiki/Boilerplate_code) ile başlayacağız:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank App</title>
  </head>
  <body>
    <!-- This is where you'll work -->
  </body>
</html>
```

---

## HTML Şablonları

Bir web sayfası için birden fazla ekran oluşturmak istiyorsanız, bir çözüm, görüntülemek istediğiniz her ekran için bir HTML dosyası oluşturmaktır. Ancak, bu çözüm bazı zorluklar içerir:

- Ekranlar arasında geçiş yaparken tüm HTML'yi yeniden yüklemeniz gerekir, bu da yavaş olabilir.
- Farklı ekranlar arasında veri paylaşmak zorlaşır.

Başka bir yaklaşım ise yalnızca bir HTML dosyasına sahip olmak ve `<template>` öğesini kullanarak birden fazla [HTML şablonu](https://developer.mozilla.org/docs/Web/HTML/Element/template) tanımlamaktır. Şablon, tarayıcı tarafından görüntülenmeyen ve çalışma zamanında JavaScript kullanılarak örneklenmesi gereken yeniden kullanılabilir bir HTML bloğudur.

### Görev

Bir giriş sayfası ve bir kontrol paneli olmak üzere iki ekranlı bir banka uygulaması oluşturacağız. İlk olarak, HTML gövdesine, uygulamamızın farklı ekranlarını örneklemek için kullanacağımız bir yer tutucu öğesi ekleyelim:

```html
<div id="app">Loading...</div>
```

Bu öğeye, daha sonra JavaScript ile kolayca bulabilmek için bir `id` veriyoruz.

> İpucu: Bu öğenin içeriği değiştirileceği için, uygulama yüklenirken gösterilecek bir yükleme mesajı veya göstergesi ekleyebilirsiniz.

Sonra, giriş sayfası için HTML şablonunu ekleyelim. Şimdilik, yalnızca bir başlık ve gezinme yapmak için kullanacağımız bir bağlantı içeren bir bölüm ekleyeceğiz.

```html
<template id="login">
  <h1>Bank App</h1>
  <section>
    <a href="/dashboard">Login</a>
  </section>
</template>
```

Daha sonra, kontrol paneli sayfası için başka bir HTML şablonu ekleyeceğiz. Bu sayfa farklı bölümler içerecek:

- Bir başlık, bir başlık ve çıkış bağlantısı ile
- Banka hesabının mevcut bakiyesi
- Bir tabloda görüntülenen işlem listesi

```html
<template id="dashboard">
  <header>
    <h1>Bank App</h1>
    <a href="/login">Logout</a>
  </header>
  <section>
    Balance: 100$
  </section>
  <section>
    <h2>Transactions</h2>
    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Object</th>
          <th>Amount</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </section>
</template>
```

> İpucu: HTML şablonları oluştururken, nasıl görüneceğini görmek isterseniz, `<template>` ve `</template>` satırlarını `<!-- -->` ile yorum satırı haline getirebilirsiniz.

✅ Sizce neden şablonlara `id` özellikleri ekliyoruz? Bunun yerine sınıflar gibi başka bir şey kullanabilir miydik?

## JavaScript ile Şablonları Görüntüleme

Mevcut HTML dosyanızı bir tarayıcıda denerseniz, `Loading...` yazısında takılı kaldığını görürsünüz. Bunun nedeni, HTML şablonlarını örneklemek ve görüntülemek için biraz JavaScript kodu eklememiz gerektiğidir.

Bir şablonu örneklemek genellikle 3 adımda yapılır:

1. Şablon öğesini DOM'da bulun, örneğin [`document.getElementById`](https://developer.mozilla.org/docs/Web/API/Document/getElementById) kullanarak.
2. Şablon öğesini [`cloneNode`](https://developer.mozilla.org/docs/Web/API/Node/cloneNode) kullanarak kopyalayın.
3. Görünür bir öğenin altına, örneğin [`appendChild`](https://developer.mozilla.org/docs/Web/API/Node/appendChild) kullanarak, DOM'a ekleyin.

✅ Şablonu DOM'a eklemeden önce neden kopyalamamız gerekiyor? Bu adımı atlarsak ne olur?

### Görev

Proje klasörünüzde `app.js` adında yeni bir dosya oluşturun ve bu dosyayı HTML'nizin `<head>` bölümüne dahil edin:

```html
<script src="app.js" defer></script>
```

Şimdi `app.js` içinde, yeni bir `updateRoute` fonksiyonu oluşturacağız:

```js
function updateRoute(templateId) {
  const template = document.getElementById(templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

Burada yaptığımız şey, yukarıda açıklanan 3 adımı tam olarak uygulamaktır. `templateId` kimliğine sahip şablonu örnekliyoruz ve kopyalanan içeriğini uygulama yer tutucumuzun içine koyuyoruz. Tüm alt ağacı kopyalamak için `cloneNode(true)` kullanmamız gerektiğini unutmayın.

Şimdi bu fonksiyonu bir şablonla çağırın ve sonucu inceleyin.

```js
updateRoute('login');
```

✅ `app.innerHTML = '';` kodunun amacı nedir? Bu kod olmadan ne olur?

## Yönlendirmeler Oluşturma

Bir web uygulamasından bahsederken, *Yönlendirme*, **URL'leri** görüntülenmesi gereken belirli ekranlarla eşleştirme niyetini ifade eder. Birden fazla HTML dosyasına sahip bir web sitesinde, bu işlem dosya yolları URL'de yansıtıldığı için otomatik olarak yapılır. Örneğin, proje klasörünüzde şu dosyalar varsa:

```
mywebsite/index.html
mywebsite/login.html
mywebsite/admin/index.html
```

`mywebsite` kök dizini ile bir web sunucusu oluşturursanız, URL eşlemesi şu şekilde olur:

```
https://site.com            --> mywebsite/index.html
https://site.com/login.html --> mywebsite/login.html
https://site.com/admin/     --> mywebsite/admin/index.html
```

Ancak, web uygulamamız için tüm ekranları içeren tek bir HTML dosyası kullandığımızdan, bu varsayılan davranış bize yardımcı olmayacaktır. Bu haritayı manuel olarak oluşturmamız ve görüntülenen şablonu JavaScript kullanarak güncellememiz gerekiyor.

### Görev

URL yolları ile şablonlarımızı eşleştirmek için basit bir nesne kullanacağız. Bu nesneyi `app.js` dosyanızın en üstüne ekleyin.

```js
const routes = {
  '/login': { templateId: 'login' },
  '/dashboard': { templateId: 'dashboard' },
};
```

Şimdi `updateRoute` fonksiyonunu biraz değiştirelim. `templateId`'yi doğrudan bir argüman olarak geçirmek yerine, önce mevcut URL'ye bakarak ve ardından haritamızı kullanarak ilgili şablon kimliği değerini alarak elde etmek istiyoruz. URL'nin yalnızca yol bölümünü almak için [`window.location.pathname`](https://developer.mozilla.org/docs/Web/API/Location/pathname) kullanabiliriz.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  const template = document.getElementById(route.templateId);
  const view = template.content.cloneNode(true);
  const app = document.getElementById('app');
  app.innerHTML = '';
  app.appendChild(view);
}
```

Burada tanımladığımız yönlendirmeleri ilgili şablonla eşleştirdik. Tarayıcınızda URL'yi manuel olarak değiştirerek doğru çalışıp çalışmadığını kontrol edebilirsiniz.

✅ URL'ye bilinmeyen bir yol girerseniz ne olur? Bunu nasıl çözebiliriz?

## Gezinme Ekleme

Uygulamamızın bir sonraki adımı, URL'yi manuel olarak değiştirmek zorunda kalmadan sayfalar arasında gezinme olanağı eklemektir. Bu iki şeyi içerir:

1. Mevcut URL'yi güncelleme
2. Yeni URL'ye göre görüntülenen şablonu güncelleme

İkinci kısmı zaten `updateRoute` fonksiyonu ile hallettik, bu yüzden mevcut URL'yi nasıl güncelleyeceğimizi bulmamız gerekiyor.

JavaScript ve özellikle [`history.pushState`](https://developer.mozilla.org/docs/Web/API/History/pushState) kullanmamız gerekecek. Bu yöntem, HTML'yi yeniden yüklemeden URL'yi güncellemeye ve tarama geçmişinde yeni bir giriş oluşturmaya olanak tanır.

> Not: HTML bağlantı öğesi [`<a href>`](https://developer.mozilla.org/docs/Web/HTML/Element/a) kendi başına farklı URL'lere bağlantılar oluşturmak için kullanılabilir, ancak varsayılan olarak tarayıcının HTML'yi yeniden yüklemesine neden olur. Yönlendirmeyi özel JavaScript ile işlerken bu davranışı önlemek için, tıklama olayında `preventDefault()` fonksiyonunu kullanmak gerekir.

### Görev

Uygulamamızda gezinmek için kullanabileceğimiz yeni bir fonksiyon oluşturalım:

```js
function navigate(path) {
  window.history.pushState({}, path, path);
  updateRoute();
}
```

Bu yöntem önce verilen yola göre mevcut URL'yi günceller, ardından şablonu günceller. `window.location.origin` özelliği, URL kökünü döndürerek, verilen bir yoldan tam bir URL'yi yeniden oluşturmamıza olanak tanır.

Artık bu fonksiyona sahip olduğumuza göre, bir yol herhangi bir tanımlı yönlendirmeyle eşleşmezse yaşadığımız sorunu ele alabiliriz. `updateRoute` fonksiyonunu, bir eşleşme bulamazsak mevcut yönlendirmelerden birine geri dönecek şekilde değiştireceğiz.

```js
function updateRoute() {
  const path = window.location.pathname;
  const route = routes[path];

  if (!route) {
    return navigate('/login');
  }

  ...
```

Bir yönlendirme bulunamazsa, artık `login` sayfasına yönlendirileceğiz.

Şimdi bir bağlantıya tıklandığında URL'yi almak ve tarayıcının varsayılan bağlantı davranışını önlemek için bir fonksiyon oluşturalım:

```js
function onLinkClick(event) {
  event.preventDefault();
  navigate(event.target.href);
}
```

Gezinme sistemini tamamlamak için HTML'deki *Giriş Yap* ve *Çıkış Yap* bağlantılarımıza bağlamalar ekleyelim.

```html
<a href="/dashboard" onclick="onLinkClick(event)">Login</a>
...
<a href="/login" onclick="onLinkClick(event)">Logout</a>
```

Yukarıdaki `event` nesnesi, `click` olayını yakalar ve `onLinkClick` fonksiyonumuza iletir.

[`onclick`](https://developer.mozilla.org/docs/Web/API/GlobalEventHandlers/onclick) özelliğini kullanarak `click` olayını JavaScript koduna bağlayın, burada `navigate()` fonksiyonunu çağırıyoruz.

Bu bağlantılara tıklamayı deneyin, artık uygulamanızın farklı ekranları arasında gezinmeniz mümkün olmalı.

✅ `history.pushState` yöntemi HTML5 standardının bir parçasıdır ve [tüm modern tarayıcılarda](https://caniuse.com/?search=pushState) uygulanmıştır. Daha eski tarayıcılar için bir web uygulaması oluşturuyorsanız, bu API yerine kullanabileceğiniz bir püf noktası vardır: bir yolun önüne bir [hash (`#`)](https://en.wikipedia.org/wiki/URI_fragment) ekleyerek, düzenli bağlantı gezintisiyle çalışan ve sayfayı yeniden yüklemeyen bir yönlendirme uygulayabilirsiniz. Bunun amacı, bir sayfa içinde dahili bağlantılar oluşturmaktır.

## Tarayıcının Geri ve İleri Düğmelerini Ele Alma

`history.pushState` kullanmak, tarayıcının gezinme geçmişinde yeni girişler oluşturur. Tarayıcınızın *geri düğmesini* basılı tutarak bunu kontrol edebilirsiniz, şöyle bir şey göstermesi gerekir:

![Gezinme geçmişi ekran görüntüsü](../../../../translated_images/history.7fdabbafa521e06455b738d3dafa3ff41d3071deae60ead8c7e0844b9ed987d8.tr.png)

Geri düğmesine birkaç kez tıklamayı denerseniz, mevcut URL'nin değiştiğini ve geçmişin güncellendiğini görürsünüz, ancak aynı şablon görüntülenmeye devam eder.

Bunun nedeni, uygulamanın her seferinde `updateRoute()` fonksiyonunu çağırmamız gerektiğini bilmemesidir. [`history.pushState` dokümantasyonuna](https://developer.mozilla.org/docs/Web/API/History/pushState) bakarsanız, durum değiştiğinde - yani farklı bir URL'ye geçtiğimizde - [`popstate`](https://developer.mozilla.org/docs/Web/API/Window/popstate_event) olayının tetiklendiğini görebilirsiniz. Bu sorunu çözmek için bunu kullanacağız.

### Görev

Tarayıcı geçmişi değiştiğinde görüntülenen şablonun güncellendiğinden emin olmak için, `updateRoute()` fonksiyonunu çağıran yeni bir fonksiyon ekleyeceğiz. Bunu `app.js` dosyanızın en altına ekleyeceğiz:

```js
window.onpopstate = () => updateRoute();
updateRoute();
```

> Not: Burada `popstate` olay işleyicimizi kısalık için bir [ok fonksiyonu](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/Arrow_functions) kullanarak tanımladık, ancak normal bir fonksiyon da aynı şekilde çalışır.

Ok fonksiyonları hakkında bir hatırlatma videosu:

[![Ok Fonksiyonları](https://img.youtube.com/vi/OP6eEbOj2sc/0.jpg)](https://youtube.com/watch?v=OP6eEbOj2sc "Ok Fonksiyonları")

> 🎥 Ok fonksiyonları hakkında bir video için yukarıdaki görsele tıklayın.

Şimdi tarayıcınızın geri ve ileri düğmelerini kullanmayı deneyin ve bu sefer görüntülenen yönlendirmenin doğru şekilde güncellenip güncellenmediğini kontrol edin.

---

## 🚀 Zorluk

Bu uygulama için kredileri gösteren üçüncü bir sayfa için yeni bir şablon ve yönlendirme ekleyin.

## Ders Sonrası Test

[Ders sonrası test](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/42)

## İnceleme ve Kendi Kendine Çalışma

Yönlendirme, web geliştirme sürecinin şaşırtıcı derecede zorlayıcı kısımlarından biridir, özellikle de web, sayfa yenileme davranışlarından Tek Sayfa Uygulaması (SPA) sayfa yenilemelerine geçerken. [Azure Static Web App hizmetinin](https://docs.microsoft.com/azure/static-web-apps/routes/?WT.mc_id=academic-77807-sagibbon) yönlendirmeleri nasıl ele aldığı hakkında biraz okuyun. Bu belgede açıklanan bazı kararların neden gerekli olduğunu açıklayabilir misiniz?

## Ödev

[Yönlendirmeyi geliştirin](assignment.md)

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalar için sorumluluk kabul etmiyoruz.