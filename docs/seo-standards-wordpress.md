# استاندارد SEO و Performance در WordPress

این سند استاندارد سئوی تکنیکال و performance در WordPress است و crawlability، indexability، metadata، headings، URL، links، images، mobile، structured data، canonical، sitemap، robots و Core Web Vitals را پوشش می‌دهد. هدف، جلوگیری از این است که theme/plugin به‌صورت ناخواسته سیگنال‌های متناقض SEO یا performance ایجاد کند.

## 2. اهداف و دامنه (Scope)

این سند روی implementation فنی تمرکز دارد. استراتژی محتوا، link building، digital PR و campaign خارج از دامنه است. تنظیمات افزونه SEO باید با معماری theme هماهنگ باشد و مالکیت هر خروجی فقط یک محل مشخص داشته باشد.

## 3. استانداردها و اصول اصلی (Best Practices)

### Crawl و Index

- صفحات قابل index باید عمداً قابل crawl باشند.
- `robots.txt` و meta robots نباید ناخواسته صفحه مهم را مسدود کنند.
- canonical باید یکتا و با URL واقعی هماهنگ باشد.
- sitemap باید فقط URLهای مناسب index را معرفی کند.
- 404، redirect و canonical chain بررسی شوند.

### Metadata و structure

- title و meta description بر اساس نوع صفحه تولید شوند.
- theme و SEO plugin نباید title/canonical/schema را duplicate کنند.
- headingها semantic باشند و برای ظاهر صرفاً از heading level استفاده نشود.
- HTML semantic و لینک‌های crawlable استفاده شود.
- anchor text باید معنای مقصد را منتقل کند.

### Images

- `alt` توصیفی برای تصویر محتوایی و خالی برای تصویر صرفاً تزئینی.
- width/height مناسب برای کاهش layout shift.
- فرمت و اندازه image متناسب با کاربرد.
- lazy loading برای تصاویر غیر بحرانی؛ LCP image نباید کورکورانه lazy شود.
- `srcset`/responsive image در صورت امکان استفاده شود.

### Core Web Vitals

معیارهای اصلی Core Web Vitals عبارت‌اند از LCP، INP و CLS. اهداف رایج «good» به‌ترتیب ≤2.5s، ≤200ms و ≤0.1 هستند؛ thresholdهای جاری باید از منبع رسمی Google در زمان audit کنترل شوند.

### Structured Data

- schema باید با محتوای قابل مشاهده و واقعی صفحه سازگار باشد.
- از داده ساختاریافته برای ادعای اطلاعاتی که واقعاً در صفحه نیست استفاده نشود.
- JSON-LD یا روش منتخب باید ownership مشخص داشته باشد.
- schema را با validator رسمی/مناسب بررسی کنید.

### URL

URL باید پایدار، خوانا و قابل پیش‌بینی باشد. تغییر URL بدون redirect strategy می‌تواند باعث افت crawl و link equity شود.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

| ابزار | کاربرد |
|---|---|
| Google Search Console | index، query و technical issues |
| PageSpeed Insights | field/lab performance |
| Lighthouse | performance/accessibility/SEO audit |
| Chrome DevTools | network، rendering و performance |
| Schema validator | بررسی structured data |
| یک SEO plugin | metadata/sitemap/schema در صورت نیاز |

همزمان چند SEO engine را برای تولید یک خروجی فعال نکنید.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. URLهای مهم و نوع pageها را inventory کنید.
2. indexability و robots را بررسی کنید.
3. sitemap را بررسی کنید.
4. canonical و redirectها را crawl کنید.
5. title، description و headingها را بررسی کنید.
6. internal links و anchor text را بررسی کنید.
7. image alt، dimensions و loading را بررسی کنید.
8. mobile rendering و viewport را تست کنید.
9. LCP، INP و CLS را اندازه‌گیری کنید.
10. render-blocking resource و third-party scriptها را بررسی کنید.
11. structured data را validate کنید.
12. theme و SEO plugin را برای duplicate output بررسی کنید.
13. 404، pagination، archive و search behavior را بررسی کنید.
14. بعد از release دوباره Search Console و performance را monitor کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- دو title یا canonical.
- noindex ناخواسته.
- sitemap شامل URLهای noindex.
- schema جعلی.
- alt پر از keyword.
- lazy loading عنصر LCP.
- image بدون dimensions.
- JavaScript سنگین و third-party غیرضروری.
- redirect chain.
- تغییر slug بدون redirect.

## 7. مثال‌های کد یا نمونه واقعی

نمونه semantic image:

```html
<img src="example.webp" alt="نمایش داشبورد مدیریت فروشگاه" width="1200" height="800" loading="lazy">
```

نمونه JSON-LD باید فقط داده واقعی را شامل شود:

```html
<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "Organization",
    "name": "Example"
}
</script>
```

## 8. نکات امنیتی و عملکردی

داده خام user را مستقیماً وارد JSON-LD یا HTML نکنید؛ context-aware encoding لازم است. third-party scriptها را محدود کنید. font، CSS و image را بهینه کنید. caching باید همراه با cache invalidation درست باشد. performance regression باید در releaseهای مهم بررسی شود.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Google Search Essentials: https://developers.google.com/search/docs/essentials
- Core Web Vitals: https://developers.google.com/search/docs/appearance/core-web-vitals
- Schema.org: https://schema.org/
- WordPress Developer: https://developer.wordpress.org/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] indexability صحیح است.
- [ ] robots/sitemap/canonical بدون conflict هستند.
- [ ] title/meta و headingها صحیح‌اند.
- [ ] URL و redirect strategy بررسی شده است.
- [ ] images دارای alt و dimensions مناسب‌اند.
- [ ] mobile تست شده است.
- [ ] Core Web Vitals اندازه‌گیری شده‌اند.
- [ ] structured data معتبر و واقعی است.
- [ ] third-party scriptهای غیرضروری حذف شده‌اند.
- [ ] با SEO plugin duplicate output وجود ندارد.
- [ ] post-release monitoring برنامه‌ریزی شده است.

## به‌روزرسانی بعدی

