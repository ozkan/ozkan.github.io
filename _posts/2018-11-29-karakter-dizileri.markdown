---
layout: post
title: "Python Karakter Dizilerinin Metotları"
date: 2018-11-29 23:47:20 +0300
description: Python Karakter Dizilerinin Metotları 
img: karakter_dizileri.png
tags: [python, karakter-dizileri]
---

  Karakter dizilerinin metotlarını dir() gömülü fonksiyonunu kullanarak listeleyebiliriz.  
dir() fonksiyonu, parametre olarak aldığı nesnenin geçerli özniteliklerinin bir listesini döndürür.

Eğer parametresiz olarak çalıştırılırsa, mevcut alandaki niteliklerin listesini döndürür.Karakter dizilerinin metotlarına şu şekilde ulaşabiliriz: dir(str)  
veya dir() fonksiyonuna bir karakter dizisi vererek: dir("karater")

{% highlight python %}
dir(str)
{% endhighlight %}

{% highlight python %}
['__add__',
 '__class__',
 '__contains__',
 '__delattr__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__getitem__',
 '__getnewargs__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__iter__',
 '__le__',
 '__len__',
 '__lt__',
 '__mod__',
 '__mul__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__rmod__',
 '__rmul__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 'capitalize',
 'casefold',
 'center',
 'count',
 'encode',
 'endswith',
 'expandtabs',
 'find',
 'format',
 'format_map',
 'index',
 'isalnum',
 'isalpha',
 'isdecimal',
 'isdigit',
 'isidentifier',
 'islower',
 'isnumeric',
 'isprintable',
 'isspace',
 'istitle',
 'isupper',
 'join',
 'ljust',
 'lower',
 'lstrip',
 'maketrans',
 'partition',
 'replace',
 'rfind',
 'rindex',
 'rjust',
 'rpartition',
 'rsplit',
 'rstrip',
 'split',
 'splitlines',
 'startswith',
 'strip',
 'swapcase',
 'title',
 'translate',
 'upper',
 'zfill']
{% endhighlight %}

***

> `isalnum()` Karakter dizisinin, sadece harflerden ve/veya sayılardan oluşup oluşmadığını sorgular.

{% highlight python %}
"1923Türkiye".isalnum()
{% endhighlight %}

**\>>>**  True



{% highlight python %}
"1923 Türkiye".isalnum() #boşluk karakterine dikkat
{% endhighlight %}

**\>>>**  False

***

> `isalpha()` Karakter dizisinin yanlızca harflerden oluşup oluşmadığını sorgular.

{% highlight python %}
"python".isalpha()
{% endhighlight %}

**\>>>**  True



{% highlight python %}
"python3".isalpha()
{% endhighlight %}

**\>>>**  False

***

> `isdecimal()` Karakter dizisi içindeki sayının ondalık sayı cinsinden olup olmadığını sorgular.

{% highlight python %}
"1923".isdecimal() 
{% endhighlight %}

**\>>>**  True



{% highlight python %}
"3.14".isdecimal()
{% endhighlight %}

**\>>>**  False

***

> `isdigit()`  Karakter dizisinin sadece sayılarda oluşup oluşmadığını sorgular.
> True dönderebilmesi için, sayı değerli karakter dizilersinin bir tam sayıdan oluşması gerekiyor.

{% highlight python %}
"1923".isdigit()
{% endhighlight %}

**\>>>**  True



{% highlight python %}
"1923.5".isdigit()
{% endhighlight %}

**\>>>**  False

***

> `isidentifier()` Karakter dizisi içindeki karakterin bir tanımlayıcı olarak kulanılıp kullanımayacağını sorgular.
> örneğin fonksiyonlar ve değişkenleri tanımlarken, bunları sayı ile başlatamıyoruz.
> Yani 1abc şeklinde bir değişken tanımlayamayız. 
> Bunu bir de isidentifier() methoduna soralım, tanımlayabiliyor muyuz diye.

{% highlight python %}
"1abc".isidentifier()
{% endhighlight %}

**\>>>**  False

***

> `islower()` Karakter dizisinin tamamen küçük harflerden oluşup oluşmadığını sorgular.

{% highlight python %}
"python".islower()
{% endhighlight %}

**\>>>**  True

***

> `isnumeric()` Karakter dizisinin sadece sayılardan oluşup oluşmadığını sorgular.

