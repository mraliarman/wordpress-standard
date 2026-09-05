# استاندارد پشتیبانی مشتریان و مدیریت تیکت

این سند استاندارد عملیاتی تیم برای دریافت، تحلیل، اولویت‌بندی، پاسخ، escalation، پیگیری و بستن تیکت مشتری است. هدف، تبدیل پشتیبانی از پاسخ‌گویی موردی به فرآیندی قابل اندازه‌گیری است که feedback مشتری را به bug fix، documentation، FAQ یا بهبود محصول تبدیل می‌کند.

## 2. اهداف و دامنه (Scope)

دامنه شامل ticket intake، severity، پاسخ اولیه، جمع‌آوری evidence، bug escalation، communication، resolution، closure و knowledge base است. تعهدات حقوقی، مالی و SLA قراردادی فقط در صورت وجود قرارداد رسمی معتبر هستند.

## 3. استانداردها و اصول اصلی (Best Practices)

### اصول ارتباط

- ابتدا مسئله مشتری را با زبان ساده بازگو کنید.
- مشتری را مقصر ندانید.
- پاسخ باید وضعیت فعلی، اقدام بعدی و owner را مشخص کند.
- زمان قطعی فقط زمانی اعلام شود که واقعاً تعهد شده است.
- پاسخ فنی باید قابل فهم و actionable باشد.
- هر تصمیم مهم داخل ticket ثبت شود.

### اطلاعات لازم برای Bug

- نسخه محصول.
- WordPress/PHP و environment.
- browser در صورت frontend issue.
- steps to reproduce.
- expected behavior.
- actual behavior.
- screenshot یا log redact شده در صورت نیاز.
- زمان رخداد در صورت اهمیت.

هرگز password، credential یا secret درخواست نکنید.

### Severity

| سطح | تعریف | اقدام |
|---|---|---|
| Critical | outage، data loss یا security exposure جدی | escalation فوری |
| High | قابلیت اصلی برای تعداد قابل توجهی از کاربران مختل | اولویت بالا |
| Medium | مشکل قابل workaround | صف عادی |
| Low | سوال، cosmetic یا improvement | برنامه‌ریزی |

Severity باید بر اساس impact و reproducibility تعیین شود، نه صرفاً لحن مشتری.

### Feedback Loop

هر issue تکرارشونده باید در یکی از این مسیرها قرار گیرد: fix، FAQ، documentation، automation یا product improvement.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- Helpdesk/CRM مورد تأیید سازمان.
- GitHub Issues/Projects برای engineering work در صورت مناسب بودن repository.
- Markdown/knowledge base برای documentation.
- Screenshot و log collection امن.

ابزار خاص نباید باعث ذخیره credential یا داده حساس مشتری شود.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. ticket را دریافت و category کنید.
2. duplicate و known issue را بررسی کنید.
3. severity و impact را تعیین کنید.
4. اطلاعات ناقص را با کمترین درخواست لازم تکمیل کنید.
5. reproduction را انجام دهید.
6. root cause یا hypothesis را ثبت کنید.
7. در صورت bug، engineering issue ایجاد و link کنید.
8. owner و next step تعیین کنید.
9. پاسخ status را به مشتری بدهید.
10. fix را روی محیط امن تست کنید.
11. نتیجه را با نسخه fix شده ثبت کنید.
12. پاسخ نهایی و workaround در صورت وجود را ارسال کنید.
13. ticket را طبق policy ببندید.
14. issueهای تکراری را به FAQ/KB منتقل کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- پاسخ کلی بدون next step.
- درخواست credential.
- blame کردن مشتری.
- اعلام ETA قطعی بدون کنترل.
- بستن ticket بدون ثبت solution.
- ارسال log حاوی PII/secret.
- ساخت issue فنی بدون reproduction.
- تکرار پاسخ یکسان بدون توجه به context.

## 7. مثال‌های کد یا نمونه واقعی

قالب گزارش داخلی:

```text
Title: فرم رزرو با PHP 8.3 خطای 500 می‌دهد
Product: Example Plugin 2.4.1
Environment: WordPress 6.x / PHP 8.3
Steps: 1) ... 2) ... 3) ...
Expected: فرم ذخیره شود
Actual: HTTP 500
Severity: High
Evidence: sanitized log attached
Workaround: ...
Owner: Engineering
```

## 8. نکات امنیتی و عملکردی

ticket system باید حداقل داده لازم را نگه دارد. log قبل از ارسال redact شود. secret، session token، password و PII غیرضروری حذف شوند. در performance issue، baseline و after-fix metric ثبت شود.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- WordPress Developer: https://developer.wordpress.org/
- OWASP Logging Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html
- OWASP: https://owasp.org/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] category و severity مشخص است.
- [ ] reproduction یا علت محتمل ثبت شده است.
- [ ] پاسخ محترمانه و actionable است.
- [ ] owner و next step مشخص‌اند.
- [ ] credential درخواست نشده است.
- [ ] evidence حساس redact شده است.
- [ ] engineering issue در صورت نیاز ساخته شده است.
- [ ] solution و version fix ثبت شده‌اند.
- [ ] FAQ/KB در موارد تکراری به‌روز شده است.

## به‌روزرسانی بعدی

