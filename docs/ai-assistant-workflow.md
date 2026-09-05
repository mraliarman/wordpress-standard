# گردش‌کار استفاده از دستیار هوش مصنوعی در توسعه

این سند روش استفاده حرفه‌ای از AI به‌عنوان دستیار توسعه را تعریف می‌کند: نوشتن prompt، دادن context، تقسیم مسئله، بررسی خروجی، تست، امنیت و ثبت تصمیم‌ها. مرجع اصلی این سند منبع درخواستی تیم، https://llm.bestjustify.ir/ است؛ در زمان تدوین این فایل دسترسی مستقیم به محتوای سایت از ابزار مرور در دسترس نبود، بنابراین خلاصه‌ای از محتوای اختصاصی آن ادعا نمی‌شود و این مورد «نیاز به بررسی» است.

## 2. اهداف و دامنه (Scope)

پوشش: coding assistant، debugging، refactoring، documentation، review و prompt engineering. جایگزینی review انسانی، تست یا مسئولیت مهندس خارج از دامنه است.

## 3. استانداردها و اصول اصلی (Best Practices)

- prompt باید هدف، context، constraints، ورودی واقعی، خروجی مورد انتظار و معیار پذیرش را مشخص کند.
- مسئله بزرگ را به taskهای قابل تست تقسیم کنید.
- نسخه زبان/framework، ساختار فایل و خطای کامل را ارائه دهید.
- از AI بخواهید قبل از تغییر، assumptions و affected files را مشخص کند.
- خروجی را بدون review وارد production نکنید.
- هر patch باید lint، test، security review و regression test داشته باشد.
- برای کد حساس، خروجی AI را مانند کد شخص ثالث غیرقابل اعتماد بررسی کنید.
- secret، token، credential، PII و فایل خصوصی را در prompt ارسال نکنید مگر محیط و سیاست سازمان صریحاً اجازه دهد.
- برای debugging، reproduction و expected/actual behavior را دقیق ارائه کنید.
- برای refactor، رفتار موجود را invariant تعریف کنید و سپس تغییر دهید.

قالب پیشنهادی prompt:

```text
نقش: مهندس ارشد WordPress/PHP
هدف: [نتیجه دقیق]
Context: [نسخه‌ها، ساختار، فایل‌ها]
مشکل: [actual vs expected]
محدودیت‌ها: [framework، style، عدم تغییر API]
خروجی: [فایل/patch/توضیح]
معیار پذیرش: [testable checklist]
```

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

ابزار AI باید با policy تیم و repository permissions سازگار باشد. ابزارهای تست همان stack پروژه هستند: PHPUnit، PHPStan، PHPCS، Playwright/Cypress در صورت نیاز و browser DevTools.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. مسئله را دقیق تعریف کنید.
2. context حداقلی ولی کافی بدهید.
3. محدودیت‌ها و استانداردهای repo را اعلام کنید.
4. از AI بخواهید plan بدهد.
5. فایل‌های affected را تعیین کنید.
6. patch کوچک تولید کنید.
7. diff را review کنید.
8. lint/static analysis/test اجرا کنید.
9. security و performance را بررسی کنید.
10. regression test اضافه کنید.
11. commit message و changelog مناسب ثبت کنید.
12. نتیجه و تصمیم‌های مهم را مستند کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- prompt مبهم و انتظار خروجی دقیق.
- اعتماد به API یا version اشتباه.
- قبول کردن hallucinated function/class.
- refactor بزرگ بدون test.
- کپی کردن secret به prompt.
- درخواست «کد کامل» بدون repository context.

## 7. مثال‌های کد یا نمونه واقعی

نمونه درخواست خوب برای bug:

```text
در WordPress 6.x و PHP 8.x، صفحه /admin/example/ هنگام ارسال فرم با 403 برمی‌گردد.
Nonce action برابر example-save است. expected: ذخیره برای کاربران manage_options.
فایل‌های مرتبط: src/Admin/ExamplePage.php و assets/admin.js.
بدون تغییر schema، root cause را پیدا و patch حداقلی پیشنهاد کن و تست regression بده.
```

## 8. نکات امنیتی و عملکردی

AI ممکن است dependency ناامن، query آسیب‌پذیر، escaping ناقص یا API منسوخ پیشنهاد کند. dependency را قبل از نصب بررسی کنید. خروجی AI را از نظر XSS، SQL injection، CSRF، privilege escalation و SSRF بررسی کنید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- مرجع اصلی داخلی: https://llm.bestjustify.ir/ — نیاز به بررسی محتوای جاری و استخراج خلاصه رسمی.
- WordPress Developer: https://developer.wordpress.org/
- PHP Manual: https://www.php.net/docs.php

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] prompt هدف و معیار پذیرش دارد.
- [ ] نسخه‌ها و context مشخص‌اند.
- [ ] هیچ secret غیرضروری ارسال نشده است.
- [ ] diff انسانی review شده است.
- [ ] lint/static analysis/test موفق است.
- [ ] security و performance بررسی شده‌اند.
- [ ] regression test اضافه شده است.
- [ ] تصمیم‌ها و محدودیت‌های مهم مستند شده‌اند.

## به‌روزرسانی بعدی

