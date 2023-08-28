Linux'daki bir diğer sorun, laptopumda touchpad ile yapılan kaydırma işleminin çok hızlı olmasıydı. Bu sorunu şu adımları izleyerek çözdüm.

Ben bu durumda Fedora Linux kullanıyordum siz kendi distronuza göre indirme işlemlerini yapabilirsiniz

Gerekli İndirmeler

```
sudo dnf install libudev-devel
sudo dnf install libinput-devel
sudo dnf install cmake
sudo dnf install gcc
sudo dnf install meson
```

Libinput-config Dosyasını indiriyoruz

```
git clone https://gitlab.com/warningnonpotablewater/libinput-config.git
cd libinput-config
```

Sonrasında bu kodları çalıştırıyoruz

```
meson setup build
cd build
ninja
sudo ninja install
```

Sonrasında "/etc/libinput.conf" dosyasını açıyoruz

```
sudo nano /etc/libinput.conf
```

ve içerisine şu kodu giriyoruz

```
scroll-factor=0.2
```

bu değeri ne kadar arttırırsanız kaydırma işlemi o kadar hızlı olur

sonrasında bilgisayarımızı yeniden başlatıyoruz

```
sudo reboot
```

