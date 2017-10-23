---
layout: post
title:  "Aurelia - nowy atrybut: else"
date:   2017-10-21 -0600
categories: 
---

Nowy atrybut `else` wprowadzony do frameworka pozwala na utworzenie w widoku instrukcji warunkowej `if`/`else`.
Przed wprowadzeniem nowego atrybutu, aby napisać kod działający tak jak instrukcja `if`/`else` można było dwukrotnie zbindować atrybut `if`, następnie wartość jednego z nich zanegować operatorem `!`, aby móc obsłużyć wartość nieprawdziwą.

{% highlight css %}
<template>
    <div if.bind="isActive">
    <!-- code -->
    </div>
    <div if.bind="!isActive">
     <!-- code -->
    </div>
</template>    
{% endhighlight %}

Po wprowadzeniu nowego atrybutu kod wygląda następująco:

{% highlight css %}
<template>
    <div if.bind="isActive">
    <!-- code -->
    </div>
    <div else>
     <!-- code -->
    </div>
</template>    
{% endhighlight %}

Informacje o pozostałych zmianach znajdziesz [w artykule Aurelia Release Notes - Early October 2017 Aurelia Blog](http://blog.aurelia.io/2017/10/03/aurelia-release-notes-early-october-2017/).
