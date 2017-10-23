---
layout: post
title:  "Aurelia - nowy atrybut: else"
date:   2017-10-21 -0600
categories: 
---

Nowy atrybut `else` wprowadzony do frameworka pozwala na utworzenie w widoku instrukcji warunkowej `if`/`else`.
Przed wprowadzeniem nowego atrybutu, aby napisać kod działający tak jak instrukcja `if`/`else`  należało dwukrotnie zbindować atrybut if, następnie wartość jednego z nich zanegować operatorem `!` aby móc obsłużyć wartość nie prawdziwą.

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

[Aurelia Release Notes - Early October 2017](http://blog.aurelia.io/2017/10/03/aurelia-release-notes-early-october-2017/)
