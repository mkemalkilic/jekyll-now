---
layout: post
title: "ArchLinux GRUB, Syslinux Kurtarma"
date: 2017-04-04 
comments: true
---

2006 yılından beri GNU/Linux’u kişisel bilgisayarımda ana işletim sistemi olarak kullanıyorum. Şimdiye kadar Windows’u Catia, Ansys, Solidworks gibi GNU/Linux sürümü bulunmayan programlar için kullandım genelde. Neden GNU/Linux sorusunun cevabı ayrı bir yazının konusu olsun. Şimdilik, yılda bir kaç defa karşılaştığım bir sorunla ilgili hem bana not olarak burada bulunsun hem de aynı sorunla karşılaşan insanlara faydası olsun diye yazıyorum.

2010 yılından itibaren ise Windows7 ile beraber [Arch Linux](https://www.archlinux.org/) kullanıyorum ve yılda bir iki kere Windows’u formatlıyorum. Windows’u formatlayınca da bildiğiniz üzere Windows’un kendi önyükleyicisi GRUB’u yok sayıyor. Bu nedenle format sonrası GNU/Linux’a boot edemiyorsunuz sistemi. Eğer Windows üstüne GNU/Linux dağıtımını kurduysanız zaten sorun yok.

Bir çok yerde, Arch Linux için de, sorunun çözümü açıklanmış ama burada derli toplu dursun istiyorum. Bu arada aşağıdaki komutlar **MBR** (Master Boot Record) spesifik komutlar.

- Öncelikle güncel Arch Linux live .iso’sunu indirip USB belleğe aktarıyoruz. (Bunların nasıl yapılacağını anlatmama gerek yok sanırım, Arch Linux kullanıyorsanız zaten az çok biliyorsunuzdur)
- Sistemi hazırladığımız live iso’dan boot ediyoruz.
- Sistem açıldığında bu komut ile Türkçe klayveyi tanıtıyoruz.
{% highlight bash %}
    $ loadkeys trq
{% endhighlight %}
- Disk bölümlendirmenizi hatırlamıyorsanız bu komutu kullanabilirsiniz.
{% highlight bash %}
    $ lsblk /dev/sda
{% endhighlight %}
Daha sonra şu komutları sırasıyla veriyoruz:

- (GRUB için)
{% highlight bash %}
    $ mount /dev/sdaX /mnt        #sdaX, "root" bölümünüz.
    $ mount /dev/sdaY /mnt/boot   #sdaY, ayrı bir "boot" bölümünüz varsa.
    $ arch-chroot /mnt
    $ grub-install --target=i386-pc /dev/sda
    $ grub-mkconfig -o /boot/grub/grub.cfg
    $ exit
    $ umount /mnt/boot
    $ umount /mnt
    $ reboot
{% endhighlight %}

- (Syslinux için)
{% highlight bash %}
    $ mount /dev/sdaX /mnt        #sdaX, "root" bölümünüz.
    $ mount /dev/sdaY /mnt/boot   #sdaY, ayrı bir "boot" bölümünüz varsa.
    $ arch-chroot /mnt
    $ syslinux-install_update -i -a -m
    $ exit
    $ umount /mnt/boot
    $ umount /mnt
    $ reboot
{% endhighlight %}