{% highlight python %}
"2019".isnumeric()
{% endhighlight %}

**\>>>**  True

***

> `isprintable()` Karakter dizsin yazdırılmayan bir karakter barındırıp barındırmadığını sorgular. 
> örneğin "\n", "\t" gibi kaçış dizileri basılamayan (yazılmayan) karakterlerdir.

{% highlight python %}
"\n".isprintable() 
{% endhighlight %}

**\>>>**  False



{% highlight python %}
"Programlama \t".isprintable() 
{% endhighlight %}

**\>>>**  False



{% highlight python %}
"python".isprintable() 
{% endhighlight %}

**\>>>**  True

***

> `isspace()` Karakter dizisinin sadece boşluk karakterinden oluşup oluşmadığını sorgular.

{% highlight python %}
"  ".isspace()
{% endhighlight %}

**\>>>**  True



{% highlight python %}
"boşluk".isspace()
{% endhighlight %}

**\>>>**  False

***

> `istitle()` Karakter dizisindeki kelimelerin baş harflerinin büyük harf olup olmadığını sorgular. 
True dönderebilmesi için sorguladığı kelimelerdeki baş haflerinin büyük, geriye kalan diğer harflerin küçük olması gerekiyor.

{% highlight python %}
"Türkiye Cumhuriyeti".istitle()
{% endhighlight %}

**\>>>**  True


{% highlight python %}
"Türkiye cumhuriyeti".istitle()
{% endhighlight %}

**\>>>**  False

***

> `isupper()` Karakter dizisindeki bütün harflerin büyük harf olup olmadığını sorgular.

{% highlight python %}
"PYTHON".isupper() 
{% endhighlight %}

**\>>>**  True

{% highlight python %}
"Python".isupper()
{% endhighlight %}

**\>>>**  False

***
> `endswith()` Karakter dizisinin parametre olarak verilen karakter ile bitip, bitmediğini sorgular.

{% highlight python %}
"python".endswith("n")
{% endhighlight %}

**\>>>**  True

{% highlight python %}
"python".endswith("z")
{% endhighlight %}

**\>>>**  False

***

> `capitalize()` Karakter dizilerinin yalnızca baş harfini büyütür.

{% highlight python %}
"python".capitalize()
{% endhighlight %}

**\>>>**  'Python'



{% highlight python %}
"python turkiye".capitalize()
{% endhighlight %}

**\>>>**  'Python turkiye'

***

> `casefold()` Karakter dizilerindeki harflerin hepsini küçük harfe çevirir.

{% highlight python %}
"PYTHON".casefold()
{% endhighlight %}

**\>>>**  'python'

***

> `center()` Karakter dizilerini ortalar.
> center() methoduna girilen parametre, karakter dizisinin kaç karakterlik bir yer kaplayacağını belirtir.

{% highlight python %}
"python".center(10)
{% endhighlight %}

**\>>>**  '  python  '
***

> `ljust()` Karakter dizisini sola hizalar, bu işlemini yaparken karakterin sağına ekleme yaparak karakteri sola yaslar.
> İki tane parametre alır, ilk parametre toplam karakter uzunluğunu , ikinci parametre ise sağa eklenecek karakteri belirler.
> Eğer ikinci parametreyi belirmezsek, hizalama işlemini yaparken boşluk karakterini kullanır.

{% highlight python %}
"python".ljust(20, "-")
{% endhighlight %}

**\>>>**  'python--------------'



{% highlight python %}
"python".ljust(20)
{% endhighlight %}

**\>>>**  'python              '

***

> `rjust()` Karakter dizisini sağa hizalar, bu işlemi yaparken karakterin soluna ekleme yaparak karakteri sağa yaslar.
> İki tane parametre alır, ilk parametre toplam karakter uzunluğunu , ikinci parametre ise sola eklenecek karakteri belirler.
> Eğer ikinci parametreyi belirmezsek, hizalama yaparken boşluk karakterini kullanır.

{% highlight python %}
"python".rjust(15, "-")
{% endhighlight %}

**\>>>**  '--------- python'


{% highlight python %}
"python".rjust(15)
{% endhighlight %}

**\>>>**  '         python'

***

> `strip()` Parametresiz olarak kullanıldığında, karakter dizisinin sağında 
> ve solunda bulunan boşluk karakteri ile kaçış dizilerini siler.
> Parametre olarak bir karakter dizisi alır, girilen parametre karakter 
> dizisinin sağında veya solunda var ise siler.

