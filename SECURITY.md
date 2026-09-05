# سیاست امنیتی

این repository شامل استانداردهای توسعه است. مسائل امنیتی واقعی را در issue عمومی با جزئیات exploit یا secret منتشر نکنید.

## گزارش آسیب‌پذیری

برای گزارش موارد حساس، از کانال خصوصی امنیتی مورد تأیید مالک repository استفاده کنید. اگر کانال خصوصی از قبل تعریف نشده است، «نیاز به بررسی» است و باید قبل از انتشار محصول یک روش گزارش‌دهی امن تعیین شود.

## اطلاعاتی که نباید ارسال شود

- password و credential
- API key و access token
- اطلاعات پرداخت
- داده شخصی مشتری
- فایل `.env`
- نمونه exploit قابل سوءاستفاده در issue عمومی

## اصول توسعه امن

تمام کدهای PHP باید ورودی را validate/sanitize، خروجی را escape و authorization را با capability کنترل کنند. عملیات state-changing باید در برابر CSRF با nonce مناسب محافظت شوند. Queryهای دارای ورودی باید parameterized باشند.

Dependencyها باید از منابع معتبر نصب، نسخه‌ها lock و به‌صورت دوره‌ای audit شوند. debug output و stack trace نباید در production برای کاربر نمایش داده شود.

## مدیریت رخداد

پس از کشف secret یا credential، آن را revoke/rotate کنید؛ صرفاً حذف فایل از آخرین commit کافی نیست. شدت رخداد، affected versions، mitigation و وضعیت patch باید ثبت شود.

## مراجع

- https://developer.wordpress.org/plugins/security/
- https://owasp.org/www-project-top-ten/
- https://www.php.net/manual/en/security.php
