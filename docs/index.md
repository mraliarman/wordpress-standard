# فهرست مستندات استاندارد توسعه

این پوشه مرجع مهندسی تیم برای توسعه، تست، debug، SEO، انتشار، preview، پشتیبانی و استفاده کنترل‌شده از AI در محصولات وب و WordPress است. هر سند باید مستقل، قابل اجرا و دارای Definition of Done باشد.

## نقشه مطالعه پیشنهادی

### مسیر توسعه‌دهنده

1. `php-standards.md`
2. `frontend-tailwind-nodejs.md`
3. `wordpress-theme-development.md` یا `wordpress-plugin-development.md`
4. `testing-quality-assurance.md`
5. `debugging-guide.md`
6. `git-essentials.md`
7. `seo-standards-wordpress.md`

### مسیر Release/QA

1. `testing-quality-assurance.md`
2. `debugging-guide.md`
3. `product-release-checklist.md`
4. `product-preview-creation.md`
5. `seo-standards-wordpress.md`
6. `customer-support-guidelines.md`

### مسیر AI

1. `ai-assistant-workflow.md`
2. اسناد stack مرتبط با task
3. `testing-quality-assurance.md`
4. `git-essentials.md`

## فهرست رسمی اسناد

| فایل | حوزه | کاربرد |
|---|---|---|
| [frontend-tailwind-nodejs.md](frontend-tailwind-nodejs.md) | Frontend | Tailwind CSS v4، Node.js، build، scanning، RTL، dark mode و optimization |
| [php-standards.md](php-standards.md) | PHP | PSR، Composer، PSR-4، PHPDoc، type system و exceptions |
| [wordpress-theme-development.md](wordpress-theme-development.md) | WordPress Theme | classic/block theme، hierarchy، assets، theme.json، Gutenberg، FSE و child theme |
| [wordpress-plugin-development.md](wordpress-plugin-development.md) | WordPress Plugin | architecture، hooks، lifecycle، security، database، REST/AJAX و i18n |
| [testing-quality-assurance.md](testing-quality-assurance.md) | QA | test strategy، unit/integration/E2E، regression، compatibility و quality gates |
| [debugging-guide.md](debugging-guide.md) | Quality | debugging سیستماتیک PHP/WordPress/JS، logs، Query Monitor و Xdebug |
| [product-release-checklist.md](product-release-checklist.md) | Release | code freeze، testing، packaging، security، documentation و release gate |
| [seo-standards-wordpress.md](seo-standards-wordpress.md) | SEO | technical SEO، Core Web Vitals، metadata، schema، images و crawlability |
| [ai-assistant-workflow.md](ai-assistant-workflow.md) | AI | prompting، context، validation، security و human review |
| [git-essentials.md](git-essentials.md) | Git | branch، Conventional Commits، PR، conflict، tags و release workflow |
| [customer-support-guidelines.md](customer-support-guidelines.md) | Support | ticket، severity، escalation، پاسخ‌گویی و knowledge base |
| [product-preview-creation.md](product-preview-creation.md) | Product | Demo، sample content، screenshots، live preview و visual QA |

## استاندارد مشترک ساختار اسناد

هر سند اصلی باید حداقل این ترتیب را حفظ کند:

1. عنوان و خلاصه یک‌پاراگرافی.
2. اهداف و دامنه Scope.
3. استانداردها و اصول اصلی Best Practices.
4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی.
5. مراحل گام‌به‌گام / چک‌لیست عملی.
6. اشتباهات رایج و نحوه پیشگیری.
7. مثال کد/نمونه واقعی در صورت کاربرد.
8. نکات امنیتی و عملکردی در صورت کاربرد.
9. منابع معتبر.
10. Definition of Done.
11. `به‌روزرسانی بعدی` خالی در انتهای فایل.

## سیاست نگهداری

- هر استاندارد باید version-aware باشد.
- ادعاهای وابسته به نسخه باید با منبع رسمی بررسی شوند.
- قوانین بیرونی و تجاری باید هنگام release دوباره بررسی شوند.
- مواردی که قابل تأیید نیستند با **«نیاز به بررسی»** مشخص شوند.
- تغییر استاندارد باید با commit معنادار و قابل ردیابی ثبت شود.
- مستندات نباید با syntax قدیمی به‌عنوان استاندارد جدید ارائه شوند.

## به‌روزرسانی بعدی

