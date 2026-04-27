# CLAUDE.md — правила роботи з репозиторієм ngpu.org

## Коміти та PR

- **Не додавати** в коміти та описи PR посилання виду `https://claude.ai/code/session_...` — вони публічні і не потрібні.
- **Не додавати** рядки `Co-authored-by: Claude <noreply@anthropic.com>` — вони теж публічні.
- До кожного PR додавати скриншот зміненої сторінки (інструкція нижче в розділі «Скриншоти»).

## Гілки та Pull Request

- **Кожна зміна — новий PR.** Після того як PR злито або закрито, створювати нову гілку для наступної зміни.
- Ніколи не пушити нові коміти в гілку вже закритого або злитого PR.
- Гілки називати описово, наприклад: `claude/fix-about-page`, `claude/add-news-article`.
- Завжди пушити в гілку командою `git push -u origin <branch-name>`.
- **Не створювати PR без явного запиту користувача.**

## Деструктивні операції

- `git reset --hard`, `git push --force` та інші незворотні операції — тільки після явного підтвердження користувача.
- Перед скиданням гілки завжди показувати, до якого коміту і що буде втрачено.

## Технічний стек

- Генератор статичних сайтів: **Hugo** (версія 0.160.1)
- Тема: `themes/ngpu-newsroom` (кастомна)
- Публікація: GitHub Actions → GitHub Pages при пуші в `main`
- Мова сайту: українська (uk-UA)

## Структура контенту

| Папка | Призначення |
|-------|------------|
| `content/news/` | Новини (один `.md` файл — одна новина) |
| `content/documents/` | Офіційні документи |
| `content/about/_index.md` | Сторінка «Про профспілку» |
| `content/contacts/_index.md` | Сторінка «Контакти» |
| `static/img/news/` | Зображення для новин |

## Зображення

- Рекомендований розмір: **800px** по ширині, пропорційно по висоті.
- Формат: JPEG або PNG.
- При ресайзі зберігати оригінальне співвідношення сторін.

## Скриншоти перед PR

До кожного PR додавати скриншот зміненої сторінки. Процес:

```bash
# 1. Зібрати сайт
hugo --minify --quiet

# 2. Запустити локальний HTTP-сервер
python3 -m http.server 1313 --directory public &

# 3. Зробити скриншот через Playwright
node -e "
const { chromium } = require('/opt/node22/lib/node_modules/playwright');
(async () => {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  await page.setViewportSize({ width: 1440, height: 900 });
  await page.goto('http://localhost:1313/about/');  // змінити URL на потрібний
  await page.screenshot({ path: '/tmp/preview.png', fullPage: true });
  await browser.close();
})();
"

# 4. Зупинити сервер
kill $(lsof -ti:1313)
```

Скриншот зберігати у `.github/screenshots/` і коммітити разом зі змінами.  
У PR вставляти як:
```markdown
![назва](https://raw.githubusercontent.com/shaposhnikoff/ngpu.org/<branch>/.github/screenshots/preview.png)
```

## Кастомні layout-и

Кастомні layout-и для розділів розміщувати у `layouts/<section>/list.html` (рівень проєкту, не теми).
