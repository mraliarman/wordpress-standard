# ساخت پیش‌نمایش و Demo محصول

این سند استاندارد ساخت Preview/Demo برای محصول دیجیتال، مخصوصاً theme/plugin وردپرس، است تا کاربر پیش از خرید ساختار، کیفیت و نتیجه محصول را واضح ببیند.

## 2. اهداف و دامنه (Scope)

پوشش: demo structure، sample content، screenshots، live demo، UI presentation و کنترل داده. طراحی کمپین تبلیغاتی خارج از دامنه است.

## 3. استانداردها و اصول اصلی (Best Practices)

- demo باید سریع، پایدار و نزدیک به تجربه واقعی محصول باشد.
- محتوای نمونه باید کامل و باورپذیر باشد؛ placeholderهای بی‌کیفیت استفاده نشود.
- مسیرهای مهم محصول را در demo قابل دسترسی کنید.
- screenshotها باید واقعی، خوانا و بدون اطلاعات خصوصی باشند.
- نسبت تصویر و کیفیت screenshots یکدست باشد.
- صفحه landing demo باید value proposition، امکانات کلیدی و لینک مشاهده را روشن کند.
- اطلاعات ورود demo در صورت نیاز محدود و قابل reset باشد.
- از داده واقعی مشتری در preview استفاده نکنید.
- demo باید در mobile و desktop تست شود.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- مرورگرهای Chrome/Firefox/Edge/Safari برای تست.
- DevTools برای بررسی responsive/performance.
- Lighthouse/PageSpeed برای performance.
- ابزار screenshot با خروجی PNG/WebP با کیفیت مناسب.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. مهم‌ترین سناریوهای خرید را تعیین کنید.
2. محتوای نمونه واقعی بسازید.
3. theme/plugin را نصب و تنظیم کنید.
4. صفحات کلیدی را آماده کنید.
5. navigation و CTAها را تست کنید.
6. demo را روی URL پایدار deploy کنید.
7. cache و assetها را بهینه کنید.
8. screenshots از صفحات کلیدی بگیرید.
9. mobile/desktop/browser را تست کنید.
10. reset procedure برای demo تعریف کنید.
11. لینک‌های شکسته و console error را بررسی کنید.
12. در هر release، demo را با نسخه محصول هماهنگ کنید.

ساختار پیشنهادی:

```text
preview/
├── landing
├── screenshots
├── demo-notes.md
└── reset.md
```

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- demo با نسخه محصول متفاوت.
- broken links.
- صفحه خالی یا محتوای lorem ipsum.
- screenshot قدیمی.
- داده خصوصی.
- demo کند یا پر از plugin اضافی.
- login demo که پس از مدتی قفل می‌شود.

## 7. مثال‌های کد یا نمونه واقعی

نمونه CTA:

```html
<a href="/demo/" class="inline-flex rounded-lg px-5 py-3 font-semibold">
    مشاهده دمو
</a>
```

## 8. نکات امنیتی و عملکردی

حساب demo حداقل permission را داشته باشد. امکان دسترسی به تنظیمات حساس، ایمیل واقعی، payment و داده کاربران را حذف کنید. cache و CDN را بررسی و third-party scriptها را محدود کنید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Lighthouse: https://developer.chrome.com/docs/lighthouse/
- Web performance: https://web.dev/fast/
- WordPress: https://developer.wordpress.org/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] demo با نسخه محصول یکسان است.
- [ ] سناریوهای اصلی قابل مشاهده‌اند.
- [ ] mobile/desktop تست شده است.
- [ ] screenshots به‌روز و بدون داده خصوصی‌اند.
- [ ] لینک‌ها سالم‌اند.
- [ ] console error وجود ندارد.
- [ ] performance قابل قبول است.
- [ ] reset و maintenance procedure ثبت شده است.

## به‌روزرسانی بعدی

