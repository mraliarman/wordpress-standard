# استاندارد مهندسی توسعه WordPress و وب

مرجع مهندسی و عملیاتی تیم برای طراحی، توسعه، بازبینی، تست، انتشار، پشتیبانی و نگهداری محصولات وب، PHP و WordPress. این repository با هدف تبدیل تجربه‌های پراکنده تیم به استانداردهای نسخه‌پذیر، قابل بازبینی و قابل استفاده توسط توسعه‌دهندگان، مدیران پروژه، QA و دستیارهای هوش مصنوعی ساخته شده است.

> **اصل کلیدی:** هیچ استانداردی نباید صرفاً به‌صورت سلیقه‌ای اجرا شود؛ هر قاعده باید تا حد امکان قابل مشاهده، قابل تست، قابل review و قابل تبدیل به checklist باشد.

## فهرست مطالب

- [هدف repository](#هدف-repository)
- [چرا این repository ایجاد شده است؟](#چرا-این-repository-ایجاد-شده-است)
- [دامنه](#دامنه)
- [معماری مستندات](#معماری-مستندات)
- [راهنمای سریع](#راهنمای-سریع)
- [استانداردهای اصلی](#استانداردهای-اصلی)
- [استاندارد فرانت‌اند و Tailwind CSS v4](#استاندارد-فرانت‌اند-و-tailwind-css-v4)
- [استاندارد PHP](#استاندارد-php)
- [استاندارد WordPress](#استاندارد-wordpress)
- [کیفیت و Debugging](#کیفیت-و-debugging)
- [SEO و Performance](#seo-و-performance)
- [Git و Release](#git-و-release)
- [محصول و پشتیبانی](#محصول-و-پشتیبانی)
- [استفاده از AI](#استفاده-از-ai)
- [فرآیند توسعه پیشنهادی](#فرآیند-توسعه-پیشنهادی)
- [Definition of Done](#definition-of-done)
- [قواعد contribution](#قواعد-contribution)
- [امنیت](#امنیت)
- [نسخه‌بندی و نگهداری](#نسخهبندی-و-نگهداری)
- [مجوز](#مجوز)

## هدف repository

این پروژه یک codebase محصول نیست؛ یک **Engineering Standards Repository** است. محتوای آن باید به تیم کمک کند تصمیم‌های فنی و عملیاتی را به شکل یکنواخت بگیرد و از خطاهای تکرارشونده جلوگیری کند.

اهداف اصلی:

1. تعریف baseline مشترک برای توسعه PHP و WordPress.
2. استانداردسازی frontend و build با Tailwind CSS.
3. کاهش خطاهای امنیتی، performance و compatibility.
4. ایجاد فرآیند مشخص برای debugging و release.
5. ایجاد checklist قابل استفاده در code review و QA.
6. استانداردسازی ارتباط تیم توسعه، محصول و پشتیبانی.
7. ایجاد چارچوبی برای استفاده کنترل‌شده از AI.
8. نگهداری دانش تیم در قالب version-controlled documentation.

## چرا این repository ایجاد شده است؟

در پروژه‌های WordPress معمولاً کیفیت فقط به توانایی برنامه‌نویس وابسته نیست؛ ساختار پروژه، coding standards، dependency management، build frontend، امنیت، SEO، release process و پشتیبانی همگی روی نتیجه نهایی اثر دارند. این repository این لایه‌ها را در یک مرجع مشترک جمع می‌کند تا «نحوه انجام کار» مستقل از فرد باشد.

## دامنه

این repository حوزه‌های زیر را پوشش می‌دهد:

| حوزه | پوشش |
|---|---|
| Frontend | Tailwind CSS v4، Node.js، CSS architecture، RTL، dark mode و build |
| PHP | PSR، Composer، PSR-4، PHPDoc، type system و exception handling |
| WordPress Theme | classic theme، block theme، hierarchy، assets، theme.json و child theme |
| WordPress Plugin | hooks، lifecycle، security، database، i18n و compatibility |
| Debugging | PHP، WordPress، JavaScript، database، network و Xdebug |
| SEO | technical SEO، Core Web Vitals، markup، images و structured data |
| Git | branch، commit، PR، conflict، tags و release workflow |
| Product | release، preview/demo، packaging و quality gate |
| Support | ticket، severity، escalation، FAQ و knowledge base |
| AI | prompt، validation، security review و human approval |

## معماری مستندات

تمام استانداردهای اصلی در `docs/` قرار دارند و از یک ساختار مشترک پیروی می‌کنند:

```text
wordpress-standard/
├── docs/
│   ├── index.md
│   ├── frontend-tailwind-nodejs.md
│   ├── php-standards.md
│   ├── wordpress-theme-development.md
│   ├── wordpress-plugin-development.md
│   ├── debugging-guide.md
│   ├── product-release-checklist.md
│   ├── seo-standards-wordpress.md
│   ├── ai-assistant-workflow.md
│   ├── git-essentials.md
│   ├── customer-support-guidelines.md
│   └── product-preview-creation.md
├── README.md
├── SECURITY.md
└── LICENSE
```

فهرست رسمی مستندات در [`docs/index.md`](docs/index.md) نگهداری می‌شود.

## راهنمای سریع

### اگر توسعه‌دهنده هستید

ابتدا این ترتیب را بخوانید:

1. `docs/php-standards.md`
2. `docs/frontend-tailwind-nodejs.md`
3. `docs/wordpress-theme-development.md` یا `docs/wordpress-plugin-development.md`
4. `docs/debugging-guide.md`
5. `docs/git-essentials.md`
6. `docs/seo-standards-wordpress.md`

### اگر QA یا Release Manager هستید

1. `docs/debugging-guide.md`
2. `docs/product-release-checklist.md`
3. `docs/product-preview-creation.md`
4. `docs/seo-standards-wordpress.md`
5. `docs/customer-support-guidelines.md`

### اگر با AI کار می‌کنید

`docs/ai-assistant-workflow.md` باید قبل از استفاده جدی از AI در taskهای repository مطالعه شود. AI مجاز به bypass کردن review، test یا security gate نیست.

## استانداردهای اصلی

### 1. Code Quality

- کد باید خوانا، قابل نگهداری و قابل تست باشد.
- public APIها باید type مشخص داشته باشند.
- dependency غیرضروری اضافه نشود.
- duplication فقط در صورت وجود دلیل معماری قابل قبول باشد.
- abstraction باید مسئله واقعی را حل کند؛ abstraction زودهنگام ممنوع.
- تغییرات بزرگ به taskهای کوچک و قابل review تقسیم شوند.

### 2. Security by Default

- secret، token، credential و داده خصوصی در repository قرار نگیرد.
- authorization از authentication و nonce از authorization تفکیک شود.
- input validation/sanitization و output escaping بر اساس context انجام شود.
- SQL دارای ورودی با API امن و parameterized اجرا شود.
- dependencyها قبل از استفاده بررسی شوند.
- debug output در production نمایش داده نشود.

### 3. Performance by Default

- هر dependency و asset باید دلیل داشته باشد.
- query و remote request غیرضروری حذف شود.
- CSS/JS production بهینه و cacheable باشد.
- تصاویر با ابعاد، فرمت و loading strategy مناسب ارائه شوند.
- performance با metric سنجیده شود، نه با حدس.

### 4. Documentation as Code

مستندات بخشی از محصول هستند. هر تغییر معماری یا workflow که روی توسعه‌دهنده بعدی اثر می‌گذارد باید همراه با documentation update شود.

## استاندارد فرانت‌اند و Tailwind CSS v4

**Tailwind CSS v4 استاندارد پیش‌فرض پروژه‌های جدید است.** در v4 معماری CSS-first است و استفاده از `@import "tailwindcss"` الگوی اصلی شروع کار است. برای پروژه‌هایی که bundler ندارند، `@tailwindcss/cli` ابزار رسمی CLI است. جزئیات کامل در `docs/frontend-tailwind-nodejs.md` آمده است.

نمونه build:

```bash
npm install tailwindcss @tailwindcss/cli
npx @tailwindcss/cli -i ./src/css/input.css -o ./static/css/app.css --watch
npx @tailwindcss/cli -i ./src/css/input.css -o ./static/css/app.css --minify
```

پروژه‌های legacy که Tailwind v3 دارند باید version خود را صریح اعلام کنند و migration به v4 را به‌صورت کنترل‌شده انجام دهند. وجود `tailwind.config.js` به‌تنهایی به معنی استاندارد بودن پروژه برای v4 نیست.

## استاندارد PHP

PHP باید بر پایه PSR-1/PSR-12، PSR-4، Composer و type-safe API طراحی شود. namespace، autoload، PHPDoc، exception handling، dependency constraints و static analysis در `docs/php-standards.md` تعریف شده‌اند.

حداقل quality gate پیشنهادی:

```bash
composer validate
php -l path/to/file.php
composer test
```

دستور دقیق test باید مطابق `composer.json` هر پروژه تعیین شود؛ command ساختگی نباید به عنوان استاندارد قطعی تلقی شود.

## استاندارد WordPress

### Theme

قالب باید presentation را مدیریت کند و functionality مستقل از presentation تا حد امکان در plugin قرار گیرد. template hierarchy، enqueue، `theme.json`، child theme، Gutenberg و block/classic architecture در `docs/wordpress-theme-development.md` مستند شده‌اند.

### Plugin

افزونه باید bootstrap کوچک، architecture قابل توسعه، hooks شفاف، lifecycle مشخص، security checks، migration قابل تکرار و i18n صحیح داشته باشد. جزئیات در `docs/wordpress-plugin-development.md` آمده است.

## کیفیت و Debugging

اصل debugging این repository:

> **Reproduce → Collect Evidence → Isolate → Fix → Test → Regression Check → Deploy → Monitor**

قبل از تغییر کد باید تا حد امکان actual behavior، expected behavior، محیط، نسخه‌ها، log و reproduction steps ثبت شود. `WP_DEBUG`، Query Monitor، Browser DevTools و Xdebug ابزارهای تشخیصی هستند، نه جایگزین تحلیل root cause.

## SEO و Performance

SEO در سطح کد باید شامل crawlability، metadata ownership، heading semantics، canonical، URL، image handling، mobile، structured data و Core Web Vitals باشد. theme نباید بدون هماهنگی با SEO plugin، title/canonical/schema را duplicate کند.

برای performance، معیارهای واقعی مانند LCP، INP و CLS اندازه‌گیری شوند و تصمیم‌ها بر اساس داده باشند.

## Git و Release

### Branching

الگوی پایه:

```text
main
feature/<name>
fix/<name>
hotfix/<name>
docs/<name>
refactor/<name>
```

### Commit

Conventional Commits الگوی پیشنهادی است:

```text
feat(admin): add customer search
fix(booking): prevent duplicate appointment
docs: update installation guide
refactor(core): simplify asset loader
chore: update dependencies
```

### Pull Request

هر PR باید حداقل شامل موارد زیر باشد:

- مسئله و هدف.
- محدوده تغییر.
- فایل‌ها یا componentهای اصلی.
- روش تست.
- risk و migration impact در صورت وجود.
- screenshot برای تغییرات UI در صورت کاربرد.

## محصول و پشتیبانی

Release صرفاً ساخت ZIP نیست. release باید شامل code freeze، dependency review، test، clean install، update test، security review، documentation، preview/demo و کنترل artifact باشد.

پشتیبانی نیز بخشی از چرخه محصول است. هر bug تکرارشونده باید در نهایت به یکی از این خروجی‌ها تبدیل شود:

1. fix محصول؛
2. documentation؛
3. FAQ؛
4. automation؛
5. تغییر فرآیند.

## استفاده از AI

AI یک **دستیار** است و صاحب تصمیم فنی نیست. خروجی AI باید مانند code شخص ثالث بررسی شود. prompt باید context، constraint، expected result و acceptance criteria داشته باشد.

ممنوع:

- ارسال secret یا credential غیرضروری.
- merge مستقیم خروجی بدون review.
- پذیرش API یا function ناشناخته بدون بررسی documentation.
- refactor بزرگ بدون regression test.
- ساخت dependency صرفاً برای حل یک مشکل کوچک بدون بررسی trade-off.

مرجع اعلام‌شده تیم برای workflow AI در `docs/ai-assistant-workflow.md` قرار دارد. محتوای جاری سایت `https://llm.bestjustify.ir/` در زمان آخرین بررسی از محیط ابزار در دسترس نبود و بنابراین ادعای خلاصه‌سازی محتوای اختصاصی آن در این repository نشده است؛ این مورد **نیاز به بررسی** است.

## فرآیند توسعه پیشنهادی

چرخه استاندارد task:

```text
Requirement
    ↓
Clarify Scope
    ↓
Technical Plan
    ↓
Implementation
    ↓
Lint / Static Analysis
    ↓
Automated Tests
    ↓
Manual QA
    ↓
Security / Performance Review
    ↓
Code Review
    ↓
Staging
    ↓
Release
    ↓
Monitor
    ↓
Documentation / Retrospective
```

### Gateهای مدیریتی

| Gate | پرسش اصلی | خروجی |
|---|---|---|
| Scope | دقیقاً چه چیزی باید تغییر کند؟ | acceptance criteria |
| Technical | چگونه و در کدام لایه؟ | technical plan |
| Development | آیا implementation کامل است؟ | code |
| Quality | آیا تست و static analysis موفق است؟ | evidence |
| Security | آیا attack surface بررسی شده؟ | security check |
| UX/SEO | آیا تجربه و discoverability حفظ شده؟ | QA result |
| Release | آیا artifact قابل انتشار است؟ | release package |
| Post-release | آیا رفتار production صحیح است؟ | monitoring |

## Definition of Done

یک task زمانی Done است که همه موارد مرتبط زیر تکمیل شده باشند:

- [ ] scope و acceptance criteria روشن است.
- [ ] implementation با architecture پروژه سازگار است.
- [ ] coding standards رعایت شده است.
- [ ] lint و static analysis موفق است.
- [ ] automated/manual tests لازم اجرا شده‌اند.
- [ ] regression risk بررسی شده است.
- [ ] security impact بررسی شده است.
- [ ] performance impact در صورت کاربرد بررسی شده است.
- [ ] documentation لازم به‌روز شده است.
- [ ] review انسانی انجام شده است.
- [ ] release/staging impact مشخص است.
- [ ] در صورت انتشار، rollback یا recovery strategy مشخص است.

## قواعد contribution

1. قبل از ایجاد استاندارد جدید، `docs/index.md` و فایل‌های موجود را بررسی کنید.
2. از ایجاد دو سند با موضوع هم‌پوشان خودداری کنید.
3. تغییر استاندارد باید دلیل مشخص داشته باشد.
4. ادعاهای وابسته به نسخه یا قوانین بیرونی باید با منبع معتبر بررسی شوند.
5. موارد تأییدنشده با عبارت **«نیاز به بررسی»** مشخص شوند.
6. لینک‌ها باید معتبر و قابل دسترسی باشند.
7. مثال‌های کد باید با نسخه اعلام‌شده سند سازگار باشند.
8. Definition of Done هر سند باید قابل اجرا و قابل review باشد.
9. commitها atomic و قابل فهم باشند.
10. تغییرات مهم باید در همان commit یا PR مستندات مرتبط را نیز به‌روزرسانی کنند.

## امنیت

سیاست امنیتی در [`SECURITY.md`](SECURITY.md) قرار دارد. در صورت مشاهده secret افشاشده، صرفاً حذف آن از آخرین commit کافی نیست؛ secret باید revoke/rotate شود و در صورت نیاز history نیز پاک‌سازی شود.

## نسخه‌بندی و نگهداری

این repository باید به‌صورت مستمر با تغییرات WordPress، PHP، Tailwind، Node.js، مرورگرها، ابزارهای build و سیاست‌های انتشار هماهنگ شود. برای هر سند، بخش `به‌روزرسانی بعدی` در انتهای فایل به‌عنوان محل ثبت برنامه یا موضوع بررسی بعدی نگهداری می‌شود.

مواردی که به قوانین خارجی وابسته‌اند، مانند سیاست‌های جاری استور ژاکت، باید در زمان release از مرجع رسمی دوباره بررسی شوند.

## منابع اصلی

- WordPress Developer Resources: https://developer.wordpress.org/
- WordPress Theme Handbook: https://developer.wordpress.org/themes/
- WordPress Plugin Handbook: https://developer.wordpress.org/plugins/
- WordPress Coding Standards: https://developer.wordpress.org/coding-standards/
- Tailwind CSS: https://tailwindcss.com/docs
- Node.js: https://nodejs.org/docs/latest/
- PHP Manual: https://www.php.net/docs.php
- PHP-FIG: https://www.php-fig.org/
- Composer: https://getcomposer.org/doc/
- Git: https://git-scm.com/doc
- Conventional Commits: https://www.conventionalcommits.org/en/v1.0.0/
- Google Search Essentials: https://developers.google.com/search/docs/essentials

## مجوز

وضعیت مجوز repository در [`LICENSE`](LICENSE) قرار دارد. هر تغییر مالکیت یا license باید با مالک repository تأیید شود.
