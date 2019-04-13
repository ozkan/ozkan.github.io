---
layout: post  #yazının hangi layout'a göre oluşturulacağı
title: "Python ile faktöriyel hesaplama" #yazının tarayıcıda görünecek başlığı
date: 2018-11-18 01:55:00 +0300 #yazının tarihi
description: Python ile faktöriyel hesaplama. #yazının kısa açıklaması
img: python.png
published: true

`python` programlama dilini kullanarak, faktöriyel hesaplama. <br>
Hesaplama yapılırken çarpma işlemi operatörü kullanılmayacaktır.


{% highlight python %}
def fact(sayi):
    a = 3
    lst = []
    if sayi == 1 or sayi == 0:
        return 1
    elif sayi == 2:
        return 2
    else:
        for i in range(sayi-2):
            if not lst:
                lst.append([a for i in range(2)])
            else:
                lst.append([a for i in range(sum([j for k in lst for j in k]))])
                lst.pop(0)
            a += 1
        else:
            return sum(lst[0])
 
veri = int(input("Bir sayı girin: "))
print(str(veri)+"!= ", fact(veri))

{% endhighlight %}



{% include testet.html adres="https://repl.it/@celikozkan/UnwrittenUnknownMicrobsd?lite=true" %}

