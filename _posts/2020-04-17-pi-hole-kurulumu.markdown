---
layout: post
title: "Pi-Hole Kurulum Rehberi"
date: 2020-08-17 02:30:20 +0300
description: Pi-Hole kurulumu
img: pihole.png 
tags: [pi-hole, raspberry pi, reklam engelleme]
---

# Pi-Hole Nedir?

Kısaca Pi-hole, internetteki reklamları, zararlı yazılım barındıran siteleri ve izleyicileri engellemek için kullanılan bir araçtır. Pi-hole bu işlemleri yapabilmeniz için kendinize ait bir DNS sunucusu oluşturmanıza imkan verir. Kullanıcıların büyük bir kısmı Pi-hole yazılımını Raspberry pi cihazına kurarlar. İç ağa bağlı Raspberry pi cihazının ip adresi DNS olarak kullanılır ve işin geri kalan kısmını cihaza yüklü Pi-Hole yazılımı halleder. Pi-hole kullanan bir ağa bağlı tüm cihazlar estra bir yazılıma veya ayara ihtiyaç duymadan reklam ve izleyicilerden temizlenmiş olur. Bir web tarayıcısına reklam engelleme eklendisi kurup çalıştırmaktan farkı budur. Web tarayıcısındaki eklenti yalnızca tarayıcıdaki etkinlikleri kapsar, Pi-Hole ise üzerinden geçen geçen tüm internet trafiğini kapsar. Aslında teknik olarak yaptığı iş kara listeye eklenmiş bir bağlantı isteği aldığıda onu 0.0.0.0 ip adresine yönlendirmektir. Bu listeleri yayınlayan ve belli aralıklarla güncelleyen serviler bulunuyor.

## Raspberry Pi OS Kurulumu (Eski adıyla Raspbian)

`Bu makaleyi okuduğunuza göre büyük ihtimalle  bir raspberry Pi cihazınız var ve işletim sistemi yüklü.  Eğer elinizde Rasbian işletim sistemi kurulu bir Raspberry Pi varsa bu adımı geçebilirsiniz.`     
Pi-hole, Linux üzerinde çalışan sunucu yazılımıdır. Yüklemek için linux çalıştıran bir bilgisayara ihtiyacınız olacak. Biz Pi-hole yazılımı Raspberry Pi üzerinde kurup çalıştıracağız. 
Pi-hole, Raspberry Pi 2, 3, 4 veya Zero üzerinede çalışabilir. Genellikle Zero modeli tercih edilir. Pi-hole minimum için 512MB RAM ve 4GB SD kart yeterlidir. Zero modeli enerji tüketimi oldulça azdır ve modeminizin USB girişiyle besleyebilirsiniz.
Zero modelinde entegre bir Ethernet portu bulunmadığından, eğer modeme Ethernet kablosu bağlamak isterseniz bir adaptöre ihtiyacınız olacaktır.     

Raspbian'ı Raspberry Pi'ye yüklerken bir kaç seçeneğimiz var, ben `Raspberry Pi OS (32-bit) Lite` sürümünü kullandım. Bu sürümde bir masaüstü grafik arayüzü bulunmuyor. Herhangi bir ekrana veya klavyeye ihtiyaç duymuyor. Kurulumu ağ üzerinden gerçekleştirceğz.    
Şu adresten indirebilirsiniz. [https://www.raspberrypi.org/downloads/raspberry-pi-os/](https://www.raspberrypi.org/downloads/raspberry-pi-os/)
Dilerseneiz farklı bir sürümü de kullanabilirsiniz ama bu işlem için en uygun seçim "Raspberry Pi OS (32-bit) Lite" olacaktır.
Kurulum dosyasını indirin ve img dosyasını "Win32DiskImager" yardımıyla SD kartınıza kurun: 
Win32DiskImager İndirme Linki: [https://sourceforge.net/projects/win32diskimager/](https://sourceforge.net/projects/win32diskimager/)    
img dosyasını ve kurulum yapacağınız SD kartı seçin ve "write" butonuyla imajı SD karta yazdırın.   

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pihole-img.png)
</center>

Kurulum tamamladıktan sonra Raspberry Pi'de SSH etkinletirebilmek için  SD kartın Boot bölümüne uzantısız SSH adlı boş bir dosya oluşturun.  Pi açıldığında boot klasöründe  SSH dosyasını arar eğer bulursa SSH etkinleştirilir ve dosya silinir. Ayrıntılı bilgiye ihtiyaç duyarsanız  şu bağlantıdan 3. adıma bakabilirsiniz: [https://www.raspberrypi.org/documentation/remote-access/ssh/](https://www.raspberrypi.org/documentation/remote-access/ssh/)

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/ssh-file.png)
</center>

SD kartınızı Raspberry Pi cihazınıza takın, modeme bağlayın ve güç kablosunu bağlayıp çalıştırın.    

Kurulumu ağ üzerinden gerçekleştireceğimiz için Rapberry pi cihazının ip adresine ihtiyacımız olacak. Bunu birkaç farklı yolla öğrenebilirsiniz. Modeminizin arayüzünden, veya ağdaki cihaz ip'lerini tarayan bir programı bilgisayarınıza kurarak öğrenebilirsiniz.    
Ben bu işlemler için çoğunlukla "Advanced IP Scanner" programını kullanıyorum.  
Şu adresten indirebilirsiniz: [ https://www.advanced-ip-scanner.com/tr/](https://www.advanced-ip-scanner.com/tr/)   

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/ip-search.png)   
</center>

