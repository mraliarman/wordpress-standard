# راهنمای سیستماتیک Debugging و رفع باگ

این سند فرآیند مهندسی عیب‌یابی PHP، WordPress، JavaScript، database و network را تعریف می‌کند. اصل اصلی این است که debugging یک فرآیند evidence-based است: ابتدا reproduction و شواهد، سپس isolation، root cause، fix و regression test؛ نه تغییرات تصادفی تا زمانی که خطا ناپدید شود.

## 2. اهداف و دامنه (Scope)

دامنه شامل local، staging و production diagnosis، PHP errors، WordPress hooks، database، AJAX/REST، browser، network، logging، Query Monitor و Xdebug است. مدیریت سازمانی incident خارج از این سند است، اما severity و escalation پایه پوشش داده می‌شود.

## 3. استانداردها و اصول اصلی (Best Practices)

### مدل چهار لایه

1. **Infrastructure:** DNS، web server، PHP-FPM، permissions، disk، memory.
2. **PHP/WordPress:** fatal، warning، hook، template، plugin/theme conflict.
3. **Data:** SQL، cache، option، transient، migration.
4. **Browser:** JavaScript، CSS، network، cookies، CORS و response.

### قواعد debugging

- bug را با همان input و role بازتولید کنید.
- actual و expected را جدا بنویسید.
- نسخه WordPress، PHP، browser، plugin/theme و commit را ثبت کنید.
- آخرین تغییرات Git را بررسی کنید.
- یک فرضیه را در هر مرحله آزمایش کنید.
- log را قبل از تغییرات destructive جمع‌آوری کنید.
- root cause را از symptom جدا کنید.
- fix حداقلی و قابل توضیح باشد.
- هر bug مهم باید regression test داشته باشد.

### WordPress debug

در local/staging:

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

در production نمایش خطا نباید فعال باشد. policy واقعی hosting و monitoring باید بررسی شود.

### JavaScript

Console به‌تنهایی کافی نیست. Console، Network، DOM، source، status code و response body را با هم بررسی کنید. HTTP 200 الزاماً موفقیت منطقی نیست.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

| ابزار | کاربرد |
|---|---|
| Xdebug 3.x | breakpoint و stack trace |
| Query Monitor | query، hooks، HTTP، PHP و performance |
| Browser DevTools | JS/CSS/network |
| WP-CLI | isolation و maintenance |
| PHPStan | static defects |
| PHPCS/WPCS | coding defects |
| PHPUnit | regression/unit tests |
| Server logs | infrastructure/PHP evidence |

نسخه ابزار باید با PHP/WordPress محیط سازگار باشد.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. impact و severity را تعیین کنید.
2. reproduction دقیق بنویسید.
3. environment و versions را ثبت کنید.
4. Git diff و recent deploy را بررسی کنید.
5. PHP/web-server logs را بخوانید.
6. browser Console و Network را بررسی کنید.
7. Query Monitor را در WordPress فعال و query/hooks/HTTP را بررسی کنید.
8. با Xdebug مسیر execution را دنبال کنید.
9. dependency/plugin/theme conflict را isolate کنید.
10. cache و opcode/cache layer را در صورت نیاز بررسی کنید.
11. root cause را مستند کنید.
12. کوچک‌ترین fix صحیح را اعمال کنید.
13. regression test اضافه کنید.
14. lint/static analysis و test اجرا کنید.
15. staging را تست کنید.
16. deploy و post-deploy monitoring انجام دهید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- تغییر همزمان چند component.
- تست فقط با admin.
- پاک کردن log پیش از جمع‌آوری evidence.
- نسبت دادن symptom به root cause.
- خاموش کردن error به‌جای رفع آن.
- تست نکردن cache بعد از fix.
- اصلاح bug بدون regression test.
- debug روی production با نمایش خطا برای کاربر.

## 7. مثال‌های کد یا نمونه واقعی

AJAX را هم از نظر transport و هم business result بررسی کنید:

```js
fetch('/wp-admin/admin-ajax.php', {
    method: 'POST',
    body: formData
})
    .then((response) => {
        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }
        return response.json();
    })
    .then((data) => {
        if (!data.success) {
            throw new Error('Application request failed');
        }
    })
    .catch((error) => console.error(error));
```

## 8. نکات امنیتی و عملکردی

stack trace، filesystem path، SQL و secret نباید به visitor نمایش داده شوند. logها باید access control و rotation داشته باشند. password، token، cookie و PII را log نکنید. ابزارهای debug سنگین را فقط در محیط لازم فعال کنید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- WordPress Developer: https://developer.wordpress.org/
- Xdebug: https://xdebug.org/docs/
- Query Monitor: https://querymonitor.com/
- PHP Errors: https://www.php.net/manual/en/language.errors.php

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] severity و impact مشخص است.
- [ ] reproduction قابل اجراست.
- [ ] versions و environment ثبت شده‌اند.
- [ ] evidence جمع‌آوری شده است.
- [ ] root cause مشخص است.
- [ ] fix حداقلی و قابل توضیح است.
- [ ] regression test وجود دارد.
- [ ] lint/static analysis/test موفق است.
- [ ] staging تست شده است.
- [ ] production debug information افشا نمی‌کند.
- [ ] post-deploy monitoring انجام شده است.

## به‌روزرسانی بعدی

