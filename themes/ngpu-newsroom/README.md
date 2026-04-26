# ngpu-newsroom

Hugo-тема для сайту Укрнафтогазпрофспілки. Редакційний (newsroom) стиль із класичною серифною типографікою.

## Структура

```
themes/ngpu-newsroom/
├── theme.toml
├── README.md
├── archetypes/
│   ├── default.md
│   └── news.md
├── assets/
│   └── scss/
│       ├── main.scss
│       ├── _tokens.scss
│       ├── _base.scss
│       ├── _masthead.scss
│       ├── _components.scss
│       ├── _home.scss
│       ├── _list.scss
│       ├── _article.scss
│       └── _footer.scss
├── layouts/
│   ├── _default/
│   │   ├── baseof.html
│   │   ├── list.html
│   │   ├── single.html
│   │   └── article.html
│   ├── index.html
│   ├── partials/
│   │   ├── masthead.html
│   │   ├── footer.html
│   │   ├── breaking.html
│   │   ├── card-news.html
│   │   ├── card-document.html
│   │   ├── theme-switch.html
│   │   └── head.html
│   ├── shortcodes/
│   │   ├── pullquote.html
│   │   ├── kicker.html
│   │   ├── photo.html
│   │   ├── stats.html
│   │   └── numbered.html
│   └── 404.html
└── static/
    └── favicon.svg
```

## Швидкий старт

```bash
# 1. створити сайт
hugo new site mysite
cd mysite

# 2. встановити тему як subtree або submodule
git submodule add <url> themes/ngpu-newsroom

# 3. підключити
echo 'theme = "ngpu-newsroom"' >> hugo.toml

# 4. запустити
hugo server
```

## Конфігурація (приклад `hugo.toml`)

```toml
baseURL = "https://ngpu.org.ua/"
languageCode = "uk-UA"
title = "Укрнафтогазпрофспілка"
theme = "ngpu-newsroom"

[params]
  description = "Профспілка працівників нафтової і газової промисловості України"
  established = 1992
  members = "174 312"
  primaries = 412
  regions = 22
  hotline = "+380503208035"
  accent = "blue"   # ochre | blue | red | forest | ink
  mode = "light"    # light | dark

  [params.contacts]
    address = "Київ, Майдан Незалежності, 2, к. 617"
    phone1 = "+38 (044) 205-74-63"
    phone2 = "+38 (044) 205-74-60"
    email = "info@ngpu.org.ua"

[menu]
  [[menu.main]]
    name = "Головна"
    url = "/"
    weight = 10
  [[menu.main]]
    name = "Новини"
    url = "/news/"
    weight = 20
  [[menu.main]]
    name = "Профспілка"
    url = "/about/"
    weight = 30
  [[menu.main]]
    name = "Охорона праці"
    url = "/labour-safety/"
    weight = 40
  [[menu.main]]
    name = "Соціальний діалог"
    url = "/social-dialogue/"
    weight = 50
  [[menu.main]]
    name = "Молодіжна політика"
    url = "/youth/"
    weight = 60
  [[menu.main]]
    name = "Документи"
    url = "/documents/"
    weight = 70
  [[menu.main]]
    name = "Контакти"
    url = "/contacts/"
    weight = 80
```

## Типи контенту

- `content/news/*.md` — новини (archetype `news.md`)
- `content/documents/*.md` — документи (PDF, статут, угоди)
- `content/about/_index.md` — сторінка «Про профспілку»
- `content/contacts/_index.md` — контакти

### Front matter новини

```yaml
---
title: "Сергій Бизов має очолити нове покоління профспілкових лідерів"
date: 2026-03-19T10:42:00+02:00
category: "Профспілковий рух"
author: "Прес-служба"
lede: "Центральна рада одноголосно висунула…"
photo: "/img/news/byzov.jpg"
photo_caption: "Засідання Центральної ради · 19.03.2026"
photo_credit: "Фото · О. Романюк"
tags: ["ФПУ", "З\u2019їзд", "Лідерство"]
featured: true
breaking: false
---
```

## Налаштування теми та акценту

Тема (`light` / `dark`) і акцентний колір (`ochre`, `blue`, `red`, `forest`, `ink`) задаються в `[params]` або через перемикач у шапці. Користувацький вибір зберігається в `localStorage`.

## Шорткоди

- `{{</* kicker accent="true" */>}}Профспілковий рух{{</* /kicker */>}}`
- `{{</* pullquote author="С. Бизов" */>}}…цитата…{{</* /pullquote */>}}`
- `{{</* photo src="..." caption="..." credit="..." */>}}`
- `{{</* stats */>}}` — генерує блок цифр з `[params]`
- `{{</* numbered */>}}1. Колективні договори :: Опис...{{</* /numbered */>}}`
