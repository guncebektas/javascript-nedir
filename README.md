Bu ders temel programlama bilgisine sahip kişilerin Javascript öğrenerek, Javascript ile temiz kod yazabilmesini sağlamak amacıyla hazırlanmıştır.

# 1. Giriş

## JavaScript Nedir?

JavaScript, web tarayıcılarında çalışan bir programlama dilidir. Hem tarayıcı tarafında (client-side) hem de sunucu tarafında (server-side) kullanılabilir.

## Neden Clean Code Önemlidir?

Clean Code, kodun okunabilirliği, bakımı ve uzun ömürlülüğü için hayati öneme sahiptir. Temiz kod, hata ayıklamayı kolaylaştırır ve kod tabanını sürdürülebilir hale getirir.

# 2. Temel Syntax

## Integer, String... Object, JSON, EJSON, BJSON

Object (Nesne): JavaScript'te ve diğer bazı programlama dillerinde, bir nesne (object), özellik ve değerlerin birleşimi olarak tanımlanan bir veri yapısıdır. Nesneler, özelliklerin anahtar-değer çiftleri şeklinde bulunduğu ve genellikle işlevlerin de dahil olduğu karmaşık veri yapılarıdır.

JSON (JavaScript Object Notation): JSON, insanlar tarafından okunabilir ve yazılabilir bir veri değişim formatıdır. JSON, JavaScript nesne literal formatından türetilmiştir ve veriyi temsil etmek için anahtar-değer çiftleri kullanır. JSON, programlama dilleri arasında veri alışverişi yapmak için yaygın olarak kullanılır.

```json
{
  "name": "John Doe",
  "age": 30,
  "isStudent": false,
  "address": {
    "street": "123 Main St",
    "city": "New York"
  },
  "languages": [
    "JavaScript",
    "Python",
    "Java"
  ]
}
```

EJSON (Extended JSON): EJSON, JSON formatına ek olarak, JavaScript'te kullanılan veri türlerini ve özelliklerini temsil etmek için geliştirilmiş bir formattır. EJSON, JavaScript nesnelerini, tarihleri, özel türleri ve diğer türleri JSON ile uyumlu bir şekilde temsil etmeyi sağlar.

```json
{
  "_id": {
    "$oid": "5f88387d645e9a3f35a61de3"
  },
  "name": "Alice",
  "age": {
    "$numberInt": "30"
  },
  "isStudent": {
    "$boolean": "false"
  },
  "address": {
    "street": "123 Main St",
    "city": "New York"
  },
  "languages": {
    "$array": [
      "JavaScript",
      "Python",
      "Java"
    ]
  }
}
```

BJSON (Binary JSON): BJSON, JSON formatının bir tür genişletilmiş sürümüdür ve verileri binary (ikili) formatta temsil eder. JSON formatının avantajlarını korurken, veriyi daha kompakt bir şekilde saklamak ve işlemek için kullanılır. Böylece, ağırlık ve hız açısından performans avantajları sağlar.

```bjson
BJSON: <binary data representing the JSON structure>
```

Bu formatlar, verilerin belirli bir yapıda ve formatta temsil edilmesini, saklanmasını ve iletilmesini sağlamak için kullanılır. JSON, genellikle web uygulamalarında ve veri alışverişlerinde kullanılan popüler bir formatken, EJSON ve BJSON gibi formatlar ise belirli gereksinimlere uygun olarak kullanılır. Nesneler ise programlama dillerinde genel bir veri yapısıdır ve birçok farklı bağlamda kullanılırlar.

## Değişkenler: `var`, `let`, `const`

JavaScript'te değişkenler, değerleri saklamak için kullanılır. `var`, `let`, ve `const` anahtar kelimeleri kullanılarak değişkenler tanımlanır.

```javascript
let sayi = 42;
const PI = 3.14;
var isim = "John Doe";
```

### Context

- Global Bağlam (Global Context):
  Eğer bir fonksiyon global bağlamda çağrılırsa, this global nesneyi temsil eder.

```javascript
console.log(this); // Global nesne (tarayıcılarda window) yazdırılır
```

- Fonksiyon Bağlamı (Function Context):
  Eğer bir fonksiyon bir nesne içinde bir metot olarak çağrılırsa, this o nesneyi temsil eder.

```javascript
const obj = {
  name: "John",
  sayHello: function () {
    console.log("Hello, " + this.name);
  }
};
obj.sayHello(); // "Hello, John" yazdırılır

```

