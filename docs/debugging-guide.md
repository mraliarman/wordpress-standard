# راهنمای رفع ایراد و باگ

این سند روش سیستماتیک عیب‌یابی پروژه‌های PHP/WordPress و JavaScript را تعریف می‌کند؛ هدف این است که به‌جای حدس، از reproduction، log، isolation و regression test استفاده شود.

## 2. اهداف و دامنه (Scope)

پوشش: PHP، WordPress، JavaScript، database، network، staging، logging و Xdebug. incident management سازمانی خارج از دامنه است.

## 3. استانداردها و اصول اصلی (Best Practices)

- ابتدا bug را reproduce کنید و دقیقاً URL، user role، input، نسخه و محیط را ثبت کنید.
- تغییر همزمان چند چیز ممنوع؛ یک فرضیه را در هر مرحله آزمایش کنید.
- محیط production را مستقیم برای آزمایش destructive استفاده نکنید.
- در WordPress از `WP_DEBUG` و log فایل استفاده کنید و نمایش خطا را در production خاموش نگه دارید.
- Query Monitor برای query، hooks، HTTP request، PHP errors و performance مفید است.
- Xdebug را برای breakpoint، stack trace و step debugging در local/staging تنظیم کنید.
- خطا را در سه لایه جدا کنید: server/PHP، WordPress/backend، browser/JS.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- Xdebug 3.x سازگار با PHP نصب‌شده.
- Query Monitor نسخه سازگار با WordPress.
- Browser DevTools.
- WP-CLI.
- PHPStan، PHPCS و PHPUnit.
- ابزار log سرور و access/error log وب‌سرور.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. Severity و impact را تعیین کنید.
2. reproduction steps بنویسید.
3. آخرین تغییرات Git را بررسی کنید.
4. PHP error log و browser console را بخوانید.
5. Network tab و response status را بررسی کنید.
6. Query Monitor را برای SQL/HTTP/hooks بررسی کنید.
7. با Xdebug وارد مسیر اجرای مشکل شوید.
8. مشکل را به کوچک‌ترین component ممکن isolate کنید.
9. fix حداقلی اعمال کنید.
10. regression test اضافه کنید.
11. روی staging تست کنید.
12. deploy و monitor کنید.

نمونه تنظیم debug در توسعه:

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

در production مقدارها باید بر اساس سیاست امنیتی تیم تنظیم شوند و stack trace یا secret به visitor نمایش داده نشود.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- تغییر مستقیم production بدون reproduction.
- پاک کردن log قبل از جمع‌آوری evidence.
- تمرکز روی اولین error در حالی که root cause قبل‌تر رخ داده است.
- خاموش کردن error به‌جای رفع آن.
- تست فقط با admin و فراموش کردن نقش کاربر عادی.
- اصلاح bug بدون regression test.

## 7. مثال‌های کد یا نمونه واقعی

```js
fetch('/wp-admin/admin-ajax.php', {
    method: 'POST',
    body: formData
})
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error(error));
```

برای خطای JS ابتدا Console و Network را جدا بررسی کنید؛ HTTP 200 الزاماً به معنی موفقیت منطقی نیست.

## 8. نکات امنیتی و عملکردی

debug display در production خطر افشای مسیر فایل، SQL و secret دارد. logها باید دسترسی محدود، retention مشخص و حذف/rotation داشته باشند. داده حساس را log نکنید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- WordPress Developer: https://developer.wordpress.org/
- Query Monitor: https://querymonitor.com/
- Xdebug: https://xdebug.org/docs/
- PHP errors: https://www.php.net/manual/en/language.errors.php

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] reproduction مستند است.
- [ ] root cause مشخص است.
- [ ] fix حداقلی و قابل توضیح است.
- [ ] log/debug evidence جمع‌آوری شده است.
- [ ] regression test وجود دارد.
- [ ] staging تست شده است.
- [ ] production اطلاعات debug نمایش نمی‌دهد.

## به‌روزرسانی بعدی

