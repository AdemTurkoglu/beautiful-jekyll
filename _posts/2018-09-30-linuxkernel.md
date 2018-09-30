---
layout: post
image: /img/ubuntu.png
title: Compiling linux kernel as open source
subtitle: Linux Kernel Upgrade
tags: [linux, sistem, programlama, kernel, upgrade]
gh-repo: ademturkoglu/ademturkoglu.github.io
gh-badge: [star, fork, follow]
---
Kernel kurulumu için öncelikle güncel kerneli indirmemiz gereklidir. [Buradan](http://www.kernel.org/) güncel kerneli indirebilirsiniz. 

![Kernel](/systemprograming/kernelorg.png)

İndirme işleminden sonra terminali (Ctrl+Alt+t) açıyoruz. 

{: .box-note}
**sudo -i**

Komutuyla root kullanıcıya geçiyoruz. Bu işlem için yönetici şifresi isteyecektir!
İndirdiğimiz kerneli **/usr/src** dizinine kopyalamamız gerekiyor. Bu dizine ara yüzden erişilememektedir. Bunun için terminale 

{: .box-note}
**cp /home/adem/dowloads/linux-4.18.10.tar.xz /usr/src** 

Komutunu girmek yeterlidir.

![Sudo](/systemprograming/sudoi.png)

Şimdi kopyalamayı yaptık , dosyayı çıkartmamız gerekecek.
**Cd /usr/src** ile o dizine gidiyoruz.

{: .box-note}
**tar –xJvf linux-4.18.10.tar.xz**

Komutunu çalıştırarak kerneli çıkartıyoruz.

![KernelCikar](/systemprograming/kernelcikar.png)

Çıkartma işleminden sonra linux-4.18.10 adında klasör oluşturuldu.
**Cd linux-4.18.10** komutunu girerek o dizinin içine giriyoruz.

![Cd](/systemprograming/cd.png)

Şimdi derleme işlemine başlıyoruz fakat öncesinde temiz bir kurulum yapmak için
eski, default ayarları temizleyelim. **make mrproper** Komutu ile eski ayarlar temizleniyor.

![Mrproper](/systemprograming/mrproper.png)

Ayar penceresini açmak için  komutunu çalıştırıyoruz.

{: .box-note}
**make menuconfig**

Komutunu çalıştırdığımızda **“curses.h”** kütüphanesi yüklü olmadığı için bir hata alırsak hata çözümü için 

{: .box-note}
**sudo apt-get install libncurses-dev**

Komutunu çalıştırarak gerekli olan kütüphanesini eklememiz gerekir.

![Curses.h](/systemprograming/cursesh.png)

Tekrar **make menucofig** dediğimizde bison: not found hatası aldık.

![bison](/systemprograming/bison.png)

{: .box-note}
**apt-get install bison** 

Komutu ile bison kurulumu yapıyoruz. Tekrar make menuconfig komutunu giriyoruz.

![flex](/systemprograming/flex.png)

Bu seferde flex not found şeklinde bir hata aldık.

{: .box-note}
**apt-get install flex** 

Komutu ile flex kurulumu yaptık tekrar make menuconfig girdiğimizde hata almadık.

![menuconfig](/systemprograming/menuconfig.png)

Bu menüden istediğiniz değişikliği yapabilirsiniz, ben bir değişiklik yapmadan ayarları kaydediyorum. 

## Çekirdek İmajı Derleme

Şimdi çekirdek imajını derlemeye geçiyoruz bunun için 

{: .box-note}
**make bzImage** 

Komutunu giriyoruz.

Komutu girdiğimizde çekirdek imajını derlemek için gerekli kütüphanenin olmadığına dair bir hata alıyoruz. 

![hata](/systemprograming/hata.png)

{: .box-note}
**sudo apt-get install libssl-dev** 

Komutunu çalıştırarak gerekli kütüphaneyi ekliyoruz ve **make bzImage** komutunu tekrar giriyoruz. Çekirdek imajını derlemesi yaklaşık 15-20 dakika sürebilir.

## Modül Derleme

Çekirdek imajı derlendikten sonra sıra modülleri derlemeye geçiyor.Bunun için 

{: .box-note}
**make modules** 

![makemodules](/systemprograming/makemodules.png)

Komutunu çalıştırıyoruz. Bu işlem yaklaşık 2 saat sürebilmektedir.

Modülleri derleme işlemi bittikten sonra modüllerimizi yükleyebiliriz.Yükleme işlemini 

 ![modulesinstall](/systemprograming/modulesinstall.png)
 
{: .box-note}
**make modules_install**
**make install**

 ![install](/systemprograming/install.png)
 
Sırayla komutları ile yapıyoruz.
İşlemimiz tamamlandıktan sonra bilgisayarımızı restart edebiliriz.

Açıldığı zaman terminalde 

{: .box-note}
**uname –r**

Komutunu çalıştırak sürüm kontrol edebiliriz.

 ![final](/systemprograming/final.png)
