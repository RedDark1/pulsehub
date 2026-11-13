# PulseHub — Инструкция по сборке для Android (.APK) и Windows/macOS (.EXE)

## 1. Быстрая установка как PWA (Без сборки)
1. Разместите файлы `index.html`, `manifest.json` и `sw.js` на любом HTTPS-хостинге (GitHub Pages, Vercel, Netlify).
2. Откройте ссылку в Chrome / Edge / Safari и нажмите **«Установить приложение»** (или «На экран Домой» на iOS).

---

## 2. Сборка .APK для Android за 2 минуты (через PWABuilder)
1. Опубликуйте папку с файлами на GitHub Pages или Vercel.
2. Перейдите на сайт [https://www.pwabuilder.com](https://www.pwabuilder.com) и вставьте URL вашего сайта.
3. Нажмите **Package for Stores → Android** → **Generate Package**.
4. Скачайте архив и установите готовый `.apk` на смартфон Android.

### Альтернатива через Capacitor:
```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init PulseHub com.pulsehub.app --web-dir=.
npx cap add android
npx cap sync
npx cap open android
```

---

## 3. Сборка .EXE для Windows (или .DMG для macOS) через Electron
1. Установите Node.js (https://nodejs.org).
2. Создайте папку проекта, положите туда `index.html` и выполните:
```bash
npm init -y
npm install --save-dev electron electron-builder
```
3. Создайте файл `main.js`:
```javascript
const { app, BrowserWindow } = require('electron');
app.whenReady().then(() => {
  const win = new BrowserWindow({ width: 1200, height: 800, autoHideMenuBar: true });
  win.loadFile('index.html');
});
```
4. Укажите `"main": "main.js"` в `package.json` и соберите установщик:
```bash
npx electron-builder --win --x64
```
Готовый `.exe` появится в папке `dist/`.
