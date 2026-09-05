# استاندارد فرانت‌اند با Tailwind CSS v4 و Node.js

این سند استاندارد رسمی تیم برای توسعه رابط کاربری با Tailwind CSS و Node.js است و معماری CSS، نصب و build، source scanning، Tailwind CSS v4، ساختار پروژه، design token، component patterns، responsive، RTL، dark mode، production optimization و کنترل کیفیت را پوشش می‌دهد. مبنای جدید پروژه‌های تازه Tailwind CSS v4 است؛ در v4 رویکرد CSS-first و `@import "tailwindcss"` محور است و CLI رسمی با بسته `@tailwindcss/cli` ارائه می‌شود. Tailwind هنگام build sourceها را برای classها scan کرده و CSS موردنیاز را تولید می‌کند. citeturn0search2

## 2. اهداف و دامنه (Scope)

این استاندارد برای پروژه‌های HTML، PHP/WordPress، JavaScript و قالب‌های server-rendered طراحی شده و Node.js را ابزار build می‌داند، نه الزاماً runtime برنامه. استفاده از React، Vue، Nuxt و Vite جزو الزامات این repository نیست. پروژه باید بین Tailwind v4 و legacy v3 انتخاب صریح داشته باشد و configuration این دو نسل بدون migration رسمی با یکدیگر مخلوط نشود.

## 3. استانداردها و اصول اصلی (Best Practices)

### 3.1 استاندارد Tailwind CSS v4

- برای پروژه جدید، Tailwind CSS v4 استاندارد پیش‌فرض است.
- نصب پایه CLI:

```bash
npm install tailwindcss @tailwindcss/cli
```

- فایل ورودی CSS حداقل باید شامل این باشد:

```css
@import "tailwindcss";
```

- build توسعه:

```bash
npx @tailwindcss/cli -i ./src/css/input.css -o ./static/css/app.css --watch
```

- build production:

```bash
npx @tailwindcss/cli -i ./src/css/input.css -o ./static/css/app.css --minify
```

این workflow با CLI رسمی Tailwind v4 هم‌راستا است. citeturn0search2

### 3.2 تفاوت v4 و v3

| موضوع | Tailwind v4 | Tailwind v3 |
|---|---|---|
| رویکرد اصلی | CSS-first | JavaScript config محور |
| import اصلی | `@import "tailwindcss"` | `@tailwind base/components/utilities` |
| config | در بسیاری از پروژه‌ها بدون config جدا | `tailwind.config.js` رایج و مرکزی |
| CLI | `@tailwindcss/cli` | CLI نسل قبلی |
| migration | نیازمند بررسی پروژه | legacy |

`tailwind.config.js` همچنان در پروژه‌های legacy v3 معتبر است، اما نباید صرفاً به‌دلیل وجود این فایل، پروژه v4 را با الگوی v3 مستند یا build کرد. برای جزئیات migration هر پروژه «نیاز به بررسی» نسخه دقیق و migration guide رسمی است.

### 3.3 Source scanning و class detection

- تمام مسیرهای واقعی template، PHP، HTML و JavaScript باید در فرآیند build قابل شناسایی باشند.
- class nameها باید به شکل کامل و قابل تحلیل در source وجود داشته باشند.
- الگوهایی مانند `text-${size}-500` قابل اتکا نیستند؛ به‌جای آن mapping صریح classها ایجاد کنید.
- اگر classها از CMS، database یا API می‌آیند، باید strategy مشخص safelist یا mapping داشته باشید.
- source map یا فایل‌های توسعه‌ای حساس نباید در artifact عمومی قرار گیرند مگر عمداً موردنیاز باشند.

### 3.4 معماری CSS

- utility-first رویکرد پیش‌فرض است.
- `@apply` فقط برای abstractionهای پایدار و قابل توضیح استفاده شود.
- component classهای بزرگ که عملاً utilityها را پنهان می‌کنند ایجاد نشوند.
- design tokenهای رنگ، spacing، typography و radius یک منبع حقیقت داشته باشند.
- نام‌گذاری semantic باشد؛ رنگی مانند `blue-600` نباید در تمام UI به‌عنوان هویت محصول hard-code شود اگر token معنایی وجود دارد.

### 3.5 Responsive، RTL و accessibility

- mobile-first طراحی کنید.
- breakpoint جدید فقط در صورت نیاز واقعی اضافه شود.
- در RTL از logical properties و الگوی سازگار با نسخه Tailwind استفاده کنید.
- ترتیب tab، focus-visible، keyboard interaction و contrast بررسی شود.
- برای icon-only control، accessible name ارائه شود.

### 3.6 Dark mode

dark mode باید برای background، surface، text، border، placeholder، icon، hover، active، focus و disabled طراحی شود؛ صرفاً تغییر background کافی نیست. strategy استفاده از class یا media باید در معماری پروژه ثابت و مستند باشد.

