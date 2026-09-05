# استاندارد ساخت Product Preview و Demo

این سند استاندارد ساخت preview، live demo، sample content و screenshots برای محصولات دیجیتال، به‌ویژه WordPress theme/plugin است. Preview باید پیش از خرید ارزش واقعی محصول را منتقل کند و هم‌زمان نماینده دقیق نسخه‌ای باشد که مشتری دریافت می‌کند؛ بنابراین demo بخشی از release quality است، نه یک صفحه تبلیغاتی جدا از محصول.

## 2. اهداف و دامنه (Scope)

دامنه شامل demo architecture، sample content، landing page، screenshots، live demo، access control، reset، performance و visual QA است. کمپین تبلیغاتی و pricing خارج از دامنه است.

## 3. استانداردها و اصول اصلی (Best Practices)

### Demo

- demo باید با نسخه release محصول هماهنگ باشد.
- سناریوهای اصلی کاربر باید بدون جست‌وجوی زیاد قابل مشاهده باشند.
- sample content کامل، فارسی/RTL در صورت محصول فارسی و باورپذیر باشد.
- lorem ipsum و صفحه خالی ممنوع.
- اطلاعات واقعی مشتری ممنوع.
- demo account حداقل permission را داشته باشد.
- reset procedure مشخص و قابل اجرا باشد.

### Screenshots

هر screenshot باید:

- نماینده قابلیت واقعی باشد.
- خوانا و بدون داده خصوصی باشد.
- نسخه UI جاری را نمایش دهد.
- از نظر ابعاد و نسبت تصویر با سایر تصاویر یکدست باشد.
- در صورت نیاز annotation محدود و واضح داشته باشد.

### Preview Information Architecture

Landing preview بهتر است شامل این بخش‌ها باشد:

1. value proposition.
2. قابلیت‌های کلیدی.
3. تصاویر واقعی.
4. سناریوهای کاربرد.
5. live demo.
6. requirements و compatibility.
7. documentation.
8. FAQ و limitations.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- Chrome، Firefox، Edge و Safari برای browser QA در صورت پشتیبانی محصول.
- DevTools.
- Lighthouse/PageSpeed.
- ابزار screenshot با خروجی lossless یا optimized.
- WordPress staging.
- ابزار reset یا database snapshot کنترل‌شده.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. target audience و سناریوهای اصلی را مشخص کنید.
2. featureهای مهم را اولویت‌بندی کنید.
3. sample content بسازید.
4. محصول release candidate را نصب کنید.
5. demo configuration را اعمال کنید.
6. navigation و CTAها را تست کنید.
7. access control و reset را پیاده و تست کنید.
8. screenshots واقعی بگیرید.
9. desktop/mobile/browser را تست کنید.
10. Lighthouse و console/network را بررسی کنید.
11. لینک‌های داخلی و external را کنترل کنید.
12. demo را با release version تطبیق دهید.
13. داده خصوصی را دوباره audit کنید.
14. maintenance و reset procedure را مستند کنید.

ساختار پیشنهادی:

```text
preview/
├── landing/
├── screenshots/
├── demo-notes.md
├── reset.md
└── compatibility.md
```

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- demo قدیمی‌تر از محصول.
- screenshot قدیمی.
- broken link.
- sample content ناقص.
- داده خصوصی یا credential در تصویر.
- demo بسیار کند.
- دسترسی بیش از حد demo account.
- نبود reset و پس از مدتی خراب شدن demo.

## 7. مثال‌های کد یا نمونه واقعی

نمونه CTA semantic:

```html
<a href="/demo/" class="inline-flex items-center rounded-lg px-5 py-3 font-semibold">
    مشاهده دمو
</a>
```

## 8. نکات امنیتی و عملکردی

demo account باید least privilege داشته باشد. payment، email واقعی، export داده و settings حساس نباید قابل سوءاستفاده باشند. rate limit و monitoring در صورت عمومی بودن demo در نظر گرفته شود. third-party scriptها محدود و assetها cacheable باشند.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Lighthouse: https://developer.chrome.com/docs/lighthouse/
- Web Performance: https://web.dev/fast/
- WordPress Developer: https://developer.wordpress.org/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] demo دقیقاً با release candidate هماهنگ است.
- [ ] سناریوهای اصلی قابل مشاهده‌اند.
- [ ] sample content کامل و باورپذیر است.
- [ ] screenshots واقعی و بدون داده خصوصی‌اند.
- [ ] desktop/mobile/browser تست شده‌اند.
- [ ] console و network خطای غیرمنتظره ندارند.
- [ ] performance بررسی شده است.
- [ ] demo account least privilege دارد.
- [ ] reset procedure مستند و تست شده است.
- [ ] compatibility و limitations مشخص‌اند.

## به‌روزرسانی بعدی