- Constructor Bağlamı (Constructor Context):
  Eğer bir fonksiyon bir constructor olarak kullanılırsa (örneğin, bir sınıfın constructor metodu), this yeni oluşturulan nesneyi temsil eder.

```javascript
function Person(name) {
  this.name = name;
}

const person1 = new Person("Alice");
console.log(person1.name); // "Alice" yazdırılır
```

### Değişken Kapsamı (Variable Scope)

- **var:** Fonksiyon kapsamında (function scope) tanımlanır. Blok içinde tanımlanmış olsa bile, yalnızca fonksiyon içinde erişilebilir.
- **let ve const:** Blok kapsamında (block scope) tanımlanır. Sadece tanımlandığı blok içinde erişilebilir.

```javascript
function exampleFunction() {
  if (true) {
    let localVar = "Bu, if bloğu içinde tanımlanmış bir değişkendir.";
    console.log(localVar); // Bu değişkene buradan erişebiliriz
  }
  console.log(localVar); // Hata! localVar burada tanımlı değil
}
```

# 3. Kontrol Yapıları

## If-Else Yapısı

If-Else yapısı, belirli bir koşulun doğru veya yanlış olmasına bağlı olarak farklı kod bloklarının çalıştırılmasını sağlar.

```javascript
const sayi = 10;
if (sayi > 0) {
  console.log("Sayı pozitif");
} else {
  console.log("Sayı negatif veya sıfır");
}
```

## Switch-Case Yapısı

Switch-Case yapısı, bir değişkenin değerine göre farklı durumların işlenmesini sağlar.

```javascript
const meyve = "elma";
switch (meyve) {
  case "elma":
    console.log("Elma seçildi");
    break;
  case "armut":
    console.log("Armut seçildi");
    break;
  default:
    console.log("Geçersiz meyve");
    break;
}
```

# 4. Döngüler

## For

For döngüsü, belirli bir başlangıç noktasından başlayarak belirtilen koşulu sağlayana kadar döngüyü çalıştırır.

```javascript
for (let i = 0; i < 5; i++) {
  console.log("Döngü adımı: " + i);
}
```

## Do-while

```javascript
let x = 0;
do {
  console.log("x değeri: " + x);
  x++;
} while (x < 5);
```

## forEach ve for...of Döngüleri

forEach ve for...of döngüleri, dizilerdeki her öğeyi ziyaret etmek için kullanılır.

### forEach döngüsü örneği:

```javascript
const dizi = [1, 2, 3, 4, 5];
dizi.forEach(function (eleman) {
  console.log(eleman);
});
```

### for...of döngüsü örneği:

```javascript
const dizi = [1, 2, 3, 4, 5];
for (let eleman of dizi) {
  console.log(eleman);
}
```

Elbette, işte 5. slaytın Markdown formatında oluşturulmuş hali:

# 5. Fonksiyonlar ```f(x) = y```

## Fonksiyon Tanımlama

JavaScript'te fonksiyonlar, belirli bir işlevi gerçekleştiren bir dizi ifadeyi içeren bir kod bloğudur. Fonksiyonlar, `function` anahtar kelimesi ile tanımlanır.

```javascript
function sayHello() {
  console.log("Merhaba!");
}
```

## Parametreler ve Argümanlar

Fonksiyonlara parametreler (parameters) geçirilebilir. Parametreler, fonksiyonun içinde belirtilen değişkenlerdir. Fonksiyon çağrılırken bu parametrelere argümanlar (arguments) verilir.

```javascript
function greet(name) {
  console.log("Merhaba, " + name + "!");
}

greet("Alice"); // "Merhaba, Alice!" yazdırılır
```

## Geri Dönüş Değeri

Fonksiyonlar bir değer döndürebilir. `return` ifadesi ile belirtilen değer fonksiyon tarafından döndürülür.

```javascript
function multiply(a, b) {
  return a * b;
}

const sonuc = multiply(3, 4); // sonuc değeri: 12
```

Elbette, işte 6. slaytın Markdown formatında oluşturulmuş hali:

# 6. Diziler ve Nesneler

## Dizi Tanımlama ve Kullanımı

Diziler, sıralı veri koleksiyonlarını temsil eder. Elemanlara ulaşmak için indeks kullanılır.

```javascript
const dizi = [1, 2, 3, 4, 5];
console.log(dizi[0]); // İlk eleman: 1
```

