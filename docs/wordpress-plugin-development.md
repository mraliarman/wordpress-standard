# استاندارد توسعه Plugin در WordPress

این سند استاندارد مهندسی توسعه افزونه‌های WordPress است و architecture، bootstrap، hooks، activation/deactivation/uninstall، settings، AJAX/REST، security، database، migrations، i18n، compatibility، performance و testing را پوشش می‌دهد. Plugin باید functionality را مستقل از presentation نگه دارد و از APIهای رسمی WordPress استفاده کند. citeturn0search3turn0search7

## 2. اهداف و دامنه (Scope)

این استاندارد برای pluginهای کوچک تا enterprise-style کاربرد دارد. WooCommerce-specific architecture، payment gateway implementation و third-party API contract در صورت نیاز باید سند تخصصی جداگانه داشته باشند.

## 3. استانداردها و اصول اصلی (Best Practices)

### Architecture

- bootstrap plugin کوچک باشد.
- namespace یا prefix یکتا داشته باشید.
- classها از `src/` و در صورت استفاده از Composer با PSR-4 load شوند.
- hook registration متمرکز و قابل ردیابی باشد.
- business logic از WordPress adapterها جدا شود تا testability افزایش یابد.
- global state فقط در صورت ضرورت استفاده شود.

ساختار پیشنهادی:

```text
plugin/
├── plugin.php
├── uninstall.php
├── composer.json
├── readme.txt
├── src/
│   ├── Admin/
│   ├── Domain/
│   ├── Infrastructure/
│   └── Plugin.php
├── assets/
├── languages/
└── tests/
```

### Hooks

Action برای اجرای رفتار و Filter برای تغییر value استفاده شود. hook name، priority و accepted args باید مستند و حداقلی باشند. از hookهای بسیار عمومی بدون namespace/prefix مناسب اجتناب کنید.

### Lifecycle

- activation: نصب اولیه، option پیش‌فرض، schema یا rewrite registration.
- deactivation: توقف موقت رفتار؛ حذف دائمی داده نباید به‌صورت پیش‌فرض اینجا انجام شود.
- uninstall: حذف داده فقط طبق policy و با رضایت/تنظیمات مشخص.
- migration: با version مستقل و idempotent طراحی شود.

### Security

nonce فقط intent/CSRF را بررسی می‌کند و جای capability check نیست. عملیات حساس باید authorization مستقل داشته باشد. input validation، sanitization و output escaping باید در مرز مناسب انجام شوند.

### Database

- از `$wpdb->prepare()` برای query دارای ورودی استفاده کنید.
- برای custom table، schema version و migration داشته باشید.
- index بر اساس query واقعی طراحی شود.
- `dbDelta()` در صورت نیاز به schema creation/upgrade استفاده و نتیجه migration بررسی شود.
- داده‌های کوچک configuration در Options API؛ داده‌های رابطه‌ای و بزرگ در ساختار مناسب.

### Internationalization

text domain ثابت، ترجمه‌پذیر و همسو با slug باشد. رشته‌های قابل ترجمه را hard-code بدون gettext رها نکنید. WordPress برای internationalization و text domain قواعد مشخصی دارد. citeturn0search3

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

| ابزار | کاربرد |
|---|---|
| WordPress | نسخه stable پشتیبانی‌شده |
| PHP | نسخه اعلام‌شده plugin |
| Composer 2.x | dependency/autoload |
| WP-CLI | install، migration و maintenance |
| PHPCS/WPCS | coding standard |
| PHPStan | static analysis |
| PHPUnit | unit/integration test |
| Browser DevTools | AJAX/REST/frontend debugging |

حداقل و حداکثر compatibility باید در release documentation مشخص شود و در CI ماتریس موردنیاز تست شود.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. slug، namespace و text domain را تثبیت کنید.
2. minimum WordPress/PHP را تعیین کنید.
3. architecture و bootstrap را بسازید.
4. PSR-4 و dependency management را تنظیم کنید.
5. hookها را ثبت کنید.
6. admin capabilityها و nonceها را طراحی کنید.
7. AJAX/REST permission callback و input validation را پیاده کنید.
8. database schema و migration version را تعریف کنید.
9. activation/deactivation/uninstall را تست کنید.
10. i18n را پیاده و extraction را بررسی کنید.
11. unit/integration tests را اجرا کنید.
12. PHPCS/PHPStan را اجرا کنید.
13. clean install و upgrade از نسخه قبلی را تست کنید.
14. uninstall behavior را طبق policy بررسی کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- nonce بدون authorization.
- اعتماد به `$_POST`، `$_GET` یا REST input بدون validation.
- SQL concatenation.
- حذف داده در deactivation.
- class/function بدون namespace یا prefix.
- enqueue asset در تمام صفحات admin/frontend.
- اجرای migration در هر request.
- API endpoint بدون permission callback مناسب.
- text domain ناسازگار.
- عدم تست update از نسخه قبلی.

## 7. مثال‌های کد یا نمونه واقعی

الگوی امن برای فرم admin:

```php
if (!current_user_can('manage_options')) {
    wp_die(esc_html__('You are not allowed to perform this action.', 'my-plugin'));
}

check_admin_referer('my-plugin-save');
$value = sanitize_text_field(wp_unslash($_POST['value'] ?? ''));
```

query با پارامتر:

```php
$sql = $wpdb->prepare(
    "SELECT id FROM {$table} WHERE email = %s LIMIT 1",
    $email
);
$id = $wpdb->get_var($sql);
```

## 8. نکات امنیتی و عملکردی

Threat model حداقل باید XSS، CSRF، SQL injection، privilege escalation، SSRF در صورت remote request و unsafe file upload را پوشش دهد. remote request باید timeout، validation و allowlist مناسب داشته باشد. cache و transients با invalidation روشن استفاده شوند. queryهای expensive در admin و frontend بی‌دلیل تکرار نشوند.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Plugin Handbook: https://developer.wordpress.org/plugins/
- Security: https://developer.wordpress.org/plugins/security/
- Nonces: https://developer.wordpress.org/plugins/security/nonces/
- Hooks: https://developer.wordpress.org/plugins/hooks/
- Internationalization: https://developer.wordpress.org/plugins/internationalization/
- Custom Tables: https://developer.wordpress.org/plugins/creating-tables-with-plugins/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] architecture و ownership هر layer مشخص است.
- [ ] namespace/prefix یکتا است.
- [ ] lifecycle کامل و تست‌شده است.
- [ ] authorization و nonce صحیح‌اند.
- [ ] input validation/sanitization و output escaping کامل است.
- [ ] SQL امن و migration versioned است.
- [ ] AJAX/REST permissionها تست شده‌اند.
- [ ] i18n و text domain صحیح است.
- [ ] compatibility مشخص و تست شده است.
- [ ] PHPCS/PHPStan/tests موفق‌اند.
- [ ] clean install و upgrade تست شده‌اند.

## به‌روزرسانی بعدی

