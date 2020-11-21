---
layout: post
title: "Pi-Hole Kurulum Rehberi"
date: 2020-08-17 02:30:20 +0300
description: Pi-Hole kurulumu
img: "/assets/img/pihole.png"
tags: [pi-hole, raspberry pi, DNSCrypt-Proxy, reklam engelleme]
---

<style>
img{
display: block;
margin-left: auto;
margin-right: auto;
width: 50%;
}


</style>

# Pi-Hole Nedir?

Kısaca Pi-hole, internetteki reklamları, zararlı yazılım barındıran siteleri ve izleyicileri engellemek için kullanılan açık kaynaklı ücretsiz bir yazılımdır. İsteğe bağlı olarak bir DHCP sunucusu olarak işlev görebilir ve tüm cihazların otomatik olarak korunmasını sağlar. Pi-hole, Linux üzerinde çalışan bir sunucu yazılımıdır. Yükleyip kullanabilmek için Linux çalıştıran bir bilgisayara ihtiyaç vardır. Kullanıcıların büyük bir kısmı Pi-hole yazılımını Raspberry Pi cihazına kurarlar. Biz de bu yazıda Pi-hole yazılımı Raspberry Pi üzerinde kurup çalıştıracağız. Raspberry Pi iç ağda bir DNS sunucusu oluşturur ve işin geri kalan kısmını cihaza yüklü Pi-hole yazılımı halleder. Pi-hole kullanan bir ağa bağlı tüm cihazlar ekstra bir yazılıma veya ayara ihtiyaç duymadan reklam ve izleyicilerden temizlenmiş olur. Bir web tarayıcısına reklam engelleme eklentisi kurup çalıştırmaktan farkı budur. Web tarayıcısındaki eklenti yalnızca tarayıcıdaki etkinlikleri kapsar, Pi-Hole ise üzerinden geçen geçen tüm internet trafiğini kapsar. Bu sayede mobil uygulamalar veya akıllı TV'ler gibi web tarayıcısı olmayan cihazlardaki reklamları da engeller. Aslında teknik olarak yaptığı iş kara listeye eklenmiş bir bağlantı isteği aldığında onu 0.0.0.0 ip adresine yönlendirmektir. Yazılımı sunucu sınıfı bir donanıma kurulduğunda yüz milyonlarca sorguyu yönetebilir. Pi-hole, etkinlikleri görüntülemek ve kontrol etmek için güzel bir Web Arayüzü panosuna sahiptir.

## Raspberry Pi OS Kurulumu (Eski adıyla Raspbian)

`Bu makaleyi okuduğunuza göre büyük ihtimalle bir Raspberry Pi cihazınız var ve işletim sistemi yüklü. Eğer elinizde Raspbian işletim sistemi kurulu bir Raspberry Pi varsa bu adımı geçebilirsiniz. `

Pi-hole, minimum donanım ve yazılım gereksinimleriyle sorunsuz çalışır. Raspberry Pi 2, 3, 4 veya Zero üzerinde çalışabilir. Genellikle Zero modeli tercih edilir. Pi-hole için 512MB RAM ve 4GB SD kart yeterlidir. Zero modelinin enerji tüketimi oldukça azdır ve modeminizin USB çıkış voltajıyla besleyebilirsiniz. Zero modelinde entegre bir Ethernet portu bulunmadığından, eğer modeme Ethernet kablosu ile bağlamak isterseniz bir adaptöre ihtiyacınız olacaktır.
Raspbian'ı Raspberry Pi'ya yüklerken birkaç seçeneğimiz var, ben `Raspberry Pi OS (32-bit) Lite` sürümünü kullandım. Bu sürümde bir masaüstü grafik arayüzü bulunmuyor ve herhangi bir ekrana veya klavyeye ihtiyaç duymuyor. Kurulumu ve kullanımı ağ üzerinden gerçekleştireceğiz.
Raspbian'ı şu adresten indirebilirsiniz. [https://www.raspberrypi.org/downloads/raspberry-pi-os/](https://www.raspberrypi.org/downloads/raspberry-pi-os/)
Dilerseniz farklı bir sürümü de kullanabilirsiniz ama bu işlem için en uygun seçim "Raspberry Pi OS (32-bit) Lite" olacaktır.
Kurulum dosyasını indirin ve img dosyasını "Win32DiskImager" yardımıyla SD kartınıza kurun:
Win32DiskImager İndirme Linki: [https://sourceforge.net/projects/win32diskimager/](https://sourceforge.net/projects/win32diskimager/)
img dosyasını ve kurulum yapacağınız SD kartı seçin ve "write" butonuyla imajı SD karta yazdırın.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pihole-img.png)
*Win32 Disk Imager ile SD kart kurulumu*


