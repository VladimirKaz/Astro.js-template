# Template-Astro

Стартовый шаблон для проектов на **Astro** с современным CSS.

Быстрый старт для вёрстки лендингов, многостраничников и пет-проектов.

---

## 🛠️ Стек

- **[Astro](https://astro.build/)** — статический генератор сайтов
- **Vanilla CSS** — без препроцессоров и фреймворков
- **CSS Custom Properties** — переменные для дизайн-токенов
- **CSS Nesting** — вложенность как в SCSS, но нативно
- **TypeScript** — типизация в `.astro` и `.ts`
- **Vite** — сборщик (идёт с Astro)

---

## 📋 Требования

- **Node.js** ≥ 18.17.1
- **npm** ≥ 9

Проверь версии:

```bash
node -v
npm -v
```

---

## 🚀 Быстрый старт

```bash
# 1. Клонировать репозиторий
git clone https://github.com/username/my-project.git

# 2. Перейти в папку
cd template-astro

# 3. Установить зависимости
npm install

# 4. Запустить dev-сервер
npm run dev
```

Сайт откроется на **http://localhost:4321**

---

## 📜 Скрипты

| Команда | Что делает |
|---|---|
| `npm run dev` | Запуск dev-сервера с hot-reload |
| `npm run build` | Сборка сайта в `dist/` |
| `npm run preview` | Локальный просмотр собранного сайта |
| `npm run astro` | Прямой доступ к CLI Astro |

---

## 📁 Структура проекта

```
my-project/
├── public/                  # Статика (копируется как есть)
│   ├── favicon.svg
│   ├── og-image.jpg
│   ├── robots.txt
│   └── fonts/               # Локальные шрифты
│
├── src/
│   ├── assets/              # Картинки для оптимизации
│   │   ├── images/
│   │   └── icons/
│   │
│   ├── components/
│   │   ├── ui/              # UI-кирпичи (Button, Icon)
│   │   ├── layout/          # Хедер, футер и т.д.
│   │   └── SEO.astro
│   │
│   ├── data/                # Данные (навигация, контакты)
│   │   ├── site.ts
│   │   └── navigation.ts
│   │
│   ├── layouts/
│   │   └── BaseLayout.astro
│   │
│   ├── pages/               # Страницы (роутинг по файлам)
│   │   ├── index.astro
│   │   └── 404.astro
│   │
│   └── styles/
│       ├── tokens.css       # CSS-переменные (цвета, размеры)
│       ├── reset.css        # Сброс стилей
│       ├── base.css         # Типографика, база
│       ├── utilities.css    # Утилиты (.container, .visually-hidden)
│       └── global.css       # Точка входа (@import всего)
│
├── astro.config.mjs         # Конфиг Astro
├── tsconfig.json            # Конфиг TypeScript (алиасы)
├── package.json
└── README.md
```

---

## 🎨 Стили

Архитектура стилей — **простая и модульная**:

| Файл | Назначение |
|---|---|
| `tokens.css` | Дизайн-токены (цвета, отступы, размеры) |
| `reset.css` | Сброс браузерных стилей |
| `base.css` | Стили тегов (`h1`, `p`, `body`) |
| `utilities.css` | Утилиты и `.container` |
| `global.css` | Точка входа, импортирует всё выше |

**Порядок импортов в `global.css` — важен!**

```css
@import './tokens.css';      /* 1. Переменные */
@import './reset.css';       /* 2. Сброс */
@import './base.css';        /* 3. База */
@import './utilities.css';   /* 4. Утилиты */
```

### Где менять цвета и размеры

Все **дизайн-токены** — в `src/styles/tokens.css`:

```css
:root {
  --color-primary: #4f46e5;
  --container-width: 1200px;
  --space-4: 1rem;
  /* ... */
}
```

Меняешь здесь — меняется **везде** в проекте.

### Правила именования классов

- **BEM-подобный** синтаксис: `.block__element--modifier`
- Пример: `.header__logo`, `.card__title`, `.btn--primary`

---

## 🧩 Компоненты

### Структура компонента

```astro
---
// 1. Импорты
import Something from '@/components/Something.astro';

// 2. Пропсы
interface Props {
  title: string;
}

const { title } = Astro.props;
---

<!-- 3. Разметка -->
<div class="component">
  <h2>{title}</h2>
  <slot />
</div>

<style>
  /* 4. Стили (scoped по умолчанию) */
  .component {
    /* ... */
  }
</style>
```

### Что куда класть

| Что | Куда |
|---|---|
| UI-кирпич (Button, Icon) | `src/components/ui/` |
| Блок страницы (Hero, Features) | `src/components/` |
| Глобальные части (Header, Footer) | `src/components/layout` |
| Layout | `src/layouts/` |
| Страница | `src/pages/` |

---

## 🔗 Алиасы путей

Настроены алиасы для удобных импортов:

| Алиас | Куда ведёт |
|---|---|
| `@/` | `src/` |

**Примеры:**

```js
import Button from '@/components/ui/Button.astro';
import BaseLayout from '@/layouts/BaseLayout.astro';
import '@/styles/global.css';
import { site } from '@/data/site';
```

**Настройка — в двух файлах:**

- `tsconfig.json` — для VS Code
- `astro.config.mjs` — для сборщика Vite

---

## 🖼️ Работа с графикой

| Что | Куда | Как использовать |
|---|---|---|
| Favicon, og-image, robots.txt | `public/` | Прямой URL: `/favicon.svg` |
| Локальные шрифты | `public/fonts/` | `/fonts/Inter.woff2` |
| Картинки контента | `src/assets/images/` | `import img from '@/...'` |
| Иконки SVG | `src/assets/icons/` | `import icon from '@/...'` |

**Правило:** если нужен **прямой URL** → `public/`. Если **оптимизация** → `src/assets/`.

---

## 📊 Данные

Статические данные проекта — в `src/data/`:

```ts
// src/data/site.ts
export const site = {
  name: 'MyProject',
  description: '...',
  email: 'hello@example.com',
};

// src/data/navigation.ts
export const navigation = [
  { href: '/', label: 'Главная' },
  { href: '/about', label: 'О нас' },
];
```

**Использование в компонентах:**

```astro
---
import { site } from '@/data/site';
---
<a href="/" class="header__logo">{site.name}</a>
```

**Правило:** если данные повторяются **3+ раз** или их **легко менять** — выноси в `data/`.

---

## 🎯 Соглашения

### Именование файлов

- **Компоненты** — `PascalCase`: `Button.astro`, `Header.astro`
- **Утилиты и данные** — `camelCase`: `site.ts`, `navigation.ts`
- **Стили** — `kebab-case` или `camelCase`: `tokens.css`, `global.css`
- **Страницы** — `kebab-case`: `about-us.astro`, `contact.astro`

### CSS-классы

- **BEM-подобный**: `.block__element--modifier`
- **Утилиты** — короткие: `.container`, `.text-center`

### Порядок стилей в компоненте

1. Позиционирование (`position`, `top`, `z-index`)
2. Блочная модель (`display`, `width`, `padding`)
3. Типографика (`font`, `color`, `text-align`)
4. Визуал (`background`, `border`, `box-shadow`)
5. Анимации (`transition`, `transform`)

---

## 🔧 Полезные команды

```bash
# Проверка типов
npx astro check

# Установка нового пакета
npm i имя-пакета

# Установка dev-зависимости
npm i -D имя-пакета

# Очистка кэша (если что-то сломалось)
rm -rf node_modules .astro dist
npm install
```

---

## 📚 Полезные ссылки

- [Документация Astro](https://docs.astro.build/)
- [Astro в примерах](https://docs.astro.build/en/guides/examples/)
- [MDN — HTML, CSS, JS](https://developer.mozilla.org/)
- [Can I use](https://caniuse.com/) — поддержка CSS-фич
- [CSS Tricks](https://css-tricks.com/) — статьи и советы

---

## 📄 Лицензия

MIT — используй свободно.

---

## 📞 Контакты

- **Автор:** Владимир Казаков
- **Email:** glck666@gmail.com
- **GitHub:** [@username](https://github.com/username)