### 3.7 ساختار پیشنهادی

```text
project/
├── package.json
├── package-lock.json
├── src/
│   └── css/
│       └── input.css
├── templates/
├── assets/
│   └── js/
├── static/
│   └── css/
│       └── app.css
└── docs/
```

در پروژه‌های Tailwind v3 که هنوز migration نشده‌اند، `tailwind.config.js` باید در root و همراه با version مشخص نگهداری شود.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

| ابزار | سیاست |
|---|---|
| Node.js | نسخه LTS مورد تأیید پروژه |
| Tailwind CSS | v4 برای پروژه جدید؛ v3 فقط برای legacy تا migration |
| `@tailwindcss/cli` | برای build بدون bundler |
| npm | همراه lockfile و `npm ci` در CI |
| Prettier | در صورت تعریف formatter تیم |
| Browser DevTools | بررسی layout، CSS و network |
| Lighthouse | کنترل performance و accessibility |

نسخه دقیق dependencyها باید در `package-lock.json` تثبیت شود؛ عبارت «latest» نباید مبنای build production باشد.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. نسخه Node و Tailwind را تعیین کنید.
2. برای پروژه جدید v4 را انتخاب کنید.
3. `package.json` و lockfile ایجاد کنید.
4. input CSS را بسازید.
5. sourceهای template را مشخص کنید.
6. build توسعه را اجرا کنید.
7. componentهای اصلی، responsive، RTL و dark mode را پیاده کنید.
8. classهای dynamic را با mapping یا strategy صریح حل کنید.
9. CSS تولیدشده را بررسی کنید و utilityهای غیرمنتظره را پیدا کنید.
10. build production با `--minify` اجرا کنید.
11. خروجی را در WordPress/PHP با enqueue صحیح سرو کنید.
12. browser، keyboard و mobile را تست کنید.
13. artifact production را از محیط توسعه جدا کنید.
14. CI را طوری تنظیم کنید که از lockfile build کند.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- استفاده از syntax v3 در پروژه v4 بدون migration.
- نگه‌داشتن `tailwind.config.js` به‌عنوان الزام v4 در حالی که پروژه config-free است.
- source scan ناقص و حذف utilityهای لازم.
- ساخت dynamic class با interpolation.
- استفاده افراطی از `@apply`.
- CSS production غیرminified.
- نبود focus state.
- dark mode ناقص.
- استفاده از رنگ و spacing بدون token در پروژه بزرگ.
- وابستگی به Node version متفاوت بین local و CI.

## 7. مثال‌های کد یا نمونه واقعی

ورودی v4:

```css
@import "tailwindcss";
```

کامپوننت قابل استفاده در template:

```html
<button type="button" class="inline-flex items-center justify-center rounded-lg px-4 py-2 text-sm font-semibold transition hover:opacity-90 focus-visible:outline-2 disabled:cursor-not-allowed disabled:opacity-50 dark:opacity-95">
    ذخیره
</button>
```

برای variantهای داده‌محور، mapping صریح بهتر از ساخت class در runtime است:

```js
const badgeClasses = {
    success: 'bg-green-100 text-green-800',
    warning: 'bg-yellow-100 text-yellow-800',
    danger: 'bg-red-100 text-red-800'
};
```

## 8. نکات امنیتی و عملکردی

Tailwind به‌خودی‌خود جایگزین امنیت HTML/PHP نیست؛ داده dynamic باید در context مناسب escape شود. dependencyها audit شوند، lockfile حفظ شود و build production از source کنترل‌شده انجام گیرد. CSS، font و image باید به‌اندازه نیاز تولید شوند. third-party CSS/JS غیرضروری حذف شود. در WordPress، assetها فقط در صفحات لازم enqueue شوند.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Tailwind CLI: https://tailwindcss.com/docs/installation/tailwind-cli
- Tailwind CSS documentation: https://tailwindcss.com/docs
- npm documentation: https://docs.npmjs.com/
- Node.js: https://nodejs.org/docs/latest/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] نسخه Tailwind مشخص است و پروژه جدید بر v4 است.
- [ ] Node و dependencyها با lockfile تثبیت شده‌اند.
- [ ] build توسعه و production موفق است.
- [ ] source scan کامل است.
- [ ] dynamic classها strategy مشخص دارند.
- [ ] CSS production minify شده است.
- [ ] responsive، RTL، dark mode و accessibility تست شده‌اند.
- [ ] focus/hover/disabled stateها بررسی شده‌اند.
- [ ] artifact نهایی بدون فایل توسعه‌ای غیرضروری است.
- [ ] CI از صفر و با lockfile build می‌کند.

## به‌روزرسانی بعدی

