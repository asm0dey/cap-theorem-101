---
marp: true
title: "Introduction to CAP theorem"
url: https://asm0dey.ru/p/devops-de
theme: gaia
size: 4K
class: default
backgroundImage: "linear-gradient(to bottom, #000 0%, #1a2028 50%, #293845 100%)"
color: white
paginate: true
footer: '[![](images/twitter_24.png)asm0di0](https://twitter.com/asm0di0)'
---
<style>
.hljs-variable { color: lightblue }
.hljs-string { color: lightgreen }
</style>
<!--
_class: lead
_paginate: false
_footer: ""
-->

# <!-- fit --> CAP Theorem 101

---
<!--
_class: lead
-->
# Кто я

- 14 лет в IT
- Сначала админ
- Потом разработчик
- И всё это время работаю с распределёнными системами

---

<!-- _class: lead -->
# А что такое распределённые системы:question:

---
# <!-- fit --> А что такое распределённые системы?

> Распределённая система — система, для которой отношения местоположений элементов (или групп элементов) играют существенную роль с точки зрения функционирования системы, а следовательно, и с точки зрения анализа и синтеза системы. 
> -- [Wikipedia][1]

[1]: https://ru.wikipedia.org/wiki/%D0%A0%D0%B0%D1%81%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D1%91%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0?oldformat=true

---
<!-- _class: lead -->

# <!-- fit --> :zzz:

---
<!-- _class: lead -->

# <!-- fit --> Попробуем попроще

* Много серверов
* Много сервисов
* **Много процессов!**

---

# И?

**Что-то может пойти не так**

CAP-теорема рассказывает о том, что пойдёт не так и к чему надо готовиться.

Так что же это за волшебные буквы?

---
<!--
_class: lead
_color:  #cd65a5 
-->
![bg cover opacity:60%](https://source.unsplash.com/1LwpTfvW4C0)
# C for Consistency



---
# C for Consistency

![bg right:20%](https://source.unsplash.com/rsqiJhaPDz8)

ACID:
* Данные соответствуют бизнес-правилам

---
# C for Consistency

![bg right:20%](https://source.unsplash.com/rsqiJhaPDz8)

ACID:
- Данные соответствуют бизнес-правилам

CAP:
* Все процессы содержат одни и те же данные
* Linearizability

---

![bg contain saturate](https://vladmihalcea.com/wp-content/uploads/2018/05/LinearizabilitySingleNode.png)

---
<!-- _class: lead -->

# <!-- fit --> :stop_sign:Но это НЕ распределённая система

Рассмотрим Postgres :elephant: с асинхронной репликацией

---

![bg contain saturate](https://vladmihalcea.com/wp-content/uploads/2018/05/Linearizability.png)

---
<!-- _footer: "" -->
# <!-- fit --> Thanks Vlad Mihalcea for these images

They are from his excellent book

You can buy it at https://vladmihalcea.com/books/high-performance-java-persistence/

Also please subscribe to his blog at https://vladmihalcea.com

![bg right:33% fit](https://d1b14unh5d6w7g.cloudfront.net/973022823X.01.S001.LXXXXXXX.jpg?Expires=1591609263&Signature=RFMeyJanTEb03LwZjOMJ3tKU6S3zJmDe7cBUYBHgKTnySBdZaCvIRnWZ49oaDSat51yitLbAwrJatUUG5+I4XtxAT/6isR+dvvMauP7kLqeSOufeDgy9dWGg4iiW8xknW9w1ohzU7fTFHfjnDOTnC+LBVnJkvyQeP9FdZzAz4b4=&Key-Pair-Id=APKAIUO27P366FGALUMQ)

---
<!-- _class: lead -->
# Consistency

Это когда данные так просто не испортишь потому что всё со всем синхронизировано :smile:

---
# A for Availability
![bg](https://source.unsplash.com/g3ag5r0NKWM)

---
# A for Availability

Как думаете, что такое доступность?

---

# A for Availability

Что такое доступность? Ответ должен прийти!

А за сколько? Голосуем!

---
<!-- _class: lead -->
# A for Availability

Ответ должен прийти

**Когда-нибудь**
**Какой-нибудь**

![bg left:60%](https://source.unsplash.com/mSESwdMZr-A)

---
# P for «Partition tolerance»
![bg](https://source.unsplash.com/E8H76nY1v6Q)

---
### P for «Partition tolerance»

* Сети не бывают идеальными
* Даже если админы говорят иначе
* **Особенно** если админы говорят иначе

![bg right:40%](https://source.unsplash.com/dMNee_epAnw)

---
### P for «Partition tolerance»

- Сети не бывают идеальными
- Даже если админы говорят иначе
- **Особенно** если админы говорят иначе

Partition tolerance — когда система продолжает работать даже если сединения между серверами нет

![bg right:40%](https://source.unsplash.com/dMNee_epAnw)

**Как-нибудь**

---
<!-- _class: lead -->
# Так что же это за теорема?

---


![bg contain](https://miro.medium.com/max/2560/1*PRIuXsw1KdbxQ-ho_yuNVA.png)

---
<!-- _class: lead -->
# Критика

https://jvns.ca/blog/2016/11/19/a-critique-of-the-cap-theorem/

---

<!-- footer: "" -->
![bg contain](https://jvns.ca/images/drawings/cap.svg)

---

# Критика

Критика заключается в том, что CAP-теорема даёт нам мало знания.

Но так ли это? С моей точки зрения нет!

Потому что CAP нам говорит о том, что произойдёт в worst-case scenario!

---

# Например?

* В Postgres с асинхронной репликацией вы получите неконсистентные данные
* С синхронной — не получите вообще
* В RabbitMQ потеряете часть данных, а часть получите много раз
* В кассандре получите не то, что исали

---

<!-- _class: lead -->
# <!-- fit --> Так просто?

---

<!-- _class: lead -->
# <!-- fit --> НЕТ
![bg brightness:0.3](https://source.unsplash.com/WPrTKRw8KRQ)

---

# PACELC

> Теорема PACELC — расширение теоремы CAP, которое гласит, что в случае разделения сети (P) в распределённой компьютерной системе необходимо выбирать между доступностью (A) и согласованностью (C) (согласно теореме CAP), но в любом случае, даже если система работает нормально в отсутствии разделения (E), нужно выбирать между задержками (L) и согласованностью (C). 
> -- [Wikipedia][1]

[1]: https://ru.wikipedia.org/wiki/%D0%A2%D0%B5%D0%BE%D1%80%D0%B5%D0%BC%D0%B0_PACELC?oldformat=true


---

<!--
_theme: white
_background: white
_backgroundImage: "linear-gradient(to bottom, #fff 0%, #fff 50%, #fff 100%)"
_color: black
-->

![bg fit](images/pacelc.png)

# PACELC

---

# Выводы?

* Знай CAP теорему
* Знай где твоя система в ней
* Не обманывайся — ты не достигнешь CAP

---

# Что почитать?

* Aphyr
* Тесты Jepsen https://jepsen.com
* Блог Джулии Эванс https://codahale.com/you-cant-sacrifice-partition-tolerance/

---

<!-- _class: lead -->

![bg left](https://source.unsplash.com/sitjgGsVIAs)

# Спасибо!

@asm0dey всюду
@asm0di0 ![](images/twitter_24.png)
https://newpodcast2.live