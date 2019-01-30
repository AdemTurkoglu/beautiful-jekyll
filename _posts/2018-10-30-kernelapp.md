---
layout: post
image: /img/ubuntu.png
title: Modul Programlama
subtitle: Dışarıdan parametre olarak text alan ve tersine çevirip kernel loglarına yazan program.
tags: [linux, sistem, programlama, kernel, moduleprograming]
gh-repo: ademturkoglu/ademturkoglu.github.io
gh-badge: [star,follow]
---
Kernel modülü, kernele sonradan eklenip çıkartılabilen kodlardır. C ile geşliştirilen Kernel Modülleri aslında sıradan bir programdan çok da farklı değildir. Kernelinizde kurulu olan modülleri lsmod komutuyla görebilirsiniz.

**Neden Modül Kullanmalıyız ?**

Linux’da donanımlar kernel sürücüleri tarafından kullanılırlar. Bu modüller genellikle lib/modules dizisi altında bulunurlar ve açılış anında yüklenirler. Sistem içerisinde hazır modüller olduğu gibi kendimiz de modül ekleyebiliriz. Kernelin fonksiyonelliğini sistemi yeniden başlatmadan modüller sayesinde arttırılabilir. Bir donanım sürücüsünü düşünecek olursak, sürücü ile kernel, sistem ve donanım arasındaki bağlantıyı sağlayacaktır. Fakat bu işlem için kernele eklenti yapmamız gerekecektir. Kernele yapılacak her hangi bir müdahalede, kernelin tekrar derlenmesi ve sistmein yeniden başlatılması gerekir. Suncu sistemleri gibi sürekli açık kalması gereken bilgisayarlar için yeniden başlatma işlemi istenmeyen bir durumdur. Bu tip durumları önlemek için modüller kullanılmaktadır.

Şimdi kernel katmanında çalışan basit bir uygulama yazalım.
Kendime modules diye bir klasör oluşturdum ve içerisin bir .c uzantılı c kod dosyası oluşturdum.
module_param(inputname, charp,0000) methodu sırayla değişken ismi, türü ve 0000 rakamı ile yetki derecesini parametre olarak alıyor.
Init fonksiyonu main fonk. gibi düşünebiliriz.
Exit fonk. ise tahmin edilebileği üzere programdan çıkışta kernel loglarına çıkış yapıldığına dair log basmakta.

![Ccode](/systemprograming2/ccode.png)

Makefile dosyaları genellikle bir veya birden fazla kaynak kod dosyasından oluşan yazılım projelerini derlememizi kolaylaştırmaya yarar.

MakeFile dosyamızı oluşturuyoruz. Terminalden "gedit Makefile" komutu ile de oluşturabilirsiniz.

![Ccode](/systemprograming2/makefile.png)

Artık make komutu ile modülü derleyebiliriz.

{: .box-note}
**sudo -s** 

Komutuyla root kullanıcısına geçiyoruz.

![Ccode](/systemprograming2/make.png)

Derledikten sonra birkaç dosya oluşuyor. StringReverser.ko adında dosya oluştuğunu görüyoruz.
Oluşan modülümüzü yükleyebiliriz.

{: .box-note}
**insmod StringReverser.ko InputString='Budenemeicinyazildi'** 

Komutu ile modülü yüklüyoruz.

![Ccode](/systemprograming2/insmod.png)


{: .box-note}
**dmesg** 

 komutu ile log a bakıyoruz.
 
 ![Ccode](/systemprograming2/dmesg.png)
 
 {: .box-note}
 **rmmod StringReverser** 
 
 Komutu ile modülü kaldırıyoruz,Başarılı bir şekilde kaldırılmışsa logları kontrol ettiğimizde "String Reversed" yazdığını görebiliriz.
 
![Ccode](/systemprograming2/rmmod.png)
  
![Ccode](/systemprograming2/dmesg2.png)
 
 

 
 