{% highlight python %}
" python  ".strip()# parametresiz kullanıldığında, sağdaki ve soldaki boşlukları sildi.
{% endhighlight %}

**\>>>**  'python'

{% highlight python %}
"python".strip("p")
{% endhighlight %}

**\>>>**  'ython'

***

> `lstrip()` Paremetre olarak girilen karakteri, karakter dizisinin sol 
> tarafından kaldırır.
> Eğer parametresiz olarak kullanılırsa, kaçış dizilerini (\n, \t) ve 
> boşluk karakterini,  karakter dizisinin sol tarafından kaldırır.

{% highlight python %}
"python".lstrip("py")
{% endhighlight %}

**\>>>**  'thon'

{% highlight python %}
"       python".lstrip()
{% endhighlight %}

**\>>>**  'python'

{% highlight python %}
"  \n  \t python".lstrip()
{% endhighlight %}

**\>>>**  'python'

***

> `rstrip()` Paremetre olarak girilen karakteri, karakter dizisinin sağ 
> tarafından kaldırır.
> Eğer parametresiz olarak kullanılırsa, kaçış dizilerini (\n, \t) ve 
> boşluk karakterini,  karakter dizisinin sağ tarafından kaldırır.

{% highlight python %}
"pyth".rstrip("on")
{% endhighlight %}

**\>>>**  'python'

{% highlight python %}
"python   ".rstrip()
{% endhighlight %}

**\>>>**  'python'

***

> `count()` Karakter dizisi içindeki belli bir karakterin kaç kez geçtiğini sorgular.

{% highlight python %}
"malatya".count("a")
{% endhighlight %}

**\>>>**  3

***

> `index()` Parametre olarak aldığı karakterin, karakter dizisi içinde kaçıncı sırada olduğunu sorgular.
> Eğer sorguladığımız karakter, karakter dizisinin içinde bulunmuyorsa Python bir hata mesajı gösterir. 
> (ValueError: substring not found)

{% highlight python %}
"Matematik".index("a")
{% endhighlight %}

**\>>>**  1

{% highlight python %}
"Matematik".index("A")
{% endhighlight %}

{% highlight python %}
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-42-69fe97c2e4a7> in <module>()
----> 1 "Matematik".index("A")

ValueError: substring not found
{% endhighlight %}

***

> `rindex()` Parametre olarak aldığı karakterin, karakter dizisi içinde kaçıncı sırada olduğunu sağdan başlayarak sorgular.
> Eğer sorguladığımız karakter, karakter dizisinin içinde bulunmuyorsa Python bir hata mesajı gösterir.

{% highlight python %}
"python python".rindex("p")
{% endhighlight %}

**\>>>**  7

***

> `find()` Parametre olarak aldığı karakterin, karakter dizisi içindeki konumunu sorgular.
>
> Eğer sorgulanan karakter, karakter dizisinin içinde yok ise   -1 değerini verir.

{% highlight python %}
"python".find("t")
{% endhighlight %}

**\>>>**  2

{% highlight python %}
"python".find("s")
{% endhighlight %}

**\>>>**  -1

***

> `rfind()` Parametre olarak aldığı karakterin, karakter dizisi içindeki konumunu sağdan başlayarak sorgular.
> Eğer aranan karakter dizinin içinde yok ise -1 değerini dönderir.

{% highlight python %}
"pythonp".rfind("p")
{% endhighlight %}

**\>>>**  6

***

> `split()` Parametresiz olarak kullanıldığında karakter dizisini boşluklardan bölerek, bir listeye ekler.
> split() Karakter dizisini soldan sağa doğru tarar. 
> Parametresiz olarak kullanılırsa eğer, karakter dizisini boşluklardan böler.
> İlk parametre ile hangi karakterlerden bölüneceği,
> ikinci parametre ile kaç kez bölüneceği belirtilir.

{% highlight python %}
"Malatya İnönü".split() #parametresiz kullanım
{% endhighlight %}

**\>>>**  ['Malatya', 'İnönü']

{% highlight python %}
"Malatya İnönü Üniversitesi".split(" ", 1) #parametreli kullanım
{% endhighlight %}

**\>>>**  ['Malatya', 'İnönü Üniversitesi']