Rasberry Pi cihazımızın ip adresini öğrendiğimize göre artık cihazımızın ternminaline bağlanabiliriz. Bu işlem (SSH) için sıklıkla "PuTTY" programı kullanılıyor. Eğer Bilgisayarınızda yüklü değilse şu adresten indirebilirsiniz:  [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html )
Programı çalıştırın ve aşağıdaki ekran görüntüsündeki gibi Raspberry Pi cihazının ip adresini girin ve ardından "Open" butonu ile cihaza bağlanın.

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/putty.png)   
</center>

Eğer başarılı bir şekilde bağlanabilirseniz Rasberry Pi sizden bir şifre ve kullanıcı adı isteyecek. Varsayılan kullanıcı adı ve şifre aşşağıdaki gibidir:  

{% highlight %}
Kullanıcı adı: pi   
Şifre: raspberry    
{% endhighlight %}

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-terminal.png)   
</center>


## Pi-Hole Kurulumu 

Kurulumu "root/su" kullanıcı olarak yapmamız gerekiyor, en azından ilerleyen adımlarda sorun yaşamamak bu adımı atlamamakta fayda var.
root olarak işlem yapabilmek için aşağıdaki komutlardan birini çalıştırın:

{% highlight %}
sudo su
sudo -i
{% endhighlight %}

Pi-hole uygulamasını tek adımda otomatik olarak kurmak mümkün, kurulumu başlatmak için aşağıdaki komutu çalıştırın:

{% highlight %}
curl -sSL https://install.pi-hole.net | bash
{% endhighlight %}

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pihole-install.png)   
</center>

Kurulum sihirbazı başlayacak ve kurulum aşamadışında Pi-hole hakkında bize bazı bilgiler gösterilecek ve bazı ayarları yapmamızı isteyecek. Aslında bu ayarların büyük bir kısmını varsayılan olarak bırakacağız. Eğer farklı bir versiyon kuruyorsanız ve tereddütte kalırsanız ayarı olduğu gibi bırakın.     
Aşağıdaki gibi bilgilendirme pencerinde "ok" seçeneğini seçip geçiyoruz. 

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a1.png)  <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a2.png)  <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a3.png)  <br>
</center>


Bu adımda bir DNS sağlayıcısı seçmenizi istiyor. Genellikle  Cloudflare kullaılıyor ben de ilk kurulumda Cloudflare DNS sağlayıcısını seçtim.   

Aşağı ıve yukarı yön tuşları: listede gezinme,    
Tab tuşu: Onay menüsüne geçme,  
Space tuşu: Seçme için kullanılır.      

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a4.png)   
</center>

Pi-hole tarafından hazırlanmış  listeleri yüklemek isterseniz her iki seçeneği işaretleyin. Daha sonra kendi listelerinizi de oluşturabiliyoruz.    

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a5.png)   
</center>

Aşağıdaki pencerede ise kullanmak istediğimiz ip protokünü seçmemizi istiyor. Şu anda Türkiyede ipv6 desteklenmiyor o yüzünden sadece ipv4 seçeneğini işaretliyoruz. 

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a6.png)   
</center>

Pi-hole sunucusunun statik adresi       
<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a7.png)   
</center>

Aşağıdaki ayarları tercihinize göre değiştirbilirsiniz, ancak ilk pencedeki admin web aryüzünü kurmanızda fayda var. Ben bu ayarları olduğu gibi bıraktım.   

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a9.png)   <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/10.png)   <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a11.png)   <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a12.png)   <br>
</center>

Kurulum tamamlandında web arayüzne giriş yapabilmeniz için bir parola verecek.  Eğer parolayı değiştirmek isterseniz aşağıdaki komutu kullanabilirsiniz.    

{% highlight %}
pihole -a -p yeniparola
{% endhighlight %}

Kurulum tamamladığında  Pi-hole uygulamasına raspberry Pi cihazımızın ip adresini bilgisayarımızın web tarayısına yazarak erişebiliriz.     

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-hole-login.png)   <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-hole-admin.png)   
</center>

Pi-hole uygulamasını DNS sunucusu olarak kullanabilmek 3 tane seçeneğimiz.   
1 İç ağdaki her cihaza Pi-hole adresini DNS adresi olarak ayarlamak.  

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/ip-dns.png)   
</center>

2 Pi-hole uygulamasını DHCP sunucusu olarak ayarlamak, dns sunucuları Pi-hole yönlendirmek.    
Bunu için "settings" -> "DHCP" yolunu izleyin ve DHCP "server enabled" seçeneğini işaretleyin. 
Pi-hole aşağıdaki resimdeki gibi belirlediğinizin aralıktaki ip adreslerini pi-hole yönlendirir  bu sayede modeme bağlanan hiçbir bilgisayara yada cihaza bir ayar yapmanıza gerek kalmaz. 
Aşağıdaki resimdeki görüldüğü gibi dağıtılacak IP adresi aralığı belirleyebilirsiniz.   

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-hole-dhcp)   
</center>

Eğer Pi-hole DHCP sunucusunu kullanmaya karar verdiyseniz modemizin DHCP sunucusu devre dışı bırakın.   

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/dhcp-mod.png)   
</center>

3 Modemden DNS Sunucusu olarak pi-hole seçmek. Bu şeklildeki bir kullanımda hiçbir  cihaza (bigisayar/telefon ..) DNS ayarı yapmanıza gerek kalmaz. Bu ağa bağlanacak tüm cihazlar Pi-hole üzerinden internete bağlanır.. (Modemlerin kullanıcı ayarları birbirinden farklılık gösterir)    

<center>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/dhcp-mod2.png)   
</center>
<br>
Pi-hole birçok komut kullanır, komut satırı arayüzü kullanabileceğiniz bir kaç komut:
Tamamı: [https://docs.pi-hole.net/core/pihole-command/](https://docs.pi-hole.net/core/pihole-command/)  

