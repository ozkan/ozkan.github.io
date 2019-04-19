---
layout: post
title: "Jeklly-Liquid Yapısı"
date: 2019-04-20 01:35:20 +0300
description: Jeklly-Liquid Yapısı
img: liquid.png 
tags: [Liquid, Jekyll]
---




## Liquid Nedir?
Liquid, Shopify tarafından özel gereksinimler için Ruby ile yazılmış açık kaynaklı bir şablon dilidir. Web uygulamalarında içeriği dinamik olarak yüklemek için kullanılır.
[Github/Liquid](https://github.com/Shopify/liquid)

## Jekyll'da Liqut Kullanımı
 Jekyll, koşullu ifadeleri, çıktıları ve filtreleri uygulamak için Liquid'in en iyi şekilde kullanılmasını sağlar. Jekyll’de Liquid’in nasıl kullanılacağını bakalım.
[Github/Jekyll](https://github.com/jekyll/jekyll)

 Jekyll, verileri dinamik olarak yüklemek, sitedeki verilere erişmek ve koşullu işlemler gerçekleştirebilmek için Luquit kullanır.

Liquid oldukça  basit ve kapsamlı bir dildir. Örnek bir kod parçası:

{% raw %}

```
{% if sayi > 1 %}
    sayi değeri pazitif
{% elsif  sayi == 0 %}
    sayi değeri sıfıra eşit
{% else %}
    sayi değeri negatif
{% endif %}
```

{% endraw %}

Liqiut'in  üç temel yapıdan oluşur, bunlar:

| Etiketler (Tags) | Nesneler(Object) | Filtreler(Filters) |
|:----------------:|:--------------:|:------------------:|
|       {% %}      |      {{ }}     |      {{  | }}      | 


## Etiketler (Tags)

Etiketler işlevseldir. Genelde ne yapacağını ve bir şeyi nasıl yapacağını söylerler. Kontrol akışlarını, yinelemeleri vb. Uygulamak için kullanılırlar. Bunun için en iyi örnek yukarıda bahsettiğim olabilir.

Koşullu ifadelerin yanı sıra, etiketler ayrıca _includes klasörlerinden bir dosyayı dahil etmek gibi özel amaçlar için de kullanılır. (jekyll'da iclude yapısını ayrıca anlatacağım)

## Nesneler (Object)

Nesneler, bir sayfaya dinamik veri üretmek için kullanılır. Çift küme parantezi içerinede tanımlanan yapılır web arayüzünde gösterilecek olan içerikler için kullanılır. Örneğin Jakyll'da sayfa başlığını şu şekilde alabiliriz.

{% raw %}

```
{{page.title}}
```
{% endraw %}

Yukarıdaki kod bu web sayfasında eklenirse şöyle bir çıktı verecektir.

```
Jekyll-Liquid Yapısı
```

## Filtreler (Filters)
Filtreler çıktıları değiştirmek için kullanılır. Nesnelerle birlikte kullanılır. Basit bir örnek aşağıda gösterilmiştir.

{% raw %}

```
{{ page.title | upcase }}
```

{% endraw %}

Sonuç:
JEKYLL-LIQUID YAPISI

upcase filtresi aldığı bütün karakterleri büyük harfe çevirir.
Liquid'daki diğer filtreleri  yazının devamında göreceğiz.

Güncellenecek..

