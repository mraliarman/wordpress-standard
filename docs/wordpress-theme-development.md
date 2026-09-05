# استاندارد توسعه Theme در WordPress

این سند استاندارد مهندسی توسعه قالب‌های WordPress را برای classic theme و block theme تعریف می‌کند و معماری فایل، template hierarchy، `functions.php`، enqueue، `theme.json`، Gutenberg، FSE، child theme، accessibility، security، performance و release readiness را پوشش می‌دهد. WordPress مستندات رسمی جداگانه‌ای برای block و classic theme دارد و انتخاب معماری باید از ابتدا روشن باشد. citeturn0search1turn0search12

## 2. اهداف و دامنه (Scope)

دامنه شامل ساخت و نگهداری theme، template، template part، asset، customization و editor integration است. business logic مستقل، payment، data ownership و functionality عمومی باید تا حد امکان در plugin یا service مناسب قرار گیرند.

## 3. استانداردها و اصول اصلی (Best Practices)

### معماری

- قبل از کدنویسی مشخص کنید theme کلاسیک است یا block theme.
- `functions.php` محل bootstrap و registrationهای theme است، نه محل تمام business logic.
- functionalityای که باید با تغییر theme باقی بماند در plugin قرار گیرد.
- naming، text domain و asset handle یکتا باشند.
- ساختار template بر اساس WordPress Template Hierarchy طراحی شود؛ فایل جدید فقط وقتی ایجاد شود که hierarchy آن را توجیه کند. citeturn0search1

### Classic Theme

حداقل‌های رایج برای theme کلاسیک شامل `style.css` و `index.php` است و بر اساس نیاز templateهای اختصاصی اضافه می‌شوند. WordPress همچنین برای theme directory فایل‌های دیگری مانند `comments.php` و screenshot را در الزامات بررسی مطرح می‌کند. citeturn0search11

ساختار پیشنهادی:

```text
theme/
├── style.css
├── functions.php
├── index.php
├── header.php
├── footer.php
├── single.php
├── page.php
├── archive.php
├── search.php
├── 404.php
├── template-parts/
├── assets/
│   ├── css/
│   └── js/
├── languages/
└── src/
```

### Block Theme و FSE

در block theme، templateها و template partها عمدتاً block markup هستند و `theme.json` برای settings و styles نقش محوری دارد. `templates/index.html` نقطه پایه template hierarchy در block theme است. مستندات جاری WordPress باید برای جزئیات نسخه‌ای بررسی شوند.

ساختار پیشنهادی:

```text
theme/
├── style.css
├── theme.json
├── functions.php
├── templates/
│   └── index.html
├── parts/
├── patterns/
├── styles/
└── assets/
```

### Assets

assetها باید با API رسمی enqueue شوند، dependency و version مناسب داشته باشند و فقط در context موردنیاز بارگذاری شوند.

```php
add_action('wp_enqueue_scripts', function (): void {
    wp_enqueue_style(
        'project-main',
        get_template_directory_uri() . '/assets/css/app.css',
        [],
        '1.0.0'
    );
});
```

### Child Theme

child theme برای customization پایدار parent theme مناسب است. قبل از override باید مشخص شود آیا hook، filter، template part یا style extension راه‌حل کم‌ریسک‌تری است. overrideهای زیاد child theme می‌توانند update parent را پرریسک کنند.

### امنیت و خروجی

- capability check برای عملیات privileged.
- nonce برای درخواست‌های state-changing در context مناسب.
- escape بر اساس context: HTML، attribute، URL و JS هرکدام الگوی مناسب دارند.
- input را validate/sanitize کنید؛ escaping جای validation نیست.
- URLها را hard-code نکنید.

### Accessibility

