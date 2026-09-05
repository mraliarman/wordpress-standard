# توسعه قالب WordPress

این سند استاندارد توسعه قالب‌های کلاسیک و block theme در وردپرس است و ساختار، template hierarchy، `functions.php`، assetها، Customizer، child theme، امنیت، Gutenberg و Full Site Editing را پوشش می‌دهد. WordPress برای قالب کلاسیک عمدتاً PHP/JS/CSS و برای block theme عمدتاً block markup و configuration استفاده می‌کند. citeturn0search15turn0search5

## 2. اهداف و دامنه (Scope)

پوشش: classic theme، block theme، template hierarchy، enqueue، theme supports، `theme.json`، child theme و editor compatibility. توسعه plugin در سند جداست.

## 3. استانداردها و اصول اصلی (Best Practices)

- functionality مستقل از presentation باید در plugin باشد، نه theme.
- `functions.php` را به bootstrap و registrationهای theme محدود کنید.
- assetها را با `wp_enqueue_style()` و `wp_enqueue_script()` روی hook مناسب ثبت کنید، نه با `<link>` و `<script>` دستی. API رسمی برای handle، dependency، version و media دارد. citeturn1search1
- template hierarchy را قبل از ایجاد فایل جدید بررسی کنید؛ WordPress اولین template منطبق را انتخاب می‌کند. citeturn0search3turn0search4
- برای classic theme حداقل `style.css` و `index.php` ضروری‌اند؛ فایل‌های `header.php`، `footer.php`، `single.php`، `archive.php` و مانند آن بر اساس نیاز ایجاد شوند.
- block theme از `/templates` و `/parts` و `theme.json` استفاده می‌کند؛ `templates/index.html` حداقل template مورد نیاز block theme است. citeturn0search6
- child theme باید برای customization پایدار استفاده شود؛ فایل child در hierarchy نسبت به parent اولویت دارد. citeturn0search10
- خروجی dynamic را escape کنید و capability/input را در admin بررسی کنید.
- `theme.json` برای settings/styles مرکزی در block theme مرجع اصلی باشد؛ user configuration می‌تواند آن را override کند. citeturn0search7

ساختار classic پیشنهادی:

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
├── assets/css/
├── assets/js/
├── languages/
└── src/
```

Enqueue نمونه:

```php
add_action('wp_enqueue_scripts', function (): void {
    wp_enqueue_style(
        'theme-main',
        get_template_directory_uri() . '/assets/css/app.css',
        [],
        '1.0.0'
    );
});
```

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- WordPress: نسخه stable پشتیبانی‌شده توسط پروژه.
- PHP: نسخه پشتیبانی‌شده WordPress و dependencyها.
- Composer 2.x در صورت استفاده از PHP libraries.
- Node.js LTS و Tailwind CLI برای build frontend در صورت نیاز.
- WP-CLI، PHPStan و PHPCS/WPCS.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. نوع قالب را مشخص کنید: classic یا block.
2. slug و text domain را ثابت کنید.
3. ساختار فایل را بسازید.
4. `theme_supports` و menus/widgets را در زمان مناسب ثبت کنید.
5. template hierarchy را تعیین کنید.
6. assetها را enqueue کنید.
7. خروجی‌ها را escape کنید.
8. Gutenberg/block editor را تست کنید.
9. responsive، RTL، keyboard و screen reader را بررسی کنید.
10. parent/child behavior و update safety را تست کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- قرار دادن business logic در theme.
- enqueue مستقیم asset.
- hard-code کردن URLها.
- override اشتباه parent با child.
- مخلوط کردن templateهای PHP و block بدون معماری مشخص.
- نادیده گرفتن `theme.json` در block theme.

## 7. مثال‌های کد یا نمونه واقعی

```php
$title = get_the_title();
echo esc_html($title);
```

در templateها از template tags رسمی استفاده و context مناسب escape کنید.

## 8. نکات امنیتی و عملکردی

از nonce/capability برای عملیات مدیریتی استفاده کنید، output escape شود، asset فقط در صفحات لازم enqueue شود و queryهای سنگین بهینه شوند. تصاویر responsive و lazy loading مناسب را فعال نگه دارید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Theme Handbook: https://developer.wordpress.org/themes/
- Template hierarchy: https://developer.wordpress.org/themes/templates/template-hierarchy/
- Block templates: https://developer.wordpress.org/themes/templates/templates/
- Child themes: https://developer.wordpress.org/themes/advanced-topics/child-themes/
- `wp_enqueue_style`: https://developer.wordpress.org/reference/functions/wp_enqueue_style/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] ساختار theme معتبر است.
- [ ] hierarchy درست کار می‌کند.
- [ ] assetها enqueue شده‌اند.
- [ ] child theme قابل استفاده است.
- [ ] Gutenberg/FSE طبق نوع theme تست شده است.
- [ ] escaping و capability checks انجام شده‌اند.
- [ ] RTL/mobile/accessibility بررسی شده است.
- [ ] business logic خارج از theme قرار گرفته است.

## به‌روزرسانی بعدی