## Nesne Tanımlama ve Kullanımı

Nesneler, anahtar-değer çiftlerini temsil eder ve karmaşık veri yapıları oluşturmak için kullanılır.

```javascript
const personel = {
  ad: "John",
  soyad: "Doe",
  yas: 30
};
console.log(personel.ad); // "John" yazdırılır
```

Diziler ve nesneler, JavaScript'te verileri düzenlemek ve erişmek için önemli veri yapılarıdır.

# 7. DOM Manipülasyonu ve Virtual DOM

## DOM Nedir?

DOM (Document Object Model), bir HTML belgesini temsil eden bir nesne ağacıdır. JavaScript, DOM'a erişerek sayfadaki içeriği değiştirebilir ve güncelleyebilir.

## Element Seçimi ve Değişiklikleri

JavaScript kullanarak DOM'dan elemanları seçebilir ve özelliklerini değiştirebiliriz.

```javascript
// Bir elementi seçme
const element = document.getElementById("myElementId");

// Bir elementin içeriğini değiştirme
element.innerHTML = "Yeni içerik";

// Bir elementin stilini değiştirme
element.style.color = "red";
```

```javascript
// Bir elementi seçme
const element = $("#myElementId");

// Bir elementin içeriğini değiştirme
element.html("Yeni içerik");

// Bir elementin stilini değiştirme
element.css("color", "red");

```

## Virtual DOM ve Performans

Virtual DOM, gerçek DOM yapısının hafızada bir temsilidir ve React gibi kütüphaneler tarafından kullanılır. Bu, DOM manipülasyonlarının daha etkili ve performanslı bir şekilde gerçekleştirilmesini sağlar.

React'te bir bileşenin güncellenmesi, Virtual DOM üzerinde gerçekleşir. Değişiklikler daha önce oluşturulan Virtual DOM ile karşılaştırılır ve sadece farklılıklar gerçek DOM'a uygulanır. Bu, gereksiz güncellemelerin önlenmesine ve uygulamanın daha hızlı çalışmasına yardımcı olur.

# 8. Modüler Programlama

## Modüler Programlama Nedir?

Modüler programlama, bir programı bağımsız, birbiriyle ilişkili parçalara (modüller) bölmeyi ve bu parçaları geliştirmeyi kolaylaştıran bir programlama yaklaşımıdır.

## Faydaları

- **Daha Düzenli Kod:** Kodu modüller halinde organize etmek, kodun daha düzenli ve anlaşılır olmasını sağlar.
- **Tekrar Kullanım:** Modüller, farklı projelerde veya farklı kısımlarda tekrar kullanılabilir.
- **Kolay Bakım:** Modüler yapı, kodun bakımını ve güncellemelerini kolaylaştırır.

## Modüler Programlama Örneği (ES6 Modules)

ES6 (ECMAScript 2015) ile birlikte JavaScript, modüler programlamayı desteklemeye başladı. Modüller, bağımsız dosyalarda tanımlanır ve diğer dosyalardan içe aktarılabilir.

Örnek modül (utils.js):

```javascript
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}
```

Modülün kullanımı:

```javascript
import {add, subtract} from './utils.js';

console.log(add(5, 3)); // 8
console.log(subtract(10, 4)); // 6
```

# 9. Hata Yakalama (Error Handling)

## Hata Yakalama Nedir?

Hata yakalama, bir programın çalışması sırasında ortaya çıkan hataları kontrol etmek ve ele almak için kullanılan bir programlama kavramıdır. Bu, programın daha güvenilir ve hata toleranslı olmasını sağlar.

## Try-Catch Blokları

`try` ve `catch` blokları, potansiyel hata yaratabilecek kodları çevreler. Eğer bir hata oluşursa, bu bloklar çalışır ve hata ele alınır.

```javascript
try {
  // Hata yaratabilecek kodlar burada
  const result = 10 / 0;
} catch (error) {
  // Hata ele alındığında burası çalışır
  console.error("Hata oluştu: " + error.message);
}
```

## Try-Catch-Finally

finally bloğu, hata olsun ya da olmasın çalışmasını istediğiniz kodları içerir.

```javascript
try {
  // Hata yaratabilecek kodlar burada
  const result = 10 / 0;
} catch (error) {
  // Hata ele alındığında burası çalışır
  console.error("Hata oluştu: " + error.message);
} finally {
  // Her durumda çalışmasını istediğiniz kodlar burada
  console.log("İşlem tamamlandı.");
}
```