***

> `rsplit()` Parametresiz olarak kullanıldığında karakter dizisini boşluklardan bölerek, bir listeye ekler.
> rsplit() Karakter dizisini sağdan sola doğru tarar.
> İlk parametre ile hangi karakterlerden bölüneceği,
> ikinci parametre ile ise kaç kez bölüneceği belirtilir.

{% highlight python %}
"Malatya İnönü".rsplit() #parametresiz kullanım
{% endhighlight %}

**\>>>**  ['Malatya', 'İnönü']

{% highlight python %}
"Malatya İnönü Üniversitesi".rsplit(" ", 1) #parametreli kullanım
{% endhighlight %}

**\>>>**  ['Malatya İnönü', 'Üniversitesi']

***

> `splitlines()` Karakter dizisini satır başı karakterinden (" \n") ayırarak bir listeye ekler.

{% highlight python %}
"Öğretmenler!\nCumhuriyet, fikren, ilmen, fennen, bedenen kuvvetli ve yüksek karakterli muhafızlar ister.\nYeni nesli bu özellik ve kabiliyette yetiştirmek sizin elinizdedir".splitlines()
{% endhighlight %}

**\>>>**  ['Öğretmenler!',
 'Cumhuriyet, fikren, ilmen, fennen, bedenen kuvvetli ve yüksek karakterli muhafızlar ister.',
 'Yeni nesli bu özellik ve kabiliyette yetiştirmek sizin elinizdedir']

***

> `zfill()` Karakter dizisinin önüne sıfır ekleyerek sağa yaslar.

{% highlight python %}
"py".zfill(10)
{% endhighlight %}

**\>>>**  '00000000py'

***

> `upper()` Karakter dizisindeki bütün harfleri büyütür.

{% highlight python %}
"türkiye".upper()
{% endhighlight %}

**\>>>**  'TÜRKIYE'

***

> `lower()` Karakter dizisindeki bütün harfleri küçük harflere çevirir.

{% highlight python %}
"PYTHON".lower()
{% endhighlight %}

**\>>>**  'python'

***

> `swapcase()` Karakter dizisindeki büyük harfleri küçük harflere, küçük harfleri ise büyük harflere çevirir.

{% highlight python %}
"PyThOn".swapcase()
{% endhighlight %}

**\>>>**  'pYtHoN'

***

> `title()` Karakter dizisindeki bütün kelimelerin baş harflerini büyütür.

{% highlight python %}
"türk dil kurumu".title()
{% endhighlight %}

**\>>>**  'Türk Dil Kurumu'

***

> `expandtabs()` Karakter dizisi içindeki tab uzunluğunu genişletir.

{% highlight python %}
"Python\tTurkiye".expandtabs(10)
{% endhighlight %}

**\>>>**  'Python    Turkiye'

***

> `partition()` Karakter dizisini, parametre olarak girilen karakterleri ortaya gelecek şekilde alarak üçe böler. Eğer boş karakterler var ise bunları sağ tarafa alır.

{% highlight python %}
"Malatya".partition("al")
{% endhighlight %}

**\>>>**  ('M', 'al', 'atya')

{% highlight python %}
"python".partition("ta")
{% endhighlight %}

**\>>>**  ('Malatya', '', '')

***

>`rpartition()` Karakter dizisini, parametre olarak girilen karakterleri ortaya gelecek şekilde alarak üçe böler. Eğer boş karakterler var ise bunları sol tarafa alır.

{% highlight python %}
"python".rpartition("p")
{% endhighlight %}

**\>>>**  ('', 'p', 'ython')

***


> `join()` Parametre olarak aldığı sıralı nesneyi (list, tuple) karakter dizisine çevirir. 

{% highlight python %}
" ".join(("Mustafa", "Kemal", "Atatürk"))
{% endhighlight %}

'**\>>>**  Mustafa Kemal Atatürk'

{% highlight python %}
"-".join(("Mustafa", "Kemal", "Atatürk"))
{% endhighlight %}

**\>>>**  'Mustafa-Kemal-Atatürk'



Not: Parametre olarak verilen veri tipinin tuttuğu nesneler sadece karakter dizilerinden oluşmalı.
Şu şekildeki bir kullanım hata verir.

{% highlight python %}
" ".join((123, "abc"))
{% endhighlight %}