Kurulum tamamladıktan sonra Raspberry Pi'da SSH (Secure Shell, uzak sunucu bağlantı protokolü) etkinleştirebilmek için SD kartın boot bölümüne uzantısız SSH adlı boş bir dosya oluşturun. Raspberry Pi açıldığında boot klasöründe SSH dosyasını arar eğer dosyayı bulursa SSH etkinleştirilir ve dosya silinir. Ayrıntılı bilgiye ihtiyaç duyarsanız şu bağlantıdan 3. adıma bakabilirsiniz: [https://www.raspberrypi.org/documentation/remote-access/ssh/](https://www.raspberrypi.org/documentation/remote-access/ssh/)

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/ssh-file.png)
*SSH dosyası*

SD kartınızı Raspberry Pi cihazınıza takın, modeme bağlayın ve güç kablosunu bağlayıp çalıştırın.
Kurulumu ağ üzerinden gerçekleştireceğimiz için Raspberry pi cihazının ip adresine ihtiyacımız olacak. İp adresini birkaç farklı yolla öğrenebilirsiniz. Modeminizin arayüzünden veya ağdaki cihaz ip'lerini tarayan bir programı bilgisayarınıza/telefonunuza kurarak öğrenebilirsiniz.
Ben bu işlemler için çoğunlukla "Advanced IP Scanner" programını kullanıyorum.
Advanced IP Scanner programını şu adresten indirebilirsiniz: [ https://www.advanced-ip-scanner.com/tr/](https://www.advanced-ip-scanner.com/tr/)

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/ip-search.png)
*Advanced IP Scanner ile Raspberry Pi İp adresi öğrenme*

Raspberry Pi cihazımızın ip adresini öğrendiğimize göre artık cihazımızın terminaline bağlanabiliriz. Bu işlem (SSH) için sıklıkla "PuTTY" adlı program kullanılıyor. Eğer Bilgisayarınızda yüklü değilse şu adresten indirebilirsiniz: [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html )
Programı çalıştırın ve aşağıdaki ekran görüntüsündeki gibi Raspberry Pi cihazının ip adresini girin ve ardından "Open" butonu ile cihaza bağlanın.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/putty.png)
*PuTTY ile Raspberry Pi cihazına bağlanama ekranı*

Eğer başarılı bir şekilde bağlanabilirseniz Raspberry Pi sizden bir şifre ve kullanıcı adı isteyecek. Varsayılan kullanıcı adı ve şifre aşağıdaki gibidir:

{% highlight python %}
Kullanıcı adı: pi
Şifre: raspberry
{% endhighlight %}

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-terminal.png)
*Raspberry Pi terminali*

## Pi-Hole Kurulumu

Kurulumu "root/su" kullanıcısı olarak yapmamız gerekiyor, en azından ilerleyen adımlarda sorun yaşamamak bu adımı atlamamakta fayda var.
root olarak işlem yapabilmek için aşağıdaki komutlardan birini çalıştırın:

{% highlight bash %}
sudo su
sudo -i
{% endhighlight %}

Pi-hole uygulamasını tek adımda otomatik olarak kurmak mümkün, kurulumu başlatmak için aşağıdaki komutu çalıştırın: 

{% highlight bash %}
curl -sSL https://install.pi-hole.net | bash
{% endhighlight %}



![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pihole-install.png)
*Pi-hole kurulumunu başlatma*

Kurulum sihirbazı başlayacak ve kurulum aşamasında Pi-hole hakkında bize bazı bilgiler gösterilecek ve bazı ayarları yapmamızı isteyecek. Aslında bu ayarların büyük bir kısmını varsayılan olarak bırakacağız. Eğer farklı bir versiyon kuruyorsanız veya tereddütte kalırsanız varsayılan ayarı olduğu gibi bırakın.

Aşağıdaki gibi bilgilendirme pencerelerinde "ok" seçeneğini seçip geçiyoruz.
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a1.png) <br>

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a2.png) <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a3.png) <br>
Bu adımda bir DNS sağlayıcısı seçmenizi istiyor. Genellikle Cloudflare  kullanılıyor ben de ilk kurulumda Cloudflare DNS sağlayıcısını seçtim.

