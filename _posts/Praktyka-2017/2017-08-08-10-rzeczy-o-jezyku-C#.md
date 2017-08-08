---
layout: post
title:  "10 rzeczy o języku C#, które nauczyłem się podczas pierwszego miesiąca praktyk.
"
date:   2017-08-08 -0600
categories: 
---

Witam Cię, Czytelniku, w moim pierwszym artykule podsumowującym pierwszy miesiąc praktyk. Jestem studentem 3 roku Informatyki Stosowanej. Moją Alma Mater jest Akademia-Górniczo Hutnicza im. Stanisława Staszica w Krakowie. Studiuję dziennie na Wydziale Inżynierii Metali i Informatyki Przemysłowej. 

W ciągu ostatniego miesiąca, moja wiedza teoretyczna skonfrontowała się z prawdziwą pracą programisty. Stanowiło to ciekawe doświadczenie, które uświadomiło mi, jak duże są braki w mojej wiedzy. W tym artykule chciałbym przedstawić pewną listę funkcjonalności języka C# zawierającą poznane przeze mnie zagadnienia. 

## 1. Value Type i Reference Type ##

Zmienne tworzone i przechowywane w pamięci można podzielić na dwa typy: [Value Type](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/value-types) oraz [Reference Type](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/reference-types). 
Operacje tworzenia i przypisania zmiennych są realizowane w odmienny sposób w zależności od danego typu. `Value Type` jest zapisywany na stosie, a `Reference Type` na stercie. 
[Pod tym linkiem]( https://www.youtube.com/watch?v=0CsRK1HzJWk ) znajdziesz film, który w prosty sposób przedstawia podstawową różnicę pomiędzy `Value Type` a `Reference Type`.

## 2. String vs. StringBuilder ##
 
Konkatenacja dużej liczby stringów nie jest optymalna. Spowodowane jest to niemutowalnością, niezmiennością (immutable) stringa. 
Rozwiązaniem tego problemu może być wykorzystanie klasy `StringBuilder`, która korzysta z mutowalnego (mutable) typu `string`. Dokładnie rzecz ujmując korzysta z tablicy charów.

- [W tym filmie przedstawione są różnice pomiędzy stringiem, a klasą StringBuilder](https://www.youtube.com/watch?v=4lFAs6FYTXg)
- [Link do artykuły wyjaśniającego niezmienność typu string w C#](http://www.c-sharpcorner.com/UploadFile/b1df45/string-is-immutable-in-C-Sharp/)

## 3. NullableTypes ##
   
Value Type nie posiada wartości `null`. Jednakże istnieje typ, który pozwoli przypisać do takiej zmiennej wartość `null`.
Typ ten posiada dwie metody zapisu: `Nullable<T>` lub krótszy `T?`.
- [Link do dokumentacji opisujący  NullableTypes](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/nullable-types/)
- [Artykuł poruszający temat wartości null i nullable types](http://cezarywalenciuk.pl/blog/programing/post/kurs-obiektowosc-w-c-wartosci-null-i-typy-nullable-04)

## 4. LINQ ##
   
Podczas pierwszego miesiąca praktyk poznałem LINQ, czyli zintegrowane zapytania językowe.  Technologia ta pozwala tworzyć zapytania np. na kolekcjach. Zapytanie możemy skonstruować przy pomocy lambd które sprawiają, że nasz kod staje się krótszy i bardziej czytelny. Prosty przykład poniżej przedstawia filtrowanie kolekcji przy użyciu pętli `foreach` oraz LINQ. 

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };
var result = new List<int>();

foreach (var number in numbers)
{
    if (number < 3)
    {
        result.Add(number);
    }
}	

//result -> 1, 2
```

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };

var result = numbers.Where(n => n < 3).ToList();

//result -> 1, 2
```

- [101 przykładów użycia LINQ przy wykorzystaniu lambd ](http://linq101.nilzorblog.com/restriction-operators.php#where-simple-1)

## 5. params ##

Nie znając `params` utworzyłbym metodę, która przyjmowałaby jako argument listę parametrów w następujący sposób:


 ```csharp
public void Foo(int [] parameters) {}
//Przykład użycia:
Foo(new int[3]{1, 2, 3});
 ```
Po dokładniejszym poznaniu języka C# wiem, że można w takim przypadku wykorzystać słówko kluczowe params. Pozwala ono na podanie argumentów rozdzielonych przecinkami. 

```csharp
public void Foo(params int [] parameters) {}
//Przykład użycia:
Foo(1, 2, 3);
   ```
Słowo kluczowe params wykorzystuje m.in. metoda `Split` służąca do dzielenia ciągów znaków na podciągi. Metoda ta przyjmuje jako argumenty separatory oddzielone przecinkami.

## 6. [Action](http://www.tutorialsteacher.com/csharp/csharp-action-delegate) i [Func](http://www.tutorialsteacher.com/csharp/csharp-func-delegate) ##

Gotowe delegaty takie jak `Action<T>` i `Func<TParameter,TOutput>`, pozwalają na przypisanie metody do zmiennych oraz zmianę implementacji metody w naszym kodzie. Mogą zostać przekazane do metody jako argumenty. Różnica pomiędzy tymi dwoma delegatami polega na tym, że `Func` posiada parametry wejściowe oraz zwracaną wartość,natomiast `Action` nie posiada wartości zwracanej. Przykład wykorzystania delegatu `Func` znajduję się w następnym paragrafie.
	
## 7. Extension Methods ## 

Extension Methods pozwalają dodać do istniejącego już typu nowej metody. To rozwiązanie wykorzystuje m.in. wcześniej wymienioną technologię LINQ. Gotową klasę wystarczy zaimportować, aby móc skorzystać z napisanej metody. Poniżej przedstawiam przykład wykorzystujący mechanizm extension methods wzorowany na metodzie `Where()` z LINQ, który korzysta z gotowego delegatu `Func`.

```csharp
namespace MyLinq
{
    public static class MyExtension
    {
        public static T[] Where<T>(this T [] src, Func<T, bool> filter )
        {
            var result = new List<T>();

            foreach (var item in src)
            {
                if (filter(item))
                {
                    result.Add(item);
                }
            }
            return result.ToArray();
        }
    }
}
```
- [Link do artykułu opisującego mechanizm Extension Methods](https://www.dotnetperls.com/extension)

## 8. Lazy evaluation ##

Pojęcie to wywodzi się z języków funkcyjnych. W dużym skrócie Lazy Evaluation polega na m.in. wykonywaniu fragmentu kodu tylko wtedy, kiedy jest to wymagane. W pewnych przypadkach Lazy Evaluation pozwoli przyspieszyć nasz program. Zamiany zwykłych zmiennych na metody pozwoli w C# na wykorzystanie Lazy Evaluation. Innym sposobem na wprowadzenie Lazy Evaluation jest użycie klasy generycznej `Lazy<T>` .
Opóźnia ona tworzenie obiektu, gdy jest on bardzo duży i zasobożerny i nie mamy pewności, czy w ogóle będzie potrzebny w trakcie wykonywania kodu. 

- [Pod tym linkiem znajdziesz artykuł omawiający Lazy Evaluation w języku C# z przykładem, w którym wykorzystuje się wcześniej wspomniane delegaty](http://cezarywalenciuk.pl/blog/programing/post/wartosciowanie-leniwe---lazy-evaluation--kp-funkcjonalnego-w-csharp)

- [Artykuł omawiający klasę Lazy](https://www.dotnetperls.com/lazy) 

## 9. "Possible multiple enumeration of IEnumerable" ##

`Possible multiple enumeration of IEnumerable` jest podpowiedzią dla piszącego kod, która ostrzega przed możliwym wielokrotnym wyliczeniem. Komunikat ten wynika z osobliwego działania metody `Where()`. Użycie metody nie wykonuje żadnego kodu. Takie zapytanie jest przechowywane, lecz nie wywoływane od razu. W momencie operacji na kolekcjach korzystających z metody `Where()` będą wykonywane wszystkie przechowywane zapytania. Aby uniknąć wielokrotnego wykonywania tych zapytań można skorzystać z dwóch dostępnych metod `ToArray()` albo `ToList()`. Zwrócą one kolekcję, na której zostały już wykonane wszystkie zapytania.

- [Link do artykułu poruszającego kwestię wykonywania zapytań](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/ef/language-reference/query-execution)

## 10. Tuple ##

`Tuple` to statyczna klasa, która pozwala na szybkie prototypowanie obiektów. Choć w kwestii korzystania z klasy `Tuple` zdania są podzielone, to w najnowszej wersji języka C# Microsoft wprowadza nowe funkcjonalności do tej klasy np. możliwość dekonstrukcji deklaracji. 
 
- [Link do artykułu o klasie Tuple](http://www.pzielinski.com/?p=1174)
- [Link do posta z nowościami w klasie Tuple](https://blogs.msdn.microsoft.com/dotnet/2017/03/09/new-features-in-c-7-0/)