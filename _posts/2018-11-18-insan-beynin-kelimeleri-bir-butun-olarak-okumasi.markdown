---
layout: post
title: "İnsan Beyninin Kelimeleri Bir Bütün Olarak Okuması"
date: 2018-11-18 18:28:20 +0300
description: Cambridge Üniversitesi'nde yapılmış bir araştırmanın sonucu 
img: "/assets/img/yazi-resmi.png"
tags: [python, cambridge]
published: true
---

Cambridge Üniversitesi'nde yapılmış bir araştırmanın sonucuna göre,<!--more-->
> Bir kleimedkei hafrlrein hnagi sıarda didizlikleri dğeil, ilk ve son hafrlrein dğoru yedre olamalrı öenm tşamıatkadır.  
> Geirsi taammen kamradaşır ve ynie de surosnuz olraak okubanilir. Buunn sbeebi isnan benyinin her hafri tek tek dieğl kemileelri bir
> btüün oralak omukadısır.

Python ile bu cümleleri otomatik oluşturun:
    
```python
from random import shuffle

def karistir(cumle):
    depo = []
    liste = cumle.split()
    for i in liste:
        kes = i[1:-1]
        uzunluk = len(kes)
        if uzunluk >= 2:
            lst= list(kes)
            shuffle(lst)
            depo.append(i[0]+("".join(lst))+i[-1])
        else:
            depo.append(i)
    else:
        return " ".join(depo)
        
veri= input("Bir şeyler yaz: ")
print(karistir(veri))
#ozkan
```

<p align="right"> {% include btn.html adres="https://repl.it/@celikozkan/insan-beyni-kelime" isim="Tıkla Test ET!" %} </p>
