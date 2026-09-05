# توسعه فرانت‌اند با Tailwind CSS و Node.js

این سند استاندارد تیم برای توسعه رابط کاربری با Tailwind CSS و Node.js است و نصب، پیکربندی، source scanning، build، ساختار پروژه، کامپوننت‌بندی، بهینه‌سازی و dark mode را پوشش می‌دهد. Tailwind CLI رسمی با نصب `tailwindcss` و `@tailwindcss/cli` و scan کردن templateها برای تولید CSS ارائه می‌شود. citeturn1search11

## 2. اهداف و دامنه (Scope)

پوشش: HTML، PHP template، JavaScript، Tailwind CLI، CSS production، responsive، RTL و dark mode. خارج از دامنه: React/Vue/Nuxt و الزام به Vite.

## 3. استانداردها و اصول اصلی (Best Practices)

- نسخه Node و Tailwind را مشخص و lock کنید.
- sourceهای PHP/HTML/JS باید کامل scan شوند.
- classهای dynamic مانند `text-${size}-500` نسازید؛ mapping کامل classها داشته باشید.
- mobile-first و breakpointهای محدود استفاده کنید.
- `@apply` فقط برای abstractionهای واقعی؛ utility-first پیش‌فرض است.
- RTL را با `dir="rtl"` و utilityهای منطقی مناسب نسخه پیاده کنید.
- tokenهای رنگ، typography و spacing متمرکز باشند.
- dark mode باید surface، text، border، hover و focus را پوشش دهد.

ساختار پیشنهادی:

```text
project/
├── package.json
├── tailwind.config.js
├── src/css/input.css
├── templates/
├── assets/js/
└── static/css/app.css
```

برای Tailwind 3:

```js
module.exports = {
    content: ['./templates/**/*.html', './**/*.php', './assets/**/*.js'],
    theme: { extend: {} },
    darkMode: 'class',
    plugins: []
};
```

در Tailwind 4، مدل configuration تغییر کرده و CSS-first است؛ config v3 را بدون بررسی migration با v4 مخلوط نکنید.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- Node.js: LTS مورد تأیید پروژه.
- Tailwind CSS: stable سازگار با پروژه، با lockfile.
- `@tailwindcss/cli`: انتخاب رسمی برای پروژه‌های بدون bundler. citeturn1search11
- npm و در صورت نیاز Prettier.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. Node را نصب و `node -v` و `npm -v` را بررسی کنید.
2. `npm init -y` اجرا کنید.
3. `npm install tailwindcss @tailwindcss/cli` اجرا کنید.
4. input CSS بسازید:

```css
@import "tailwindcss";
```

5. sourceهای پروژه را پوشش دهید.
6. توسعه:

```bash
npx @tailwindcss/cli -i ./src/css/input.css -o ./static/css/app.css --watch
```

7. production:

```bash
npx @tailwindcss/cli -i ./src/css/input.css -o ./static/css/app.css --minify
```

8. خروجی را با cache busting سرو کنید.
9. responsive، RTL، dark mode و keyboard states را تست کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- مسیر ناقص source و حذف شدن utilityها.
- dynamic class غیرقابل تشخیص scanner.
- مخلوط کردن v3/v4.
- انتشار CSS توسعه‌ای.
- استفاده افراطی از `!important`.
- dark mode ناقص.

## 7. مثال‌های کد یا نمونه واقعی

```html
<button class="inline-flex items-center rounded-lg bg-blue-600 px-4 py-2 text-sm font-semibold text-white hover:bg-blue-700 focus-visible:outline-2 disabled:opacity-50 dark:bg-blue-500">
    ذخیره
</button>
```

## 8. نکات امنیتی و عملکردی

CSS را minify کنید، artifactهای debug را منتشر نکنید، dependencyها را audit کنید و build را از lockfile انجام دهید. فونت و icon unused حذف شود.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- https://tailwindcss.com/docs/installation/tailwind-cli
- https://tailwindcss.com/docs
- https://docs.npmjs.com/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] نسخه‌ها مشخص و lock شده‌اند.
- [ ] sourceها کامل scan می‌شوند.
- [ ] build توسعه و production موفق است.
- [ ] CSS minify شده است.
- [ ] responsive، RTL و dark mode تست شده‌اند.
- [ ] focus و disabled بررسی شده‌اند.
- [ ] CI از صفر build می‌کند.

## به‌روزرسانی بعدی