Aşağı ve yukarı yön tuşları: Listede gezinme, 
Tab tuşu: Onay menüsüne geçme,  
Space tuşu: Seçme/kaldırma için kullanılır. 

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a4.png)

Pi-hole tarafından hazırlanmış listeleri yüklemek isterseniz her iki seçeneği işaretleyin. Daha sonra kendi listelerimizi de oluşturabiliyoruz.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a5.png)

Aşağıdaki pencerede ise kullanmak istediğimiz ip protokolünü seçmemizi istiyor. Şu anda Türkiye'de ipv6 desteklenmiyor o yüzünden sadece ipv4 seçeneğini işaretleyebilirsiniz.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a6.png)

Pi-hole sunucusunun statik adresi.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a7.png)

Aşağıdaki ayarları tercihinize göre değiştirebilirsiniz, ancak ilk penceredeki admin web arayüzünü mutlaka kurun(işaretli bırakın). Ben bu ayarları olduğu gibi bıraktım.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a9.png) <br>

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a10.png) <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a11.png) <br>
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/a12.png) <br>
Kurulum tamamlandığında web arayüzne giriş yapabilmeniz için bir parola verecek. Eğer parolayı değiştirmek isterseniz aşağıdaki komutu kullanabilirsiniz.

{% highlight c %}

pihole -a -p yeniparola
{% endhighlight %}
Artık Pi-hole uygulamasına Raspberry Pi cihazımızın ip adresini bilgisayarımızın web tarayıcısına yazarak erişebiliriz.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-hole-login.png)
*Pi-Hole giriş ekranı*

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-hole-admin.png)
*Pi-Hole index sayfası*
Pi-hole uygulamasını DNS sunucusu olarak kullanabilmek 3 tane seçeneğimiz.

`1` İç ağdaki her cihaza Pi-hole adresini DNS adresi olarak ayarlamak.
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/ip-dns.png)
*Bilgisayarın DNS adresini ayarlama ekranı*

`2` Pi-hole uygulamasını DHCP sunucusu olarak ayarlamak, dns sunucuları Pi-hole yönlendirmek.

Bunu için "settings" -> "DHCP" yolunu izleyin ve DHCP "server enabled" seçeneğini işaretleyin.
Pi-hole aşağıda bulunan resimdeki gibi belirlediğiniz aralıktaki ip adreslerini Pi-hole yönlendirir bu sayede modeme bağlanan hiçbir bilgisayara ya da cihaza bir ayar yapmanıza gerek kalmaz.
Aşağıdaki resimdeki görüldüğü gibi dağıtılacak IP adresi aralığı belirleyebilirsiniz.
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/pi-hole-dhcp.png)
*Pi-hole DHCP server enabled olarak ayarlam*

Eğer Pi-hole DHCP sunucusunu kullanmaya karar verdiyseniz modemizin DHCP sunucusu devre dışı bırakın.

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/dhcp-mod.png)
*Modem arayünde DHCP ayarı*

`3` Modemden DNS Sunucusu olarak Pi-hole seçmek. Bu şekildeki bir kullanımda hiçbir cihaza (bilgisayar/telefon ...) DNS ayarı yapmanıza gerek kalmaz. Bu ağa bağlanacak tüm cihazlar Pi-hole üzerinden İnternet'e bağlanır.. (Modemlerin kullanıcı ayarları birbirinden farklılık gösterir)

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/dhcp-mod2.png)
*Modem arayünde DHCP ayarı*

<br>

