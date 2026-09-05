# چک‌لیست انتشار محصول در استور ژاکت

این سند فرآیند آماده‌سازی محصول WordPress برای انتشار در استور ژاکت را تعریف می‌کند؛ از freeze کد و تست تا مستندات، تصاویر، نسخه و بسته نهایی. قوانین دقیق استور ممکن است تغییر کند؛ موارد قراردادی/قوانین فعلی با برچسب «نیاز به بررسی» باید در زمان ارسال از مرجع رسمی ژاکت کنترل شوند.

## 2. اهداف و دامنه (Scope)

پوشش: theme/plugin release، کیفیت کد، امنیت، بسته‌بندی، مستندات، screenshots، versioning و تست. جزئیات جاری قوانین ژاکت در صورت تغییر، خارج از این سند ثابت است.

## 3. استانداردها و اصول اصلی (Best Practices)

- release candidate را freeze کنید.
- debug code، dump، test account، secret، API key و فایل local حذف شوند.
- version در header/package/changelog هماهنگ باشد.
- dependencyهای Composer/npm و license آن‌ها بررسی شوند.
- محصول روی WordPress تازه و سایت دارای محتوای واقعی تست شود.
- activation، update، deactivation و uninstall بررسی شود.
- PHP notices/warnings/fatal و JS console error صفر باشد.
- فارسی، RTL، mobile و browserهای اصلی تست شوند.
- readme نصب، تنظیمات، FAQ، requirements و update procedure داشته باشد.
- screenshots واقعی و بدون داده خصوصی باشند.
- «نیاز به بررسی»: قوانین و محدودیت‌های فعلی ژاکت، فرمت و ابعاد دقیق تصاویر و شرایط تجاری باید قبل از submit از پنل/راهنمای رسمی تأیید شوند.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- WordPress stable پشتیبانی‌شده.
- PHP و MySQL/MariaDB مطابق requirements محصول.
- WP-CLI.
- PHPCS/WPCS، PHPStan، PHPUnit.
- Node.js LTS و build tool پروژه.
- Lighthouse/PageSpeed برای frontend.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. branch release را freeze کنید.
2. version و changelog را نهایی کنید.
3. dependency audit و license review انجام دهید.
4. lint/static analysis/tests اجرا کنید.
5. clean install تست کنید.
6. update از نسخه قبلی تست کنید.
7. activation/deactivation/uninstall را تست کنید.
8. RTL/mobile/browser/accessibility را تست کنید.
9. امنیت nonce/capability/escape/sanitize را بازبینی کنید.
10. build production را بسازید.
11. ZIP نهایی را از صفر extract و نصب کنید.
12. فایل‌های غیرضروری را حذف کنید.
13. مستندات و screenshots را کنترل کنید.
14. قوانین فعلی ژاکت را دوباره بررسی کنید.
15. checksum و نسخه artifact را ثبت کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- انتشار `.env`، backup یا source map حساس.
- mismatch نسخه محصول و changelog.
- تست فقط روی سایت توسعه‌دهنده.
- نبود update migration.
- تصاویر دارای اطلاعات مشتری.
- مستندات ناقص یا لینک‌های شکسته.

## 7. مثال‌های کد یا نمونه واقعی

ساخت artifact تمیز:

```bash
composer install --no-dev --optimize-autoloader
npm ci
npm run build
```

سپس فقط فایل‌های runtime و مستندات لازم را داخل ZIP قرار دهید.

## 8. نکات امنیتی و عملکردی

secretها هرگز داخل ZIP یا Git نباشند. assetها minify شوند. query و remote request غیرضروری حذف شوند. دسترسی فایل‌ها و endpointهای admin بازبینی شود.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- WordPress Plugin Handbook: https://developer.wordpress.org/plugins/
- WordPress Theme Handbook: https://developer.wordpress.org/themes/
- نیاز به بررسی: قوانین جاری استور ژاکت در زمان انتشار.

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] clean install موفق است.
- [ ] update از نسخه قبلی موفق است.
- [ ] هیچ secret/debug artifact وجود ندارد.
- [ ] lint/test/static analysis موفق است.
- [ ] RTL/mobile/browser تست شده است.
- [ ] مستندات و screenshots نهایی‌اند.
- [ ] قوانین جاری استور بررسی شده‌اند.
- [ ] ZIP نهایی از صفر قابل نصب است.

## به‌روزرسانی بعدی

