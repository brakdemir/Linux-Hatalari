Linux'daki bir diğer sorun, laptopumda tarayıcılarda touchpad ile yapılan kaydırma işleminin çok hızlı olmasıydı. Bu sorunu şu adımları izleyerek çözdüm.

Chromium tabanlı tarayıcılar

```
1.brave://flags/ a gidin 
2.Windows Scrolling Personality yazın 
3.değeri Defult olarak gelir değeri Enabled yapın
4.brave'i yeniden başlatın
```

Firefox

```
1.about:config e gidin
2.mousewheel.default.delta_multiplier_y yazın
3.değeri 100 olarak gelir değeri 15 ile 20 arasına bir değer yapın
4.firefox'u yeniden başlatın
```
