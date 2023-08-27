Linux'da karşılaştığım başka bir sorun ise bilgisayarımı uyku moduna alıp tekrar başlattığımda faremin çalışmamasıydı. Bunu düzeltmek için şu adımları izledim.

1.Aşağıdaki kodu '/usr/local/bin/reset-input-devices.sh' dosyasını oluşturup koydum.

```
#! /bin/sh
# Reset the keyboard driver and USB mouse 
        
modprobe -r atkbd
modprobe atkbd reset=1
echo "Finished resetting the keyboard."
        
# Reset every USB device, because we don't know in advance which port
# the mouse is plugged into. Send errors to /dev/null to avoid 
# cluttering up the logs.
for USB in /sys/bus/usb/devices/*/authorized; do
    eval "echo 0 > $USB" 2>/dev/null 
    eval "echo 1 > $USB" 2>/dev/null
done
echo "Finished resetting USB inputs."
```


2.Root olarak çalıştırılması gerektiğinden, izinleri şu şekilde ayarladım:

```
cd /usr/local/bin/
sudo chown root:root reset-input-devices.sh
sudo chmod 744 reset-input-devices.sh
```

3.Bu betiğin uyku işleminden sonra çalışmasını sağlamak için bir systemd servisi kullandım.  
Bunun için /etc/systemd/system/ dizininde bir hizmet dosyası oluşturdum.
Bu bağlamda /etc/systemd/system/reset-input-devices-after-sleep.service dosyasını oluşturdum. içeriği bu şekilde ayarladım:


```
# This service is used to work around an apparent bug that freezes 
# keyboard and mouse inputs after waking from sleep.
            
[Unit]
Description=Reset the keyboard and mouse after waking from sleep
After=suspend.target hibernate.target hybrid-sleep.target suspend-then-hibernate.target
            
[Service]
ExecStart=/usr/local/bin/reset-input-devices.sh
CPUWeight=500
           
[Install]
WantedBy=suspend.target hibernate.target hybrid-sleep.target suspend-then-hibernate.target
```


4.Ardından, hizmeti hem şimdi hem de her yeni önyüklemeden sonra uykudan dönüş olayına yanıt vermeye hazır olacak şekilde etkinleştirdim:

```
cd /etc/systemd/system/
systemctl enable --now reset-input-devices-after-sleep.service
```