# 10. Asenkron Programlama

## Asenkron Programlama Nedir?

Asenkron programlama, programın belirli işlemleri eşzamanlı olarak yürütmesini sağlayan bir programlama yaklaşımıdır. Bu, özellikle giriş/çıkış işlemlerinde (network çağrıları, dosya okuma/yazma vb.) ve zaman alıcı işlemlerde yaygın olarak kullanılır.

## Callback Fonksiyonları

Callback fonksiyonları, bir işlem tamamlandığında çalıştırılacak olan fonksiyonlardır. Bu, asenkron işlemlerin sonucunu ele almak için kullanılır.

```javascript
function fetchData(url, callback) {
  // Asenkron işlemi simüle et
  setTimeout(() => {
    const data = "Veri alındı!";
    callback(data);
  }, 2000);
}

function displayData(data) {
  console.log("Veri gösteriliyor: " + data);
}

fetchData("https://example.com/api", displayData);
```

## Promise

Promise, asenkron işlemleri daha etkili bir şekilde ele almak için kullanılır. Bir işlemin başarılı olup olmadığını temsil eden bir nesnedir.

```javascript
function fetchData(url) {
  return new Promise((resolve, reject) => {
    // Asenkron işlemi simüle et
    setTimeout(() => {
      const success = true;
      if (success) {
        const data = "Veri alındı!";
        resolve(data);
      } else {
        reject("Veri alınamadı.");
      }
    }, 2000);
  });
}

fetchData("https://example.com/api")
.then((data) => console.log("Veri gösteriliyor: " + data))
.catch((error) => console.error("Hata: " + error));
```

## Async/Await

async ve await, Promise tabanlı asenkron kodu daha okunabilir ve yönetilebilir hale getiren ES8 özellikleridir.

```javascript
async function fetchData(url) {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    throw new Error("Veri alınamadı.");
  }
}

async function displayData() {
  try {
    const data = await fetchData("https://example.com/api");
    console.log("Veri gösteriliyor: ", data);
  } catch (error) {
    console.error("Hata: " + error.message);
  }
}

displayData();
```

# 11. Web API'leri ve AJAX

## Web API Nedir?

Web API (Web Application Programming Interface), uygulamaların belirli işlevleri kullanarak birbiriyle iletişim kurmasını sağlayan bir arayüzdür. Bu, genellikle sunucudan veri almak veya sunucuya veri göndermek için kullanılır.

## AJAX Nedir?

AJAX (Asynchronous JavaScript and XML), tarayıcı tabanlı asenkron iletişim için kullanılan bir tekniktir. Bu, sayfanın yeniden yüklenmeden belirli içeriğin güncellenmesine ve sunucu ile veri alışverişine olanak tanır.

## AJAX Kullanımı

AJAX, JavaScript kullanarak sunucuyla veri alışverişi yapmak için kullanılır. Örneğin, bir HTTP isteği göndermek ve sunucudan gelen veriyi işlemek için kullanılabilir.

```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", "https://api.example.com/data", true);

xhr.onload = function () {
  if (xhr.status === 200) {
    const responseData = JSON.parse(xhr.responseText);
    console.log("Sunucudan gelen veri: ", responseData);
  } else {
    console.error("Hata: ", xhr.statusText);
  }
};

xhr.send();
```

## AJAX Kullanımı (jQuery)

AJAX, jQuery kütüphanesi ile de kolayca kullanılabilir. jQuery, AJAX isteklerini basitleştirir ve tarayıcı uyumluluğu sağlar.

```javascript
$.ajax({
  url: "https://api.example.com/data",
  method: "GET",
  dataType: "json",
  success: function (data) {
    console.log("Sunucudan gelen veri: ", data);
  },
  error: function (xhr, status, error) {
    console.error("Hata: ", error);
  }
});
```

## AJAX Kullanımı (axios.js)

React.js, Vue.js gibi modern bir JavaScript framework'ünde AJAX istekleri fetch ya da Axios adında popüler kütüphanelerle kolayca yapılabilir, bu tip kütüphaneler HTTP istekleri yapmayı kolaylaştırır ve tarayıcı uyumluluğu sağlar.

```javascript
// Öncelikle Axios kütüphanesini projeye dahil et
// npm install axios
import axios from 'axios';

// API'den veri çekme
axios.get('https://api.example.com/data')
.then(response => {
  console.log('Sunucudan gelen veri: ', response.data);
})
.catch(error => {
  console.error('Hata: ', error);
});
```

