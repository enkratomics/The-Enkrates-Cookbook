# Интернет-зависимость и её преодоление
```Введение.```

## Стратегии

```Cold turkey vs. gradual, немного теории; пари, денежный коммитмент```

## Простой путь: закрытие доступа к нежелательным сайтам через файл hosts

> Это пробная заметка Текстора, рассмотрение частного случая.

_Дваче- (и специфично политаче-) зависимость – застарелая привычка, которая не преодолевается надёжно никакими волевыми методами, так как может инициализироваться без осознания (скажем, при проседании внимания от усталости/стресса, в очереди и т.д.), и далее усугубляет ситуацию, приведшую к её инициализации; если смотреть на тайм-трек, она совсем не тратит время только в очень удачные отчётные периоды полной загрузки и бесшовных цепочек осмысленных действий. Также общение на пораше делает меня а) узко и шаблонно мыслящим животным б) большим мизантропом, чем мне имеет смысл быть. Браузерные плагины недостаточны, т.к. у меня есть m$ edge и мобильные девайсы. tl;dr хватит это терпеть.  
«Почему» не нужны двачи – пояснять нет настроения. Так что интерпретирую это как вопрос "почему hosts".  
Это простое мейнстримное решение, которое приемлемо работает у многих людей и которому я иррационально сопротивлялся, выдумывая чепуху типа "а вот гаджеты, а я обратно отредактирую, надо на СИЛЕ ВОЛИ".  
Думаю, **можно принять за общий принцип, что так [через упрямый отказ от рабочего мейнстримного подхода] проявляется самая банальная акразия**, в которой я стыжусь себе признаться._

---

* **Windows**
    * `C:\Windows\System32\drivers\etc` (если не было перемещений; по ссылке ниже инструкции на иной случай).
        * Для изменения файла `hosts` необходимо открыть его в текстовом редакторе, запущенном от имени Администратора.
        * Для редактирования файла hosts просто добавьте подряд новые строки, которые должны выглядеть как IP-адрес, один или несколько пробелов, адрес сайта (URL, который будет перенаправляться на указанный IP-адрес).
        * _From: [remontka.pro](http://remontka.pro/hosts-file-windows-10/)._
    * Also, make sure to place an extra line after the last entry for the section. _From: [howtogeek.com](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/)._
    * Changes to hosts should take effect immediately, but Windows caches name resolution data so for some time the old records may be used. Open a command line (Windows+R, cmd, Enter) and type to drop the old data
        * `ipconfig /flushdns`
        * To check if it works, use (assuming you have an ipv4 entry in your hosts for www.example.com, or an ipv6 entry in your hosts for ipv6.example.com):
            * `ping www.example.com -n 1`
            * `ping -6 ipv6.example.com -n 1`
            * And see if it uses the correct IP. If yes, your hosts file is fine and the problem is elsewhere.
        * Also, you can reset the NetBios cache with (open the console as an admin or it will fail):
            * `nbtstat -R`
    * _From: [serverfault.com](https://serverfault.com/questions/452268/hosts-file-ignored-how-to-troubleshoot)_
* **macOS**
    * `sudo nano /private/etc/hosts`
    * When finished, hit Control+O followed by ENTER/RETURN to save changes to /private/etc/hosts, then hit Control+X to exit out of nano
    * Changes take effect immediately though some adjustments may need to be accompanied by a DNS flush which can be done with the following command in macOS 10.12+ through OS X 10.9:
    * `dscacheutil -flushcache;sudo killall -HUP mDNSResponder`
    * _From: [osxdaily.com](http://osxdaily.com/2012/08/07/edit-hosts-file-mac-os-x/)_
* **Android**
    * В Android файл hosts находится по следующему пути: `/system/etc/hosts`
    * Для того, чтобы поменять файл hosts, в Android необходимо сначала получить права root, также для некоторых устройств требуется снять защиту с системного раздела (s-off). При наличии прав сделать это в Android можно, например, с помощью текстового редактора, встроенного в Root Explorer.
    * _From: [android-manual.org](http://android-manual.org/level2/android-hosts-file)_
    * Примечание: Chrome и другие браузеры с функцией «экономии трафика» (не только мобильные) обходят hosts для сайтов без https. 
* **iOS**
    * C джейлбрейком: 
        * Cydia – iFile
        * В root (/) лежит файл hosts
        * Редактировать приложением вроде Text Viewer
        * *From: [daveden](https://daveden.wordpress.com/2013/01/16/how-to-edit-the-hosts-file-in-ios/amp/)*
    * Без: no[t possible]. Apps can only modify files within the documents directory, within their own sandbox. This is for security, and ease of installing/uninstalling. So you could only do this on a jailbroken device. * _From: [stackoverflow.com](https://stackoverflow.com/questions/4783923/can-i-edit-an-ipads-host-file)_
* **В общем случае:** Умные люди рекомендуют действовать на уровне роутера.

С первой попытки не получилось, мне некогда выяснять детали. На всякий случай вписал все варианты и в какой-то момент неугодные сайты были заблокированы на всех доступных девайсах. Финальная версия списка:

```
127.0.0.1 https://2ch.hk
127.0.0.1 2ch.hk
127.0.0.1 mangareader.net
127.0.0.1 www.mangareader.net
127.0.0.1 mangahere.co
127.0.0.1 www.mangahere.co
127.0.0.1 m.mangahere.co
```

## Расширения браузеров и другие инструменты