Linux'u Asus laptopuma yükledikten sonra karşılaştığım sorunlardan biri ise bilgisayarım her açıldığında FN tuşunun aktif olarak gelmesiydi. Bunun kapatmak için şu adımları izledim.

1.Terminalde bu kodu çalıştırdım.

```
ls /etc/modprobe.d
```

2.içerisinde "appletalk-blacklist.conf" dosyasının olduğunu gördüm.

3.dosyayı nano ile açtım.

```
sudo nano /etc/modprobe.d/appletalk-blacklist.conf
```

4.Ve dosyanın sonuna bu kodu ekledim 

```
options asus_wmi fnlock_default=N
```

5.Sonrasında makineyi yeniden başlatmak için bu kodu çalıştırdım.

```
$ sudo update-initramfs -u -k all; reboot
```

ve düzeldi umarım işinize yaramıştır.
