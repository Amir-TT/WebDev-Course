<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "b4612bbb9ace984f374fcc80e3e035ad",
  "translation_date": "2025-08-25T21:44:14+00:00",
  "source_file": "2-js-basics/2-functions-methods/README.md",
  "language_code": "tr"
}
-->
# JavaScript Temelleri: Metotlar ve Fonksiyonlar

![JavaScript Temelleri - Fonksiyonlar](../../../../translated_images/webdev101-js-functions.be049c4726e94f8b7605c36330ac42eeb5cd8ed02bcdd60fdac778174d6cb865.tr.png)
> Sketchnote: [Tomomi Imura](https://twitter.com/girlie_mac)

## Ders Öncesi Quiz
[Ders öncesi quiz](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/9)

Kod yazmayı düşündüğümüzde, her zaman kodumuzun okunabilir olmasını sağlamayı hedefleriz. Bu kulağa ters gelebilir, ancak kod yazıldığından çok daha fazla okunur. Geliştiricilerin sürdürülebilir kod yazmasını sağlayan temel araçlardan biri **fonksiyon**dur.

[![Metotlar ve Fonksiyonlar](https://img.youtube.com/vi/XgKsD6Zwvlc/0.jpg)](https://youtube.com/watch?v=XgKsD6Zwvlc "Metotlar ve Fonksiyonlar")

> 🎥 Metotlar ve fonksiyonlar hakkında bir video için yukarıdaki görsele tıklayın.

> Bu dersi [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101-functions/?WT.mc_id=academic-77807-sagibbon) üzerinden alabilirsiniz!

## Fonksiyonlar

Temel olarak, bir fonksiyon talep üzerine çalıştırabileceğimiz bir kod bloğudur. Bu, aynı görevi birden fazla kez gerçekleştirmemiz gereken senaryolar için mükemmeldir; mantığı birden fazla yerde çoğaltmak yerine (ki bu, güncelleme gerektiğinde zor olurdu), onu tek bir yerde merkezileştirebilir ve işlemi gerçekleştirmek istediğimizde çağırabiliriz - hatta bir fonksiyonu başka bir fonksiyondan çağırabilirsiniz!

Bir fonksiyona isim verebilmek de aynı derecede önemlidir. Bu önemsiz gibi görünebilir, ancak isim bir kod bölümünü hızlı bir şekilde belgelemek için bir yol sağlar. Bunu bir düğme üzerindeki etiket gibi düşünebilirsiniz. Eğer "Zamanlayıcıyı iptal et" yazan bir düğmeye tıklarsam, saati durduracağını bilirim.

## Bir fonksiyon oluşturma ve çağırma

Bir fonksiyonun sözdizimi şu şekilde görünür:

```javascript
function nameOfFunction() { // function definition
 // function definition/body
}
```

Bir selamlama mesajı göstermek için bir fonksiyon oluşturmak isteseydim, bu şöyle görünebilirdi:

```javascript
function displayGreeting() {
  console.log('Hello, world!');
}
```

Fonksiyonumuzu çağırmak (veya çalıştırmak) istediğimizde, fonksiyonun adını ve ardından `()` kullanırız. Fonksiyonun, çağrılmadan önce veya sonra tanımlanabileceğini belirtmekte fayda var; JavaScript derleyicisi onu sizin için bulacaktır.

```javascript
// calling our function
displayGreeting();
```

> **NOTE:** **Metot** olarak bilinen özel bir fonksiyon türü vardır ve bunu zaten kullanıyorsunuz! Aslında, yukarıdaki demoda `console.log` kullandığımızda bunu gördük. Bir metodu bir fonksiyondan ayıran şey, bir metodun bir nesneye (`console` örneğimizde olduğu gibi) bağlı olmasıdır, oysa bir fonksiyon serbesttir. Birçok geliştiricinin bu terimleri birbirinin yerine kullandığını duyacaksınız.

### Fonksiyonlar için en iyi uygulamalar

Fonksiyonlar oluştururken akılda tutulması gereken birkaç en iyi uygulama vardır:

- Her zaman olduğu gibi, fonksiyonun ne yapacağını anlamak için açıklayıcı isimler kullanın.
- Kelimeleri birleştirmek için **camelCasing** kullanın.
- Fonksiyonlarınızı belirli bir göreve odaklanmış tutun.

## Bir fonksiyona bilgi aktarma

Bir fonksiyonu daha yeniden kullanılabilir hale getirmek için genellikle ona bilgi aktarmak istersiniz. Yukarıdaki `displayGreeting` örneğimizi düşünürsek, yalnızca **Hello, world!** gösterecektir. Bu, oluşturulabilecek en kullanışlı fonksiyon değildir. Daha esnek hale getirmek, örneğin selamlanacak kişinin adını belirtmek istiyorsak, bir **parametre** ekleyebiliriz. Parametre (bazen **argüman** olarak da adlandırılır), bir fonksiyona gönderilen ek bilgidir.

Parametreler, tanım kısmında parantez içinde listelenir ve virgülle ayrılır:

```javascript
function name(param, param2, param3) {

}
```

`displayGreeting` fonksiyonumuzu bir isim kabul edecek ve bunu gösterecek şekilde güncelleyebiliriz.

```javascript
function displayGreeting(name) {
  const message = `Hello, ${name}!`;
  console.log(message);
}
```

Fonksiyonumuzu çağırmak ve parametreyi aktarmak istediğimizde, bunu parantez içinde belirtiriz.

```javascript
displayGreeting('Christopher');
// displays "Hello, Christopher!" when run
```

## Varsayılan değerler

Fonksiyonumuzu daha da esnek hale getirmek için daha fazla parametre ekleyebiliriz. Ancak her değerin belirtilmesini zorunlu kılmak istemiyorsak ne yaparız? Selamlama örneğimizle devam edersek, ismi gerekli bırakabiliriz (kimi selamladığımızı bilmemiz gerekiyor), ancak selamlamanın kendisinin isteğe bağlı olarak özelleştirilmesine izin vermek isteyebiliriz. Birisi bunu özelleştirmek istemezse, bunun yerine bir varsayılan değer sağlayabiliriz. Bir parametreye varsayılan bir değer sağlamak için, bir değişkene değer atadığımız gibi `parameterName = 'defaultValue'` şeklinde ayarlarız. Tam bir örnek görmek için:

```javascript
function displayGreeting(name, salutation='Hello') {
  console.log(`${salutation}, ${name}`);
}
```

Fonksiyonu çağırdığımızda, `salutation` için bir değer belirlemek isteyip istemediğimize karar verebiliriz.

```javascript
displayGreeting('Christopher');
// displays "Hello, Christopher"

displayGreeting('Christopher', 'Hi');
// displays "Hi, Christopher"
```

## Geri dönüş değerleri

Şimdiye kadar oluşturduğumuz fonksiyon her zaman [console](https://developer.mozilla.org/docs/Web/API/console)'a çıktı verecektir. Bazen bu tam olarak aradığımız şey olabilir, özellikle de diğer hizmetleri çağıracak fonksiyonlar oluşturduğumuzda. Ancak bir hesaplama yapmak ve değeri başka bir yerde kullanmak için geri döndürmek istediğim bir yardımcı fonksiyon oluşturmak istersem ne olur?

Bunu bir **geri dönüş değeri** kullanarak yapabiliriz. Bir geri dönüş değeri, fonksiyon tarafından döndürülür ve bir değişkende saklanabilir, tıpkı bir dize veya sayı gibi sabit bir değeri saklayabileceğimiz gibi.

Bir fonksiyon bir şey döndürecekse, `return` anahtar kelimesi kullanılır. `return` anahtar kelimesi, döndürülen şeyin bir değerini veya referansını bekler:

```javascript
return myVariable;
```  

Bir selamlama mesajı oluşturmak ve değeri çağırana geri döndürmek için bir fonksiyon oluşturabiliriz.

```javascript
function createGreetingMessage(name) {
  const message = `Hello, ${name}`;
  return message;
}
```

Bu fonksiyonu çağırdığımızda, değeri bir değişkende saklayacağız. Bu, sabit bir değeri bir değişkene atadığımız şekilde yapılır (örneğin, `const name = 'Christopher'`).

```javascript
const greetingMessage = createGreetingMessage('Christopher');
```

## Fonksiyonları fonksiyonlara parametre olarak geçirme

Programlama kariyerinizde ilerledikçe, parametre olarak fonksiyon kabul eden fonksiyonlarla karşılaşacaksınız. Bu harika numara, bir şeyin ne zaman gerçekleşeceğini veya tamamlanacağını bilmediğimiz, ancak buna yanıt olarak bir işlem gerçekleştirmemiz gerektiği durumlarda yaygın olarak kullanılır.

Bir örnek olarak, [setTimeout](https://developer.mozilla.org/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)'u düşünün. Bu, bir zamanlayıcı başlatır ve tamamlandığında kodu çalıştırır. Hangi kodu çalıştırmak istediğimizi ona söylememiz gerekir. Bu, bir fonksiyon için mükemmel bir iş gibi görünüyor!

Aşağıdaki kodu çalıştırırsanız, 3 saniye sonra **3 saniye geçti** mesajını göreceksiniz.

```javascript
function displayDone() {
  console.log('3 seconds has elapsed');
}
// timer value is in milliseconds
setTimeout(displayDone, 3000);
```

### İsimsiz fonksiyonlar

Oluşturduğumuz şeyi bir kez daha inceleyelim. Bir kez kullanılacak bir isimle bir fonksiyon oluşturuyoruz. Uygulamamız daha karmaşık hale geldikçe, yalnızca bir kez çağrılacak birçok fonksiyon oluşturduğumuzu görebiliriz. Bu ideal değildir. Görünüşe göre, her zaman bir isim vermemiz gerekmiyor!

Bir fonksiyonu parametre olarak geçirirken, önceden bir tane oluşturmayı atlayabilir ve bunun yerine parametrenin bir parçası olarak bir tane oluşturabiliriz. Aynı `function` anahtar kelimesini kullanırız, ancak bunu bir parametre olarak oluştururuz.

Yukarıdaki kodu bir isimsiz fonksiyon kullanacak şekilde yeniden yazalım:

```javascript
setTimeout(function() {
  console.log('3 seconds has elapsed');
}, 3000);
```

Yeni kodumuzu çalıştırırsanız, aynı sonuçları elde ettiğimizi fark edeceksiniz. Bir fonksiyon oluşturduk, ancak ona bir isim vermemiz gerekmedi!

### Fat arrow fonksiyonları

Birçok programlama dilinde (JavaScript dahil) yaygın olan bir kısayol, **ok** veya **fat arrow** fonksiyonu olarak adlandırılan bir özelliği kullanma yeteneğidir. Bu, bir ok gibi görünen özel bir `=>` göstergesi kullanır - bu yüzden bu isim verilmiştir! `=>` kullanarak, `function` anahtar kelimesini atlayabiliriz.

Kodumuzu bir kez daha bir fat arrow fonksiyonu kullanacak şekilde yeniden yazalım:

```javascript
setTimeout(() => {
  console.log('3 seconds has elapsed');
}, 3000);
```

### Hangi stratejiyi ne zaman kullanmalı

Artık bir fonksiyonu parametre olarak geçmek için üç yol gördünüz ve her birini ne zaman kullanmanız gerektiğini merak ediyor olabilirsiniz. Fonksiyonu birden fazla kez kullanacağınızı biliyorsanız, onu normal şekilde oluşturun. Sadece bir yerde kullanacaksanız, genellikle bir isimsiz fonksiyon kullanmak en iyisidir. Fat arrow fonksiyonu mu yoksa daha geleneksel `function` sözdizimini mi kullanacağınız size kalmış, ancak çoğu modern geliştiricinin `=>` tercih ettiğini fark edeceksiniz.

---

## 🚀 Meydan Okuma

Fonksiyonlar ve metotlar arasındaki farkı bir cümleyle açıklayabilir misiniz? Bir deneyin!

## Ders Sonrası Quiz
[Ders sonrası quiz](https://ashy-river-0debb7803.1.azurestaticapps.net/quiz/10)

## Gözden Geçirme ve Kendi Kendine Çalışma

[Ok fonksiyonları hakkında biraz daha okumaya](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Functions/Arrow_functions) değer, çünkü bunlar kod tabanlarında giderek daha fazla kullanılmaktadır. Bir fonksiyon yazmayı ve ardından bu sözdizimiyle yeniden yazmayı deneyin.

## Ödev

[Fonksiyonlarla Eğlence](assignment.md)

**Feragatname**:  
Bu belge, AI çeviri hizmeti [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba göstersek de, otomatik çevirilerin hata veya yanlışlık içerebileceğini lütfen unutmayın. Belgenin orijinal dili, yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımından kaynaklanan yanlış anlamalar veya yanlış yorumlamalar için sorumluluk kabul etmiyoruz.