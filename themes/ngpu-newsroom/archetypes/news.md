---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
category: ""
author: "Прес-служба"
lede: ""
photo: ""
photo_caption: ""
photo_credit: "Фото · Прес-служба"
tags: []
featured: false
breaking: false
---

Текст матеріалу. Підтримуються шорткоди:

{{</* pullquote author="Автор цитати" */>}}
Текст пул-цитати на повну ширину колонки.
{{</* /pullquote */>}}

{{</* photo src="/img/news/foo.jpg" caption="Підпис" credit="Фото · Автор" */>}}
