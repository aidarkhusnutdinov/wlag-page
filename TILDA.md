# Перенос на Тильду

## Шаги

### 1. Загрузить изображение
Редактор страницы → Media Library → загрузить `typewriter.png` → скопировать CDN-ссылку
(`https://static.tildacdn.com/...`)

### 2. Добавить Google Fonts глобально
Site Settings → More → HTML code → вкладка `<head>`:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400&subset=latin,cyrillic" rel="stylesheet">
```

### 3. Добавить Zero Block (T396)
Высота блока: ~700–800px или «по высоте экрана».

### 4. HTML (вкладка HTML в блоке)
```html
<div class="tw-outer">
  <div class="tw-wrap" id="tw-wrap">
    <img class="tw-img" id="typewriter" src="ВСТАВЬ_CDN_URL" alt="Машинка">
    <div class="paper-text" id="paper-text"></div>
    <div class="hint">нажми на машинку</div>
  </div>
</div>
```

### 5. CSS (вкладка CSS в блоке)
```css
.tw-outer {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.tw-wrap {
  position: relative;
  width: min(70vh, 88vw);
}
.tw-img {
  width: 100%;
  height: auto;
  display: block;
  cursor: pointer;
  user-select: none;
  -webkit-user-drag: none;
}
.paper-text {
  position: absolute;
  left: 32%; right: 35%;
  top: 6%; height: 36%;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding: 8% 6% 3%;
  font-family: 'Roboto Mono', 'Courier New', monospace;
  font-size: 13px;
  line-height: 1.55;
  color: #1a1a1a;
  text-align: center;
  word-break: break-word;
  pointer-events: none;
  overflow: hidden;
  -webkit-font-smoothing: antialiased;
}
@keyframes charIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}
.ch { animation: charIn 0.1s ease-out forwards; }
.sparkle {
  position: fixed;
  pointer-events: none;
  color: #e83030;
  font-weight: 700;
  z-index: 9999;
  line-height: 1;
  animation: spark 0.75s ease-out forwards;
}
@keyframes spark {
  0%   { opacity: 1; transform: scale(0.4) translate(0, 0); }
  55%  { opacity: 1; transform: scale(1.5) translate(var(--tx1), var(--ty1)); }
  100% { opacity: 0; transform: scale(0.8) translate(var(--tx2), var(--ty2)); }
}
.hint {
  position: absolute;
  bottom: -28px;
  left: 0; right: 0;
  text-align: center;
  font-family: 'Courier New', Courier, monospace;
  font-size: clamp(9px, 1.2vw, 13px);
  color: #aaa;
  letter-spacing: 0.05em;
}
```

### 6. JS (вкладка JS в блоке)
Скопировать содержимое тега `<script>` из `index.html` без изменений.

## Что проверить после вставки
- Текст попадает на бумагу (позиционирование absolute)
- Тильда не переопределяет стили блока
- Шрифт Roboto Mono загружается (открыть DevTools → Network)

Если текст поедет — скорее всего Тильда добавила свои стили на `.paper-text` или `.tw-wrap`. Решение: добавить специфичность (`#tw-wrap .paper-text { ... }`).
