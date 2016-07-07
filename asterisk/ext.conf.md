
#ДиалПланы

ДиалПлан хело ворлд
```
[incoming]
exten => s,1,Answer()
exten => s,n,Playback(hello-world)
exten => s,n,Hangup()
```

Добавычной номер s(start) - дефолтный добавочный номер(если не указан)
```
[incoming]
exten => s,1,приложение()
exten => s,n,приложение()
exten => s,n,приложение()

exten => (номер(имя)),(приоритет(номерстроки)),(команда, приложение)
exten => 123,1,Answer()
exten => 123,n,выполнить что-то
exten => 123,n,выполнить что-то еще
exten => 123,n,выполнить последнее
exten => 123,n,Hangup()

exten => 123,n(метка),приложение()
```



##Приложенеия

filename имеет формат **.gsm**
```
Answer()
Playback()
Hangout()
Playback(/home/john/sounds/filename) :нельзя прервать
Background(/home/john/sounds/filename) ;прерывает при нажатии кнопки
exten => 123,n,WaitExten(5) ;ждать ответа 5 сек
exten => 123,n,Goto(контекст,добавочныйномер,приоритет)
exten => 123,1,Dial(Zap/1) ;вызов абона 1 по протоколу Zap
exten => 123,1,Dial(SIP/1) ;вызов абона 1 по протоколу SIP
exten => 123,1,Dial(Zap/1&Zap/2&SIP/Jane) ;звонить по нексколими каналам, любой, который ответить первым будет соединен
Dial(технология/пользователь[:пароль]@удаленный_хост[:порт][/удаленный_доба-вочный_номер]) ;связь с произвольной точкой которой нет в конфиге

```

Направление на добавчные номера WaitExten
```
exten => 123,1,Answer()
exten => 123,n,Background(main-menu)
exten => 123,n,WaitExten()
exten => 2,1,Playback(digits/2)
exten => 3,1,Playback(digits/3)
exten => 4,1,Playback(digits/4)
```

Пример goto
```
[incoming]
exten => 123,1,Answer()
exten => 123,n,Background(main-menu)
exten => 1,1,Playback(digits/1)
exten => 1,n,Goto(incoming,123,1)
exten => 2,1,Playback(digits/2)
exten => 2,n,Goto(incoming,123,1)
```

Перенаправление на номер **t** если ввода номер не было за указанное время
добавчный номер **i** когда абонент соврешает направильные(несущестующий выбор)
```
[incoming]
exten => 123,1,Answer()
exten => 123,n,Background(enter-ext-of-person)
exten => 123,n,WaitExten()
exten => 1,1,Playback(digits/1)
exten => 1,n,Goto(incoming,123,1)
exten => 2,1,Playback(digits/2)
exten => 2,n,Goto(incoming,123,1)
exten => 3,1,Playback(digits/3)
exten => 3,n,Goto(incoming,123,1)
exten => i,1,Playback(pbx-invalid)
exten => i,n,Goto(incoming,123,1)
exten => t,1,Playback(vm-goodbye)
exten => t,n,Hangup()
```


