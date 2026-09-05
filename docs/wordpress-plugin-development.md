# توسعه افزونه WordPress

این سند استاندارد معماری و توسعه افزونه‌های وردپرس است: ساختار، hooks، lifecycle، امنیت، database، i18n و سازگاری نسخه‌ای. Hooks اساس تعامل افزونه با Core هستند و به Actions و Filters تقسیم می‌شوند. citeturn1search3

## 2. اهداف و دامنه (Scope)

پوشش: plugin architecture، activation/deactivation/uninstall، hooks، admin، database، nonce، capability، sanitize/escape و translation. توسعه اختصاصی WooCommerce خارج از دامنه است.

## 3. استانداردها و اصول اصلی (Best Practices)

- plugin باید slug و text domain ثابت داشته باشد.
- bootstrap افزونه باید کوچک باشد و کلاس‌ها از `src/` با PSR-4 autoload شوند.
- Action برای اجرای کار و Filter برای تغییر مقدار استفاده شود. citeturn1search3
- activation برای ساخت جدول/default option/rewrite و deactivation برای cleanup موقت است؛ حذف دائمی داده را uninstall انجام دهد. citeturn1search14
- قبل از عملیات حساس capability بررسی شود و nonce فقط برای اثبات intent است، نه authorization.
- ورودی validate/sanitize و خروجی escape شود.
- `$wpdb->prepare()` برای query دارای ورودی استفاده شود.
- optionهای کم‌حجم در Options API و داده‌های حجیم/رابطه‌ای در جدول مناسب ذخیره شوند.
- migration دیتابیس versioned باشد.
- رشته‌ها با gettext و text domain ثابت internationalize شوند. WordPress توصیه می‌کند text domain با slug و با حروف کوچک و dash باشد. citeturn1search4

ساختار:

```text
plugin/
├── plugin.php
├── uninstall.php
├── composer.json
├── readme.txt
├── src/
├── assets/
├── languages/
└── tests/
```

نمونه lifecycle:

```php
register_activation_hook(__FILE__, 'plugin_activate');
register_deactivation_hook(__FILE__, 'plugin_deactivate');
```

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- WordPress stable پشتیبانی‌شده.
- PHP نسخه سازگار با WordPress و dependencyها.
- Composer 2.x.
- WP-CLI برای migration/maintenance.
- PHPCS/WPCS، PHPStan و PHPUnit.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. slug، namespace و text domain تعیین کنید.
2. bootstrap و PSR-4 را بسازید.
3. hooks را در یک محل ثبت کنید.
4. capability و nonce را برای admin/AJAX/REST تعریف کنید.
5. validation/sanitization ورودی را انجام دهید.
6. خروجی را بر اساس context escape کنید.
7. database schema و version option را طراحی کنید.
8. activation/deactivation/uninstall را تست کنید.
9. translation و language files را بررسی کنید.
10. حداقل و حداکثر نسخه WordPress/PHP را اعلام و تست کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- nonce بدون capability check.
- `esc_html()` در contextی که `esc_attr()` یا URL escaping لازم است.
- SQL string concatenation.
- حذف داده در deactivation.
- text domain dynamic و غیرقابل استخراج.
- global function/class بدون namespace یا prefix.

## 7. مثال‌های کد یا نمونه واقعی

```php
if (!current_user_can('manage_options')) {
    wp_die(esc_html__('You are not allowed to perform this action.', 'my-plugin'));
}

check_admin_referer('my-plugin-save');
$value = sanitize_text_field(wp_unslash($_POST['value'] ?? ''));
```

برای table سفارشی از `dbDelta()` و versioned schema استفاده کنید؛ مستندات رسمی WordPress ساخت و upgrade جدول را پوشش می‌دهد. citeturn1search12

## 8. نکات امنیتی و عملکردی

CSRF، privilege escalation، SQL injection، XSS و unsafe deserialization را در threat model بررسی کنید. queryهای غیرضروری را در هر request اجرا نکنید؛ cache و indexes را بر اساس داده واقعی طراحی کنید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Plugin Handbook: https://developer.wordpress.org/plugins/
- Security: https://developer.wordpress.org/plugins/security/
- Nonces: https://developer.wordpress.org/plugins/security/nonces/
- Hooks: https://developer.wordpress.org/plugins/hooks/
- i18n: https://developer.wordpress.org/plugins/internationalization/
- Custom tables: https://developer.wordpress.org/plugins/creating-tables-with-plugins/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] lifecycle کامل و تست شده است.
- [ ] authorization و nonce صحیح‌اند.
- [ ] sanitize/validate/escape کامل است.
- [ ] SQL امن و migration versioned است.
- [ ] i18n صحیح است.
- [ ] PHP/WordPress compatibility مشخص است.
- [ ] PHPCS/PHPStan/tests موفق‌اند.

## به‌روزرسانی بعدی