# 12. Single Page Applications (SPA)

## Single Page Applications (SPA) Nedir?

Single Page Application (Tek Sayfa Uygulaması), bir web uygulamasının yalnızca bir HTML dosyasını yükleyerek çalıştığı, dinamik ve etkileşimli bir kullanıcı deneyimi sunan uygulamalardır.

## Avantajları

- **Hızlı Yükleme:** İlk yükleme sonrasında sayfa yeniden yüklenmez, sadece içerik güncellenir.
- **Daha İyi Kullanıcı Deneyimi:** Sayfa geçişleri daha hızlı ve akıcıdır.
- **Verimli:** Tek sayfa üzerinde çalıştığı için sunucudan daha az veri alınır.

## Tek Sayfa Uygulaması Örneği

Meteor.js, Vue.js, React, Angular gibi modern JavaScript framework'leri ile SPA geliştirilebilir. Bu framework'ler sayesinde tek sayfa uygulamaları geliştirmek daha kolay ve verimli hale gelir.

Örneğin, Vue.js ile basit bir tek sayfa uygulaması:

```html

<div id="app">
  <router-view></router-view>
</div>

<script>
  const Home = {template: '<div>Ana Sayfa</div>'};
  const About = {template: '<div>Hakkımızda Sayfası</div>'};

  const router = new VueRouter({
    routes: [
      {path: '/', component: Home},
      {path: '/about', component: About}
    ]
  });

  new Vue({
    router,
    el: '#app'
  });
</script>
```

## Tek Sayfa Uygulaması Örneği (Meteor ve Blaze)

Meteor, bir platform ve Blaze ise bir şablon motorudur. Bu teknolojilerle basit bir tek sayfa uygulaması oluşturalım.

```html

<head>
  <title>Meteor Blaze SPA</title>
</head>

<body>
<h1>{{title}}</h1>
<button id="changeTitle">Başlığı Değiştir</button>
</body>
```

```javascript
import {Template} from 'meteor/templating';

import './main.html';

Template.body.helpers({
  title: 'Merhaba, Meteor ve Blaze!'
});

Template.body.events({
  'click #changeTitle'() {
    Template.instance().$("h1").text("Yeni Başlık");
  }
});
```

# 13. Temiz Kodlama Prensipleri (Clean Code)

## SOLID Prensipleri

### 1. Tek Sorumluluk Prensibi (Single Responsibility Principle - SRP)
Bir sınıfın sadece bir nedeni olmalı ve bu neden doğrultusunda değişmelidir. Bir sınıfın işlevselliği tek bir sorumlulukla sınırlı olmalıdır.

### 2. Açık/Kapalı Prensibi (Open/Closed Principle - OCP)
Yazılım varlıkları (sınıflar, modüller, fonksiyonlar vb.), değişikliklere kapalı ancak uzantılara açık olmalıdır. Yeni işlevselliği eklemek, mevcut kodu değiştirmeden mümkün olmalıdır.

### 3. Liskov Yerine Koyma Prensibi (Liskov Substitution Principle - LSP)
Bir türetilmiş sınıf, onun temel sınıfının yerine geçebilmelidir. Bu, türetilmiş sınıfların, temel sınıfın davranışlarını değiştirmeden kullanılabilir olması gerektiği anlamına gelir.

### 4. Arayüz Ayrımı Prensibi (Interface Segregation Principle - ISP)
Müşterilerin ihtiyaç duymadığı işlevselliği içeren büyük arayüzler yerine, özel ihtiyaçlara yönelik daha küçük ve özgün arayüzler oluşturun. Bir sınıfın kullanmadığı metotlara bağımlı olmamalıdır.

### 5. Bağımlılıkların Tersine Çevrilmesi Prensibi (Dependency Inversion Principle - DIP)
Yüksek seviyeli modüller, düşük seviyeli modüllere bağımlı olmamalıdır. İki seviye de soyutlamalara bağımlı olmalıdır. Yani, detaylara karşı yüksek seviyeli modül bağımlı olmamalıdır.


## Temiz Kodlama Nedir?

Temiz kodlama, yazılım geliştirme sürecinde okunabilir, anlaşılabilir ve sürdürülebilir kod üretmek için prensiplere dayalı bir yaklaşımdır. Temiz kod, sadece bilgisayarlar tarafından değil, aynı zamanda diğer yazılımcılar tarafından da anlaşılabilir olmalıdır.

