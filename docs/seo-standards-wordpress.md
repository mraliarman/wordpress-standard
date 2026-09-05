# استانداردهای SEO در WordPress

این سند اصول سئوی تکنیکال و پیاده‌سازی آن در قالب WordPress را تعریف می‌کند: crawlability، metadata، heading، URL، image، mobile، performance، structured data و سازگاری با افزونه‌های SEO. Google توصیه می‌کند محتوا people-first باشد، لینک‌ها crawlable باشند و برای image/JS/structured data نیز best practice رعایت شود. citeturn1search15

## 2. اهداف و دامنه (Scope)

پوشش: theme-level SEO و performance و markup. استراتژی محتوایی، link building و campaignهای خارج از کد در دامنه نیست.

## 3. استانداردها و اصول اصلی (Best Practices)

- `<title>`، canonical، robots و meta description نباید توسط theme و SEO plugin همزمان و متناقض تولید شوند.
- یک H1 منطقی برای محتوای اصلی داشته باشید؛ headingها بر اساس ساختار معنایی، نه ظاهر انتخاب شوند.
- URL کوتاه، پایدار، خوانا و ترجیحاً بر اساس slug باشد.
- لینک داخلی باید crawlable و دارای anchor text معنادار باشد.
- تصویر مهم `alt` توصیفی داشته باشد؛ تصویر تزئینی alt خالی داشته باشد.
- تصاویر responsive و با ابعاد مشخص برای جلوگیری از CLS ارائه شوند.
- lazy loading برای تصاویر غیر بحرانی مناسب است؛ LCP image را کورکورانه lazy نکنید.
- Core Web Vitals شامل LCP، INP و CLS است؛ اهداف «خوب» به‌ترتیب کمتر/برابر 2.5s، کمتر/برابر 200ms و کمتر/برابر 0.1 هستند. citeturn1search0
- structured data فقط بر اساس محتوای واقعاً موجود و نوع schema معتبر تولید شود.
- robots.txt، sitemap و canonical را با یک مالکیت مشخص مدیریت کنید.
- با افزونه‌های SEO مثل Yoast SEO یا Rank Math تداخل markup ایجاد نکنید.

نمونه semantic markup:

```html
<main>
    <article>
        <h1>عنوان مقاله</h1>
        <p>محتوای اصلی...</p>
        <img src="example.webp" alt="توضیح دقیق تصویر" width="1200" height="800" loading="lazy">
    </article>
</main>
```

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- Google Search Console.
- PageSpeed Insights و Lighthouse.
- Chrome DevTools.
- یکی از SEO pluginهای مورد تأیید پروژه؛ همزمان چند موتور metadata فعال نکنید.
- ابزار validation structured data.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. indexability و robots را بررسی کنید.
2. sitemap و canonical را بررسی کنید.
3. title/meta و heading را crawl کنید.
4. URLها و redirectها را بررسی کنید.
5. image dimensions/alt/lazy loading را کنترل کنید.
6. mobile layout و viewport را تست کنید.
7. Core Web Vitals را اندازه‌گیری کنید.
8. structured data را validate کنید.
9. 404، pagination و archiveها را بررسی کنید.
10. تداخل theme و SEO plugin را تست کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- تولید دو title/canonical.
- noindex ناخواسته.
- H1 متعدد بدون منطق.
- alt پر از keyword.
- lazy loading عنصر LCP.
- تصاویر بدون width/height.
- schema جعلی یا ناسازگار با محتوای صفحه.

## 7. مثال‌های کد یا نمونه واقعی

برای داده ساختاریافته، JSON-LD را فقط با داده واقعی تولید کنید:

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

structured data را از input خام بدون escaping/encoding صحیح تولید نکنید. scriptهای third-party را محدود کنید. font و image را بهینه کنید و caching/CDN را با cache invalidation صحیح تنظیم کنید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Google Search Essentials: https://developers.google.com/search/docs/essentials
- Core Web Vitals: https://developers.google.com/search/docs/appearance/core-web-vitals
- Schema.org: https://schema.org/
- WordPress: https://developer.wordpress.org/themes/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] indexability صحیح است.
- [ ] title/meta/canonical یکتا و بدون conflict است.
- [ ] headingها semantic هستند.
- [ ] images دارای alt و ابعاد مناسب‌اند.
- [ ] mobile تست شده است.
- [ ] CWV اندازه‌گیری و موارد بحرانی اصلاح شده‌اند.
- [ ] structured data معتبر و واقعی است.
- [ ] با SEO plugin تداخل وجود ندارد.

## به‌روزرسانی بعدی

