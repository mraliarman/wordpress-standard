# استانداردهای PHP

این سند قواعد کدنویسی، معماری، Composer، PHPDoc، type system و مدیریت خطا را برای کد PHP تیم مشخص می‌کند. PSR-12 استاندارد PSR-2 را گسترش داده و جایگزین آن است و به PSR-1 وابسته است. citeturn1search5

## 2. اهداف و دامنه (Scope)

پوشش: PHP مدرن، PSR-1/12، Composer، PSR-4، SemVer، PHPDoc و Exception handling. خارج از دامنه: framework-specific styleهایی که با این سند تعارض دارند.

## 3. استانداردها و اصول اصلی (Best Practices)

- PHP فایل فقط PHP: closing tag `?>` حذف شود.
- LF، یک newline در انتهای فایل و بدون trailing whitespace رعایت شود. PSR-12 soft limit را 120 کاراکتر و توصیه عمومی را 80 کاراکتر بیان می‌کند. citeturn1search5
- namespace و classها مطابق PSR-4 باشند؛ نام کلاس PascalCase و متد/متغیر camelCase باشد.
- هر API عمومی type declaration روشن داشته باشد: parameter، return و در صورت نیاز property.
- برای مقادیر nullable از `?Type` یا union مناسب استفاده کنید.
- Exception را برای خطای واقعی پرتاب کنید و آن را فقط در لایه‌ای catch کنید که توان recovery یا تبدیل خطا دارد.
- `catch (Throwable $e)` فقط وقتی لازم است؛ خطاهای برنامه را بی‌صدا نخورید.
- Composer فقط dependency لازم را نگه دارد؛ `composer.lock` برای application/plugin build قابل تکرار commit شود.

نمونه `composer.json`:

```json
{
    "autoload": {
        "psr-4": {
            "Ts\\Project\\": "src/"
        }
    },
    "require": {
        "php": ">=8.1"
    }
}
```

بعد از تغییر autoload:

```bash
composer dump-autoload
```

PHPDoc استاندارد:

```php
/**
 * Finds a user by email address.
 *
 * @param string $email User email address.
 * @return User|null Matching user or null when not found.
 */
public function findByEmail(string $email): ?User
{
    return null;
}
```

PHPDoc نباید typeهایی را ادعا کند که signature خلاف آن را می‌گوید.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- PHP: نسخه LTS/پشتیبانی‌شده محیط پروژه؛ برای پروژه جدید حداقل نسخه را بر اساس dependencyها تعیین کنید.
- Composer 2.x.
- PHP_CodeSniffer با استاندارد PSR-12 و WordPress Coding Standards در پروژه‌های وردپرس.
- PHPStan برای static analysis.
- PHPUnit برای تست.

PSR-12 مرجع اصلی style است. citeturn1search5

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. `composer.json` را تعریف کنید.
2. PSR-4 را مشخص کنید.
3. `composer install` را با lockfile اجرا کنید.
4. `composer validate` را اجرا کنید.
5. lint: `php -l path/to/file.php`.
6. static analysis و tests را اجرا کنید.
7. coding standard را اجرا کنید.
8. Exceptionها را در boundaryهای مناسب مدیریت کنید.
9. dependencyهای غیرضروری را حذف کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- namespace ناسازگار با PSR-4.
- commit نکردن lockfile در applicationها.
- PHPDoc بدون type واقعی.
- catch کردن exception و ادامه بی‌صدا.
- استفاده از global state بدون دلیل.
- dependency با constraint بیش از حد باز.

## 7. مثال‌های کد یا نمونه واقعی

```php
namespace Ts\Project\Service;

final class UserService
{
    /**
     * Creates a user service.
     *
     * @param UserRepository $repository User repository.
     */
    public function __construct(
        private UserRepository $repository
    ) {
    }
}
```

## 8. نکات امنیتی و عملکردی

ورودی را validate کنید، secrets را در کد commit نکنید، dependency audit انجام دهید و exception message حساس را به کاربر نمایش ندهید. Autoload optimized در production می‌تواند با `composer install --no-dev --optimize-autoloader` انجام شود.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- PSR-12: https://www.php-fig.org/psr/psr-12/
- PSR-1: https://www.php-fig.org/psr/psr-1/
- PSR-4: https://www.php-fig.org/psr/psr-4/
- Composer: https://getcomposer.org/doc/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] PSR-12 رعایت شده است.
- [ ] PSR-4 صحیح است.
- [ ] public APIها type دارند.
- [ ] PHPDocهای لازم دقیق هستند.
- [ ] Composer lock و autoload معتبر است.
- [ ] lint، static analysis و test موفق‌اند.
- [ ] Exception handling قابل مشاهده و هدفمند است.

## به‌روزرسانی بعدی

