# استاندارد گردش‌کار استفاده از دستیار هوش مصنوعی

این سند چارچوب استفاده حرفه‌ای، امن و قابل کنترل از AI در توسعه نرم‌افزار است. AI در این repository نقش دستیار تحلیل، coding، debugging، refactoring، documentation و review اولیه را دارد و هرگز جایگزین مالکیت مهندس، تست، code review یا تصمیم معماری نیست. مرجع اصلی اعلام‌شده تیم `https://llm.bestjustify.ir/` است؛ در آخرین بررسی محیطی، دسترسی مستقیم به محتوای آن ممکن نبود، بنابراین خلاصه‌ای از محتوای اختصاصی آن بدون مشاهده منبع ادعا نمی‌شود و این مورد «نیاز به بررسی» است.

## 2. اهداف و دامنه (Scope)

دامنه شامل prompt engineering، context management، coding assistant، debugging، refactoring، documentation، review، validation و security hygiene است. تصمیم‌های نهایی architecture، merge و release در اختیار انسان مسئول باقی می‌ماند.

## 3. استانداردها و اصول اصلی (Best Practices)

### Prompt Contract

هر prompt مهم باید تا حد امکان شامل این موارد باشد:

```text
Role
Goal
Context
Current behavior
Expected behavior
Constraints
Affected files
Output format
Acceptance criteria
Validation requirements
```

### اصل Context حداقلی ولی کافی

تمام repository را بدون نیاز ارسال نکنید. فقط فایل‌ها، نسخه‌ها، errorها، interfaces و constraints مؤثر را ارائه کنید. اما context حیاتی را نیز حذف نکنید؛ پاسخ AI بدون context کافی قابل اعتماد نیست.

### AI Change Protocol

1. ابتدا مسئله را خلاصه کنید.
2. assumptions را مشخص کنید.
3. affected files را تعیین کنید.
4. plan کوتاه بدهید.
5. کوچک‌ترین patch لازم را تولید کنید.
6. diff را review کنید.
7. test/lint/static analysis اجرا کنید.
8. security/performance impact را بررسی کنید.
9. regression test اضافه کنید.
10. سپس commit/merge کنید.

### Validation

هیچ API، package، hook، function، class یا command ناشناخته‌ای صرفاً چون AI پیشنهاد داده پذیرفته نشود. نسخه documentation و compatibility باید بررسی شود.

### محرمانگی

secret، token، credential، private key، PII و داده حساس مشتری را وارد prompt نکنید مگر محیط و policy سازمان صریحاً مجاز کرده باشد. نمونه‌سازی باید با داده synthetic انجام شود.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

ابزار AI خاصی الزام‌آور نیست؛ ابزار باید با policy امنیتی و دسترسی repository سازگار باشد. برای validation از stack واقعی پروژه استفاده کنید:

- PHPStan
- PHPCS/WPCS
- PHPUnit
- Browser DevTools
- Lighthouse
- Git diff/PR review
- CI pipeline

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. requirement را دقیق بنویسید.
2. repository rules را در اختیار AI قرار دهید.
3. versionهای PHP/WordPress/Tailwind/Node را مشخص کنید.
4. expected/actual را ثبت کنید.
5. AI را وادار به اعلام assumptions کنید.
6. affected files را مشخص کنید.
7. patch کوچک دریافت کنید.
8. diff را خط‌به‌خط review کنید.
9. dependency و APIهای جدید را verify کنید.
10. lint/static analysis/test اجرا کنید.
11. security review انجام دهید.
12. performance regression را در صورت کاربرد بررسی کنید.
13. regression test اضافه کنید.
14. documentation را به‌روز کنید.
15. commit استاندارد و قابل ردیابی ایجاد کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- prompt مبهم.
- context ناقص.
- اعتماد به hallucinated API.
- نصب dependency بدون بررسی.
- refactor بزرگ بدون test.
- ارسال secret.
- قبول کردن code فقط چون compile می‌شود.
- نادیده گرفتن compatibility WordPress/PHP.
- درخواست rewrite کامل وقتی patch کوچک کافی است.

## 7. مثال‌های کد یا نمونه واقعی

نمونه prompt برای debugging:

```text
نقش: مهندس ارشد WordPress/PHP
هدف: پیدا کردن root cause خطای 500
Context: WordPress 6.x، PHP 8.3، plugin version 2.4.1
Actual: POST به /wp-admin/admin-ajax.php با HTTP 500 شکست می‌خورد
Expected: درخواست با capability مناسب ذخیره شود
Constraints: schema تغییر نکند؛ API عمومی حفظ شود
Affected files: src/Admin/Example.php و assets/admin.js
Output: ابتدا root cause و affected code، سپس patch حداقلی و regression test
Acceptance: PHPCS، PHPStan و PHPUnit بدون خطا
```

## 8. نکات امنیتی و عملکردی

خروجی AI را untrusted code در نظر بگیرید. XSS، SQL injection، CSRF، privilege escalation، SSRF، file upload و dependency risk را بررسی کنید. prompt injection نیز در سیستم‌هایی که AI با داده خارجی کار می‌کند باید در threat model لحاظ شود. هیچ دستور تولیدشده توسط AI نباید بدون بررسی در production اجرا شود.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- مرجع اصلی داخلی: https://llm.bestjustify.ir/ — **نیاز به بررسی:** دسترسی و استخراج محتوای جاری.
- WordPress Developer: https://developer.wordpress.org/
- PHP Manual: https://www.php.net/docs.php
- OWASP: https://owasp.org/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] goal/context/constraint مشخص است.
- [ ] assumptions شناسایی شده‌اند.
- [ ] secret یا داده حساس غیرضروری ارسال نشده است.
- [ ] API و dependencyهای پیشنهادی verify شده‌اند.
- [ ] diff انسانی review شده است.
- [ ] lint/static analysis/test موفق است.
- [ ] security review انجام شده است.
- [ ] performance impact بررسی شده است.
- [ ] regression test در صورت نیاز اضافه شده است.
- [ ] documentation به‌روز شده است.
- [ ] commit قابل ردیابی است.

## به‌روزرسانی بعدی

