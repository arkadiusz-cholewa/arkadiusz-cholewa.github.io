---
layout: post
title:  "9 rzeczy o języku JavaScript, które nauczyłem się po dwóch miesiącach praktyki."
date:   2017-09-11 -0600
categories: 
---

W moim [pierwszym artykule](https://arkadiusz-cholewa.github.io/2017/08/08/10-rzeczy-o-jezyku-C.html) poruszyłem temat funkcjonalności w języku C# poznanych podczas pierwszego miesiąca praktyk. W czasie praktyki mam możliwość współtworzenia frontendu aplikacji właśnie przy pomocy języka JavaScript. Korzystamy również z wielu bibliotek i frameworka, ale to temat na inny artykuł. 

W tym artykule chciałbym wymienić 9 funkcjonalności języka, które udało mi się poznać i uważam, że każdy frontend developer powinien je znać i stosować. A dlaczego warto? Poznając tajniki języka programowania będziemy  pisać bardziej wartościowy, krótszy i czytelniejszy kod, a tym samym będziemy stawać się lepszymi developerami. 

## 1.	var i let ##

Dobrą praktyką programistyczną jest tworzenie zmiennych o jak najmniejszym zasięgu (ang. scope). Na niekorzyść języka JavaScript, słowo kluczowe `var` pozwala tworzyć zmienne globalne lub lokalne tylko dla bloku funkcji. Na szczęście JavaScript w wersji ES6 wprowadza nowe słowo kluczowe `let`. Zasięg zmiennych zadeklarowanych przy pomocy `let` ograniczony jest do bloku, czy też wyrażenia, w którym zostały utworzone. Dwa przykłady poniżej przedstawią problem wynikający z natury działania var i rozwiązanie go za pomocą słowa kluczowego `let`.

```javascript
var x = 100;
let y = 100;

if (true) {
  var x = 200; //poprzedni x i ten, to ta sama zmienna
  let y = 200;
}

console.log(x); // x -> 200 
console.log(y); // y -> 100
```
```javascript
for (var i = 0; i < 10; i++) {
  //...
}
console.log(i);  // i -> 10

for (let j = 0; j < 10; j++) {
  //...
}
console.log(j) // ReferenceError: j is not definied
```

## 2.	Dwa operatory równości ##
 
Ucząc się języka JavaScript poznajemy dwa różne operatory porównania.
Pierwszy, znany z innych języków programowania (C++, Java) to operator `==` który w JS porównuję tylko wartości i pozwala na uprzednią konwersję wartości. 

Dlatego warunek `5 =='5'` będzie prawdziwy, ponieważ przed porównaniem `‘5’` jest konwertowana na wartość `5` i dopiero po konwersji następuje porównanie wartości. 

```javascript
5 == 5 // true
```

Aby mieć większą kontrolę nad porównywaniem zmiennych JavaScript posiada operator `===`, który porówna wartość oraz typ zmiennych i nie pozwali na wcześniejszą konwersję zmiennych, tak jak w przypadku operatora `==`. 

```javascript
5 === '5' // false
```

## 3.	Operator potrójny (Ternary operator) ##
Operator występujący w wielu językach programowania również w JS. Pozwala on zapisać warunek `if` w skrótowej formie. Kod staję się krótszy i czytelniejszy.
 
Zapis: 
 ```javascript
 let isActive = true;
let result = '';
 if(isActive) {
   result = 'YES';
 } else {
   result = 'NO';
 }
```
Jest równoznaczny zapisowi:
  ```javascript
  let isActive = true;
  let result = isActive ? 'YES' : 'NO';
```
- [Jeśli chodzi o performence kodu to ternary operator działa wolniej niż klasyczny if/else](https://stackoverflow.com/questions/2586842/javascript-if-else-or-ternary-operator-is-faster)



## 4.	Truthy i Falsy ##
W JavaScript poza wartościami `true` i `false` występują "wartości" `truthy` i `falsy`. 
Termin truthy nie oznacza, że zmienna o wartości 100 ma również wartość `true`. Można powiedzieć, że jej wartość jest podmieniana na wartość logiczną w momencie, gdy dana zmienna zostaje użyta w kontekście warunku logicznego. 
Wszystkie wartości są truthy poza `false`, `null`, `undefined`, `0`, pusty `string` i `NaN` (nie posiadają realnej wartości). 
Dzięki Truthy i Falsy można tworzyć bardziej zwięzły kod np. instrukcjach warunkowych. 
 
 ```javascript
function sayHello(person) { 
  return person.specialWelcome ? `${person.specialWelcome} Im ${person.name}`: `Hello, Im ${person.name }`
}
  
let shorty = {name: "Shorty", specialWelcome: 'Whatzzzzzz up!' };
let bob = {name: "Bob"};

console.log(sayHello(bob)); // -> Hello, Im Bob
console.log(sayHello(shorty)); // -> Whatzzzzzz up! Im Shorty
```
## 5.	Destructuring assignment ##

Destructuring assignment  to operacja pozwalająca na przypisanie danych z tablicy lub obiektu bezpośrednio do zmiennych.  Bardzo ciekawym przypadkiem użycia jest przypisanie elementów tablicy zwracanej przez metodę do zmiennych.

 ```javascript
function foo() {
  return [1, 2];
}

let [a, b] = foo(); 

console.log(a); // a -> 1
console.log(b); // b -> 2
```
W łatwy i czytelny sposób zapisujemy zwrócone dane. 


## 6. JSON.parse() i JSON.stringify() ##
 
Warto zauważyć, że komunikując się z API poprzez protokół HTTP, dane wysyłane i odbierane to zwyczajny tekst zapisany w różnych formatach np. JSON. `JSON.parse() ` pozwala na zamianę zwykłego stringa w zapisie JSON na obiekt javascriptowy. Natomiast `JSON.stringify() ` działa odwrotnie, to znaczy zamienia obiekt na tekst w formacie JSON.

```javascript
let personJSON = '{"name":"Bob"}';
let personObject = JSON.parse(personJSON);

console.log(personObject.name); // -> Bob
console.log(personJSON === JSON.stringify(personObject)); // -> true
```

## 7.	Arrow functions ##

`Arrow functions` to nowość wprowadzona do języka JS w standardzie ES6. 

Dwie największe zalety funkcji strzałkowych:

1. Krótszy zapis metod anonimowych
2. Automatyczny dostęp do `this`'a z poza bloku metody (więcej szczegółów w paragrafie 13.2 w linku poniżej)

Funkcja anonimowa:
  - bez parametrów

```javascript
function() {return 1} //ES5

() => 1 //ES6
```
- z parametrami:

```javascript
function(a, b) {return a + b} //ES5

(a,b) => a + b; // ES6
```

- [Po więcej szczegółów zapraszam do lektury](http://exploringjs.com/es6/ch_arrow-functions.html) 

## 8. map() i filter() ## 

Metody `map()` i `filter()` to natywne metody języka JavaScript, służące do manipulowania zbiorami danych, które każdy programista powinien znać i rozsądnie używać. Dzięki tym metodom nasz kod będzie bardziej czytelny i krótszy (szczególnie, gdy wykorzystamy w zapisie arrow functions). Istnieje kilka wariantów tychże metod. Możemy skorzystać z tych wbudowanych w język, napisać własne lub skorzystać z biblioteki. Jeżeli interesuje nas wydajność to warto sprawdzić, która implementacja jest najszybsza. W przeciwnym wypadku, aby przyspieszyć kodowanie można skorzystać z gotowych rozwiązań. Oczywiście nie są to jedyne metody, ktore operują na tablicach, ale uważam, że są najbardziej użyteczne.
 
## 9. Lodash ##
[Lodash](https://lodash.com/) to biblioteka napisana w języku JavaScript, służąca do manipulowania danymi. Jeżeli chcesz napisać metodę operującą na tablicy, obiekcie lub stringu to sprawdź, czy nie została już zaimplementowana w lodash'u. Wykorzystanie tej biblioteki przyspieszy pisanie kodu, a zarazem zwiększy jego wydajność.

 - [Link do benchmarka](https://jsperf.com/native-map-vs-lodash-map)
 porównującego wydajność metod z lodasha z natywnymi metodami, które oferuje JavaScript. 
 - Aby pozostać obiektywnym znalazłem również przykład, gdy [natywna metoda jest dużo szybsza od tej z biblioteki](https://jsperf.com/lodash-get-vs-native-2)
- Oraz przykład porównania wydajności [metody map w 4 różnych implementacjach](https://jsperf.com/map-lodash-vs-native-vs-loop)