![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](https://www.osnews.com/images/comics/wtfm.jpg)

## Temiz Kodlamanın Önemi

- Daha okunabilir ve anlaşılabilir kod.
- Kodun sürdürülebilirliğini artırır.
- Hataları daha kolay bulma ve düzeltme.
- Kod tekrarını azaltır.
- Takım çalışmasını kolaylaştırır.

## Temiz Kodlama Prensipleri

1. **Kodun Anlaşılabilirliği**: Kodun açık, basit ve anlaşılır olmalıdır.
2. **İsimlendirme Uygunluğu**: Değişkenler, fonksiyonlar ve sınıflar anlamlı ve açıklayıcı isimlere sahip olmalıdır.
3. **Fonksiyon Boyutu**: Her fonksiyon sadece bir işi yapmalı ve küçük olmalıdır.
4. **Tek Sorumluluk Prensibi (Single Responsibility Principle)**: Bir sınıf sadece bir işlevi yerine getirmelidir.
5. **Düzeyli Yapı (Indentation)**: Kod düzgün bir şekilde girintilenmelidir.
6. **Kod Tekrarının Önlenmesi (DRY - Don't Repeat Yourself)**: Kodun içinde tekrar eden yapılar olmamalı, ortak kod parçaları ayrı bir yerde tutulmalıdır.
7. **Yorumlar ve Belgeler**: Kodda gerekliyse açıklayıcı yorumlar ve belgeler bulunmalıdır.

## Temiz Kodlama Örnekleri

### İsimlendirme
Kötü:
```javascript
const yyyymmdstr = moment().format("YYYY/MM/DD");
```
İyi:
```javascript
const currentDate = moment().format("YYYY/MM/DD");
```
------
Kötü:
```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```
İyi:
```javascript
getUser();
```
------
Kötü:
```javascript
// 86400000 ne...?
setTimeout(blastOff, 86400000);
```
İyi:
```javascript
// Aaaa 1 günmüş
const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;
setTimeout(blastOff, MILLISECONDS_PER_DAY);
```
------
Kötü:
```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Upss `l` neydi?
  dispatch(l);
});
```
İyi:
```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(location => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```
------
Kötü:
```javascript
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue"
};

function paintCar(car, color) {
  car.carColor = color;
}
```
İyi:
```javascript
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue"
};

function paintCar(car, color) {
  car.color = color;
}
```

### Fonksiyonlar
Fonksiyon parametrelerinin sayısını sınırlamak son derece önemlidir çünkü bu, fonksiyonunuzu test etmeyi daha kolay hale getirir. Üçten fazlasına sahip olmak, her bir ayrı argümanla onlarca farklı durumu test etmek zorunda olduğunuz bir karmaşıklığa yol açar.

#### Fonksiyonlar tek bir iş yapmalıdır
Bu, yazılım mühendisliğindeki en önemli kuraldır. Fonksiyonlar birden fazla iş yaptığında, birleştirmek, test etmek ve anlamak daha zor olurlar. Bir fonksiyonu sadece bir eyleme izole edebildiğinizde, bu fonksiyonu kolayca yeniden yapılandırabilir ve kodunuz çok daha temiz okunur. 

> Bu dersten öğrendiğiniz tek şey bu kural olsaydı, birçok geliştiriciden önde olacaksınız.

İki parametreden fazlasına sahip olan fonksiyon çok fazla iş yapıyor demektir.

Tek bir parametre alması o fonksiyonu kusursuz yapmaz. Örneğin;

Kötü:
```javascript
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```
İyi:
```javascript
function emailActiveClients(clients) {
  clients.filter(isActiveClient).forEach(email);
}

function isActiveClient(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```
Kötü olarak yazılmış fonksiyon tek parametre almasına rağmen birden fazla iş yapmaktadır.

Kötü:
```javascript
function addToDate(date, month) {
  // ...
}

const date = new Date();

// Ne yaptığını anlamak imkansız
addToDate(date, 1);
```
İyi:
```javascript
function addMonthToDate(month, date) {
  // ...
}

const date = new Date();
addMonthToDate(1, date);
```

#### Fonskiyonlar Boolean Parametre Almamalıdır
Kötü:
```javascript
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```
İyi:
```javascript
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```

### Kopyalanmış Koddan Kaçılınılmalıdır
Buraya bir PR yapıp git konusunda öğrendiklerini pekiştirebilirsin.

### Global'lerden Kaçınılmalıdır
Kötü:
```javascript
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};
```
İyi:
```javascript
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}
```

### Optimizasyon İyidir, Fazlası Kötüdür

### Kullanılmayan Kodlar Silinmelidir

### Class Kullanmak Tercih Edilmelidir
Kötü:
```javascript
const Animal = function(age) {
  if (!(this instanceof Animal)) {
    throw new Error("Instantiate Animal with `new`");
  }

  this.age = age;
};

Animal.prototype.move = function move() {};

const Mammal = function(age, furColor) {
  if (!(this instanceof Mammal)) {
    throw new Error("Instantiate Mammal with `new`");
  }

  Animal.call(this, age);
  this.furColor = furColor;
};

Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;
Mammal.prototype.liveBirth = function liveBirth() {};

const Human = function(age, furColor, languageSpoken) {
  if (!(this instanceof Human)) {
    throw new Error("Instantiate Human with `new`");
  }

  Mammal.call(this, age, furColor);
  this.languageSpoken = languageSpoken;
};

Human.prototype = Object.create(Mammal.prototype);
Human.prototype.constructor = Human;
Human.prototype.speak = function speak() {};
```
İyi:
```javascript
class Animal {
  constructor(age) {
    this.age = age;
  }

  move() {
    /* ... */
  }
}

class Mammal extends Animal {
  constructor(age, furColor) {
    super(age);
    this.furColor = furColor;
  }

  liveBirth() {
    /* ... */
  }
}

class Human extends Mammal {
  constructor(age, furColor, languageSpoken) {
    super(age, furColor);
    this.languageSpoken = languageSpoken;
  }

  speak() {
    /* ... */
  }
}
```


### Akıcı Desenler (Chaining) Kullanmak Tercih Edilmelidir
Kötü:
```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
  }

  setModel(model) {
    this.model = model;
  }

  setColor(color) {
    this.color = color;
  }

  save() {
    console.log(this.make, this.model, this.color);
  }
}

const car = new Car("Ford", "F-150", "red");
car.setColor("pink");
car.save();
```
İyi:
```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
    // NOTE: Returning this for chaining
    return this;
  }

  setModel(model) {
    this.model = model;
    // NOTE: Returning this for chaining
    return this;
  }

  setColor(color) {
    this.color = color;
    // NOTE: Returning this for chaining
    return this;
  }

  save() {
    console.log(this.make, this.model, this.color);
    // NOTE: Returning this for chaining
    return this;
  }
}

const car = new Car("Ford", "F-150", "red").setColor("pink").save();
```
# 14. Dökümantasyon ve Yorumlar

## Kod Dökümantasyonu

- Kodunuzun ne yaptığını, niçin yaptığını ve nasıl çalıştığını açıklayan belgelerdir.
- Kodun okunabilirliğini artırır ve gelecekteki geliştiricilere rehberlik eder.
- İyi dökümantasyon, projenin sürdürülebilirliğini ve büyüklüğünü artırır.

## Dökümantasyon İlkeleri

- **Açıklamalar**: Kodun içeriği ve işlevi hakkında bilgi vermelidir.
- **Fonksiyonlar ve Metodlar**: Ne iş yaptıklarını, aldıkları parametreleri ve döndürdükleri değerleri belirtmelidir.
- **Değişkenler**: Kullanım amacını ve ne tür verileri temsil ettiğini açıklamalıdır.
- **Kod Blokları**: Karmaşık veya önemli kod blokları hakkında bilgi sağlamalıdır.

## Yorumlar

- **Kod İçi Yorumlar**: Belirli bir satır veya blok için açıklamalar ekler.
- **TODO Etiketleri**: Henüz tamamlanmamış işleri veya gelecekteki iyileştirmeleri işaretler.
- **FIXME Etiketleri**: Hızlıca düzeltilmesi gereken hataları veya eksiklikleri işaretler.
- **XXX Etiketleri**: Dikkatle incelenmesi veya gözden geçirilmesi gereken noktaları işaretler.
- **İsimlendirme İle İfade Etme**: Kodunuzu açık ve anlaşılır şekilde yazarak aşırı yorumlardan kaçının.

## İyi Uygulamalar

- **Düzenli Güncelleme**: Kodunuzu değiştirdiğinizde dökümantasyonu da güncelleyin.
- **Açıklayıcı İsimler**: Anlamlı değişken, fonksiyon ve metod isimleri kullanarak dökümantasyonu azaltın.
- **Belgeleme Aracı Kullanımı**: Otomatik belge oluşturma araçları ile süreci kolaylaştırın.

> Eğer kodunuzu temiz yazarsanız dökümantasyonunuzu daha sade tutabilirsiniz.

## jsDoc Kullanımı
```javascript
/**
 * Bu fonksiyon, verilen iki sayıyı toplayarak sonucu döndürür.
 *
 * @param {number} a - Toplama işlemi için birinci sayı.
 * @param {number} b - Toplama işlemi için ikinci sayı.
 * @returns {number} İki sayının toplamı.
 * @throws {Error} Eğer herhangi bir parametre bir sayı değilse veya eksikse hata fırlatılır.
 */
export function addNumbers(a, b) {
  if (typeof a !== 'number' || typeof b !== 'number') {
    throw new Error('Her iki parametre de sayı olmalıdır.');
  }

  return a + b;
}
```


# 15. Test Yazma ve Otomasyon

## Test Yazmanın Önemi

- Kodun doğru çalıştığından emin olmak için önemlidir.
- Kodun değiştirilmesi veya güncellenmesi sırasında mevcut işlevselliğin bozulmadığını kontrol etmek için kullanılır.
- Hata ayıklamayı kolaylaştırır ve güven duygusu sağlar.

## Test Türleri

- **Birim Testleri**: Kodun en küçük parçalarını (fonksiyonlar, metodlar) test etmek için kullanılır.
- **Entegrasyon Testleri**: Farklı parçaların bir araya gelip uygun şekilde çalışıp çalışmadığını kontrol etmek için kullanılır.
- **Kabul Testleri**: Kullanıcının bakış açısından sistemin doğru çalışıp çalışmadığını doğrulamak için kullanılır.

## Test Otomasyonu

- Manuel test süreçlerini otomasyon araçları kullanarak tekrarlanabilir ve verimli hale getirir.
- Sürekli entegrasyon ve sürekli dağıtım süreçlerini destekler.
- Kodun kalitesini artırır ve hızlı geri bildirim sağlar.

## Popüler Test Çerçeveleri

- **Jest**: JavaScript uygulamaları için yaygın olarak kullanılan bir test çerçevesidir.
- **Mocha**: Esnek ve basit bir test çerçevesidir, farklı assert kütüphaneleriyle uyumlu çalışabilir.
- **Selenium**: Web uygulamalarını test etmek için kullanılan bir otomasyon aracıdır.

## İyi Uygulamalar

- **Kodla Birlikte Test Yazma**: Kodunuzu yazarken aynı zamanda testlerinizi de oluşturun.
- **Kapsayıcı ve Anlamlı Testler**: Tüm senaryoları kapsayan ve anlamlı isimlendirilmiş testler yazın.
- **Sürekli Entegrasyon (CI) ve Sürekli Dağıtım (CD)**: Otomatik testlerle entegrasyon ve dağıtım süreçlerini kurun.

```javascript
const addNumbers = require('./addNumbers');

test('İki sayının toplamı doğru hesaplanmalı', () => {
  expect(addNumbers(3, 5)).toBe(8);
});

test('Geçersiz parametrelerde hata fırlatılmalı', () => {
  expect(() => addNumbers('a', 5)).toThrow('Her iki parametre de sayı olmalıdır.');
});
```

# 16. Sonuç ve Kaynaklar

## Sonuçlar

- JavaScript'in temellerini öğrendiniz.
- Clean Code prensiplerini kavradınız.
- SOLID prensiplerini öğrendiniz ve nasıl uygulanacağını anladınız.
- Kod dökümantasyonu, yorumlar ve test yazmanın önemini kavradınız.
- Unit testlerin nasıl yazılacağını öğrendiniz.
- Test otomasyonunun faydalarını ve popüler test çerçevelerini keşfettiniz.

## Kaynaklar

- [MDN Web Docs - JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [W3Schools](https://www.w3schools.com/js/)
- [Clean Code: A Handbook of Agile Software Craftsmanship by Robert C. Martin](https://www.goodreads.com/book/show/3735293-clean-code)
- [Clean Code JS](https://github.com/ryanmcdermott/clean-code-javascript)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [Jest - JavaScript Testing Framework](https://jestjs.io/)

Teşekkürler!
















