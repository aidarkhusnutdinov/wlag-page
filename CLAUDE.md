# wlag-page

Страница для сайта writelikeagirl.ru (клиент — Тильда).

## Что это

Кликабельная иллюстрация пишущей машинки: нажимаешь — на бумаге появляется случайная идея для письма с эффектом печати и красными искрами.

## Файлы

- `index.html` — весь код страницы (один файл, без зависимостей кроме Google Fonts)
- `typewriter.png` — 4558×3869px RGBA, основная иллюстрация (прозрачный фон)
- `Машинка 4.png` — 4558×1727px RGBA, крупный план бумаги. **Другой угол съёмки**, не кроп typewriter.png — не использовать как позиционный сайзер
- `animation stars.gif` — референс анимации искр
- `animation type.gif` — референс анимации печатания

## Область бумаги (измерено через getBoundingClientRect на десктопе 1280×720)

Машинка рендерится 504×428px.
Бумага: X от ~28.6% до ~73.4% ширины машинки, Y от ~6% до ~42% высоты.
В CSS: `left: 32%, right: 35%, top: 6%, height: 36%` + `padding: 8% 6% 3%`.

## Идеи для письма

Загружаются с:
```
https://raw.githubusercontent.com/writelikeagirl/ideasforwriting/refs/heads/main/ideas.txt
```
Кэшируются после первого запроса. Последние 8 показанных исключаются из следующей выборки.

## Шрифт

Roboto Mono (Google Fonts, cyrillic subset) — Courier New давал разную ширину кириллицы на iOS vs Chrome, текст вылезал за правый край бумаги.

## Динамический размер шрифта

```js
function calcFontSize(len) {
  const mobile = window.innerWidth < 640;
  if (mobile) {
    if (len <= 30) return '11px';
    if (len <= 55) return '9px';
    return '7px';
  }
  if (len <= 35) return '13px';
  if (len <= 60) return '11px';
  if (len <= 90) return '9px';
  return '8px';
}
```

## Скорость печати

`Math.max(90, Math.min(140, 3500 / text.length))` мс/символ — ощущается как реальная машинка.

## Следующий шаг

Перенести на Тильду: загрузить `typewriter.png` в медиабиблиотеку, поставить Zero Block (T396), добавить картинку и HTML-блок с кодом из `index.html`.

## Известные проблемы решённые

- Текст выходил за бумагу вертикально → `align-items: flex-start` + динамический шрифт
- Текст выходил за бумагу горизонтально на мобилке → переход с Courier New на Roboto Mono + `right: 35%`
- `Машинка 4.png` как позиционный сайзер — не работает (другой угол)