مطابق اصول WordPress، keyboard navigation، focus، semantics، labels، contrast و screen reader behavior باید بخشی از acceptance criteria باشد. WordPress استانداردهای accessibility خود را در سطح WCAG AA دنبال می‌کند. citeturn0search0

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- WordPress stable پشتیبانی‌شده توسط محصول.
- PHP نسخه مورد تأیید پروژه.
- Composer 2.x در صورت dependency.
- Node.js LTS و Tailwind CSS v4 در پروژه‌های دارای Tailwind.
- WP-CLI.
- PHPCS + WordPress Coding Standards.
- PHPStan و PHPUnit در صورت پوشش مناسب پروژه.
- Browser DevTools، Lighthouse و ابزارهای accessibility.

نسخه دقیق هر dependency باید در پروژه تثبیت شود؛ «آخرین نسخه» یک requirement قابل تست نیست.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. هدف theme و نوع معماری را مشخص کنید.
2. minimum WordPress/PHP را تعیین کنید.
3. slug، text domain و namespace/prefix را تعیین کنید.
4. structure و template hierarchy را طراحی کنید.
5. `theme.json` را در block theme طراحی کنید.
6. theme supports و editor features را ثبت کنید.
7. assetها را enqueue کنید.
8. templateها و parts را بسازید.
9. dynamic output را context-aware escape کنید.
10. RTL، responsive و accessibility را تست کنید.
11. customizer/editor behavior را در صورت کاربرد تست کنید.
12. parent/child update safety را بررسی کنید.
13. PHPCS، static analysis و test را اجرا کنید.
14. روی WordPress تمیز و داده واقعی staging تست کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- قرار دادن business logic دائمی در theme.
- override زیاد parent theme.
- نادیده گرفتن hierarchy و ساخت template تکراری.
- enqueue مستقیم `<script>` یا `<link>`.
- escaping اشتباه یا دیرهنگام.
- hard-code URL و asset path.
- نادیده گرفتن RTL و keyboard.
- تولید CSS/JS برای تمام صفحات بدون نیاز.
- استفاده همزمان و متناقض از روش‌های classic و block بدون architecture روشن.

## 7. مثال‌های کد یا نمونه واقعی

Escape عنوان:

```php
<h1><?php echo esc_html(get_the_title()); ?></h1>
```

بارگذاری asset فقط در context مناسب باید با شرط‌های دقیق و hook صحیح انجام شود. در صورت امکان dependencyها را اعلام کنید تا WordPress ترتیب بارگذاری را مدیریت کند.

## 8. نکات امنیتی و عملکردی

Theme نباید debug output، secret یا داده خصوصی داشته باشد. queryهای template loop را کنترل کنید و N+1 query ایجاد نکنید. image dimensions، responsive image و loading strategy مناسب باشند. third-party assetها را حداقل کنید. در production debug display خاموش باشد.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Theme Handbook: https://developer.wordpress.org/themes/
- Theme Structure: https://developer.wordpress.org/themes/core-concepts/theme-structure/
- Template Hierarchy: https://developer.wordpress.org/themes/templates/template-hierarchy/
- `theme.json`: https://developer.wordpress.org/themes/global-settings-and-styles/
- Child Themes: https://developer.wordpress.org/themes/advanced-topics/child-themes/
- WordPress Coding Standards: https://developer.wordpress.org/coding-standards/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] معماری classic یا block مشخص است.
- [ ] minimum WordPress/PHP مشخص است.
- [ ] hierarchy صحیح و بدون template duplication است.
- [ ] assetها enqueue شده‌اند.
- [ ] `theme.json` در block theme صحیح است.
- [ ] child theme strategy مشخص است.
- [ ] خروجی‌ها context-aware escape شده‌اند.
- [ ] capability/nonce در عملیات لازم وجود دارد.
- [ ] RTL، mobile و accessibility تست شده‌اند.
- [ ] performance و asset loading بررسی شده است.
- [ ] lint/static analysis/test موفق است.
- [ ] theme روی clean install و staging تست شده است.

## به‌روزرسانی بعدی