{% highlight python %}
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-83-f130c6fb494f> in <module>()
----> 1 " ".join((123, "abc"))

TypeError: sequence item 0: expected str instance, int found
{% endhighlight %}

Bu hatadan, intager tipindeki değeri, string tipine çevirerek kurtulabiliriz.

{% highlight python %}
" ".join(map(str, (123, "abc")))
{% endhighlight %}

**\>>>**  '123 abc'

***

> `count()` Parametre olarak aldığı kararkterin, karakter dizisi içinde kaç kez geçtiğini sorgular.

{% highlight python %}
"müdür müdür müdür".count("müdür")
{% endhighlight %}

**\>>>**  3



count() Bir, iki veya üç parametreyle kullanılabilir.
Bir parametre ile nasıl bir sonuç dödürdüğünü gördük.
İkinci parametre ise sorgulamaya hangi sıradan başlayacğını belirtir.

{% highlight python %}
"müdür müdür müdür".count("müdür", 2)
{% endhighlight %}

**\>>>**  2



count() Methodunu üç parametrey kullanırsak, ilk parametre  sorgulanak karakteri, ikinci parametre sorgulamaya başlanacak sırayı,
üçüncü parametre ise sorgulamayı bitirecek sırayı belirtir.



{% highlight python %}
"Türkiye Cumhuriyeti".count("i", 6, 15)
{% endhighlight %}

**\>>>**  1

***

> `format()` Karakter dizisi biçimlendirmek için kullanılır.
> Prametre olarak verilen veriyi karakterin içinde belirtilen {} bloğunun yerine yazar.
> Karakter dizisi içinde kaç tane {} işareti varsa, format() metodu da o kadar parametre almalı.

{% highlight python %}
"python {}".format("turkiye")
{% endhighlight %}

**\>>>**  'python turkiye'

{% highlight python %}
"{} {} {} ".format("Malatya", "İnönü", "Üniversitesi")
{% endhighlight %}

**\>>>**  'Malatya İnönü Üniversitesi '

{% highlight python %}
a = "Mars"
"Merhaba  {0}".format(a)
{% endhighlight %}

**\>>>**  'Merhaba  Mars'



İstersek sıra da belirtebiliriz.

{% highlight python %}
"{1} {0} {2} ".format("Malatya", "İnönü", "Üniversitesi")
{% endhighlight %}

**\>>>**  'İnönü Malatya Üniversitesi '



Bir adet parametreyi birden fazla kez kullanabiliriz.

{% highlight python %}
"{0} {0} {1} {0}".format("Malatya", "İnönü")
{% endhighlight %}

**\>>>**  'Malatya Malatya İnönü Malatya'



Parametleri isimlendirerek kullanabiliriz.

{% highlight python %}
"{a} {b} {b} {a}".format(a="inönü", b="böte")
{% endhighlight %}

**\>>>**  'inönü böte böte inönü'



Bazı aritmetik işlemler de yaptırabiliriz. Örneğin onluk bir sayıyı ikili sayı sistemine şu şekilde çevirebiliriz.

{% highlight python %}
"{:b}".format(25)
{% endhighlight %}

**\>>>**  '11001'

float bir sayının, noktadan sonra alınacak basamak sayısını belirtip  yuvarlamasını isteyebiliriz.
örneğin 3.1415926 sayının noktadan sonra iki basamağını versin.

{% highlight python %}
"{:.2f}".format(3.1415926)
{% endhighlight %}

**\>>>**  '3.14'

***

> `format_map()` Parametre olarak bir sözlük (dict) verisi alır.

{% highlight python %}
sozluk= {'a':5,'b':10}
print('{a} {b}'.format_map(sozluk))
{% endhighlight %}

**\>>>**  5 10

Bu işlemi format metoduyla da yapabiliriz, kullanımı şu şekilde.
(Çift yıldız, anahtar kelimesini kullanır, **kwargs)

{% highlight python %}
sozluk= {'a':5,'b':10}
print('{a} {b}'.format(**sozluk))
{% endhighlight %}

**\>>>**  5 10

***

> ***encode()*** Karakter dizisini parametre olarak aldığı  kodlama sistemine göre kodlar.
> Varsayılan kodlama sistemi "utf-8" dir.

{% highlight python %}
"çelik".encode("cp1252")
{% endhighlight %}

**\>>>**  b'\xe7elik'

***