Pi-hole birçok komut kullanır, komut satırı arayüzü kullanabileceğiniz birkaç komut:  
Tamamı: [https://docs.pi-hole.net/core/pihole-command/](https://docs.pi-hole.net/core/pihole-command/)
## Pi-hole Core Komutları:

{% highlight bash %}

# Beyaz listeye alma (Whitelisting):
pihole -w

# Kara listeye alma (Blacklisting):
pihole -b

# Düzenli ifade (Regex):
pihole -regex

# Hata ayıklayıcı (Debugger):
pihole debug

# Pi-hole günlüğü (Log Flush):
pihole flush

# Yeniden yapılandırma (Reconfigure):
pihole reconfigure

# Günlük izleme (Tail):
pihole tail

# Yönetici (Admin):
pihole -a
# Güncelleme (Update):
pihole updatePihole / pihole pihole -up

# Version:
pihole version / pihole -v -c

# Kurulumu kaldırma (Uninstall):
pihole uninstall

# Durum (Status):
pihole status

# Etkinletşrme & Devre dışı bırakma (Enable & Disable):
pihole enable

# DNS yeniden başlatma (Restart DNS):
# pihole restartdns
{% endhighlight %}

## Pi-hole Web Komutları:

{% highlight bash %}
# Parola (Password):
pihole -a password secretpassword

# Sıcaklık birimi (Temperature Unit):
pihole -a celsius, pihole -a fahrenheit, pihole -a kelvin fahrenheit, pihole -a kelvin

# Ana Bilgisayar Kaydı (Host Record):
pihole -a hostrecord

# E-posta adresi (Email Address):
pihole -a email admin@domain.com

# Arayüz (Interface):
pihole -a interface local
{% endhighlight %}


## DNSCrypt-Proxy Kurulumu

DNSCrypt-Proxy, anonimleştirilmiş şifrelenmiş DNS protokollerini destekleyen esnek bir DNS proxydir.  
Ben bu yazıyı yazarken en güncel sürümü "2.0.44" idi.   
Kuruluma başlamadan önce şu adresten en güncel versiyonu kontrol edebilirsiniz, kurulumu Raspberry Pi cihazına yapacağımız için `linux-arm` sürümünü seçmelisiniz.  
[https://github.com/DNSCrypt/dnscrypt-proxy/releases](https://github.com/DNSCrypt/dnscrypt-proxy/releases)  

Kululum için aşağıdaki adamları sırasıyla uygulayın.  

{% highlight bash %}
cd /opt
sudo wget https://github.com/DNSCrypt/dnscrypt-proxy/releases/download/2.0.44/dnscrypt-proxy-linux_arm-2.0.44.tar.gz
sudo tar xzvf dnscrypt-proxy-linux_arm-2.0.44.tar.gz
cd linux-arm
sudo cp example-dnscrypt-proxy.toml dnscrypt-proxy.toml
sudo nano dnscrypt-proxy.toml
{% endhighlight %}

dnscrypt-proxy.toml dosyasındaki ayarları aşağıdaki gibi değiştirin.  

53 numaralı port pi-hol tarafından kullanıldığı için listen_addresses satırındaki portu 5300 olarak değiştirin.
{% highlight bash %}
listen_addresses = ['127.0.0.1:5300']
require_dnssec = true
cache = false
{% endhighlight %}

Aşağısaki komutlar yardımıyla ayarları kurun ve çalıştırın.  
{% highlight bash %}
sudo ./dnscrypt-proxy -service install
sudo ./dnscrypt-proxy -service start
sudo setcap cap_net_bind_service=+pe dnscrypt-proxy
{% endhighlight %}

Daha sonra Raspberry Pi'yi statik bir IP adresi için yapılandırmalıyız. Bu işlem için aşağıdaki komutu girin:   

{% highlight bash %}
sudo nano /etc/dhcpcd.conf
{% endhighlight %}

`static domain_name_servers` yazan satırı aşağıdaki gibi değiştirin.  
{% highlight bash %}
static domain_name_servers=127.0.0.1
{% endhighlight %}

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/dns-set.png) 

Pi-hole ile oturum açın, Ayarlardan DNS'ye gidin. (settings -> DNS)  
Tüm `Upstream DNS Servers` seçeneklerini kaldırın.   

![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/UpstreamDNSServers.png) 

Custom 1'e (IPv4) 127.0.0.1#5300 girin ve kutuyu işaretleyin ve değişiklikleri kaydedin.  
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/custom-dns-server.png)   

Raspberry Pi'nizi yeniden başlatın. 
{% highlight bash %}
sudo reboot
{% endhighlight %}

Tüm DNS sorgularının düzgün çalıştığını ve Pi-hole'un bazı istekleri engellediğini doğrulayın. 
Aşağıdaki komutu çalıştırdığınızda xp.apple.com engelli bir adres olduğu için 0.0.0.0 döndermelidir.

{% highlight bash %}
nslookup xp.apple.com 
{% endhighlight %}

Eğer DNSCrypt-Proxy başarılı bir şekilde çalışıyorsa aşağıdaki gibi bir sonuç döndermelidir.  
![Pi-hole]({{site.baseurl}}/assets/img/pi-hole/DNSCrypt-Proxy-test.png)   

