# استاندارد انتشار نهایی محصول در استور ژاکت

این سند quality gate انتشار محصول WordPress در استور ژاکت را تعریف می‌کند؛ از feature freeze و code review تا تست clean install، update، امنیت، مستندات، تصاویر، demo، versioning، packaging و کنترل artifact. قوانین بیرونی استور ممکن است تغییر کنند و هر requirement تجاری یا ابعادی که در این سند با «نیاز به بررسی» مشخص شده باید هنگام release از مرجع رسمی بررسی شود.

## 2. اهداف و دامنه (Scope)

دامنه شامل plugin/theme release، source cleanup، dependency/license review، testing، documentation، screenshots، preview، ZIP packaging، versioning و release evidence است.

## 3. استانداردها و اصول اصلی (Best Practices)

### Release Gate

هیچ release صرفاً با «کار می‌کند» تأیید نمی‌شود. release باید قابل نصب، قابل update، قابل پشتیبانی و قابل توضیح باشد.

### Code Quality

- debug، dump، test route و temporary code حذف شود.
- naming و coding standards بررسی شوند.
- dependencyها ضروری و license آن‌ها مشخص باشد.
- version در header/package/changelog/tag هماهنگ باشد.
- deprecated APIها بررسی شوند.

### Testing

حداقل سناریوها:

| سناریو | نتیجه مورد انتظار |
|---|---|
| Clean install | نصب بدون خطای fatal |
| Activation | activation موفق |
| Core feature | همه سناریوهای اصلی موفق |
| Update | migration و compatibility موفق |
| Deactivation | رفتار تعریف‌شده حفظ شود |
| Uninstall | حذف داده طبق policy |
| RTL/mobile | UI صحیح |
| Browser | browserهای هدف صحیح |
| Security | authorization/escaping/nonce صحیح |

### Packaging

ZIP باید فقط artifactهای لازم را داشته باشد. `.env`، backup، cache، local configuration، credential، dump و فایل‌های توسعه‌ای غیرضروری نباید داخل آن باشند.

### Zhaket Rules

**نیاز به بررسی:** قوانین جاری استور ژاکت، محدودیت حجم/ابعاد تصاویر، فرمت فایل‌ها، metadata اجباری، policy licensing و الزامات تجاری باید دقیقاً در زمان submit از مرجع رسمی ژاکت کنترل شوند.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- WordPress و PHP در محدوده پشتیبانی محصول.
- WP-CLI.
- Composer 2.x و npm در صورت کاربرد.
- PHPCS/WPCS، PHPStan و PHPUnit.
- Lighthouse/PageSpeed.
- Browser DevTools.
- ZIP tool یا build script قابل تکرار.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. feature freeze کنید.
2. issueهای open و blockerها را ببندید.
3. version و changelog را نهایی کنید.
4. dependency و license audit انجام دهید.
5. lint/static analysis/test را اجرا کنید.
6. clean WordPress نصب کنید.
7. محصول را install و activate کنید.
8. سناریوهای اصلی را اجرا کنید.
9. update از حداقل نسخه قبلی را تست کنید.
10. deactivation/uninstall را تست کنید.
11. RTL/mobile/accessibility/browser را تست کنید.
12. performance و console/network error را بررسی کنید.
13. source و artifact را برای secret/debug scan کنید.
14. documentation، FAQ و screenshots را نهایی کنید.
15. demo را با version محصول هماهنگ کنید.
16. ZIP را از صفر بسازید.
17. ZIP را در محیط تمیز extract و نصب کنید.
18. قوانین جاری ژاکت را دوباره بررسی کنید.
19. checksum و release commit/tag را ثبت کنید.
20. rollback/recovery plan را مشخص کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- انتشار build از working tree آلوده.
- mismatch نسخه و changelog.
- secret یا `.env` در ZIP.
- تست فقط روی محیط توسعه.
- تست نکردن update.
- screenshot قدیمی یا دارای داده خصوصی.
- مستندات بدون requirements و troubleshooting.
- dependency license نامشخص.
- نبود rollback plan.

## 7. مثال‌های کد یا نمونه واقعی

build قابل تکرار:

```bash
composer install --no-dev --optimize-autoloader
npm ci
npm run build
```

سپس artifact را از فایل‌های تعریف‌شده در release manifest بسازید؛ صرفاً کل working directory را ZIP نکنید.

## 8. نکات امنیتی و عملکردی

secretها باید خارج از Git و artifact باشند. داده مشتری در screenshots/demo ممنوع است. debug display خاموش باشد. dependencyهای production حداقلی باشند. assetها minify و cacheable باشند. performance regressionهای مهم قبل از release اندازه‌گیری شوند.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- WordPress Plugin Handbook: https://developer.wordpress.org/plugins/
- WordPress Theme Handbook: https://developer.wordpress.org/themes/
- WordPress Coding Standards: https://developer.wordpress.org/coding-standards/
- نیاز به بررسی: قوانین جاری استور ژاکت و الزامات submit در زمان انتشار.

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] code freeze و review کامل است.
- [ ] version/changelog/tag هماهنگ‌اند.
- [ ] lint/static analysis/test موفق‌اند.
- [ ] clean install موفق است.
- [ ] update از نسخه قبلی موفق است.
- [ ] activation/deactivation/uninstall تست شده است.
- [ ] security review انجام شده است.
- [ ] RTL/mobile/accessibility/browser تست شده‌اند.
- [ ] demo و screenshots به‌روز هستند.
- [ ] ZIP فقط artifactهای لازم را دارد.
- [ ] secret/debug/local files حذف شده‌اند.
- [ ] قوانین جاری ژاکت بررسی شده‌اند.
- [ ] rollback/recovery strategy مشخص است.

## به‌روزرسانی بعدی

