# استانداردهای مهندسی PHP

این سند استاندارد فنی تیم برای توسعه PHP مدرن است و PSR-1، PSR-12، PSR-4، Composer، SemVer، PHPDoc، type declarations، exception handling، dependency management، static analysis و quality gates را تعریف می‌کند. هدف، تولید کدی است که برای توسعه‌دهنده بعدی قابل فهم، برای CI قابل بررسی و برای production قابل نگهداری باشد.

## 2. اهداف و دامنه (Scope)

این استاندارد برای کتابخانه‌ها، WordPress theme/plugin و سرویس‌های PHP کاربرد دارد. قوانین اختصاصی WordPress در اسناد WordPress تکمیل می‌شوند. در تعارض، rule اختصاصی framework باید صریح و مستند باشد.

## 3. استانداردها و اصول اصلی (Best Practices)

### PSR و style

- PSR-1 برای basic coding standard و PSR-12 برای extended coding style مبنا قرار گیرد.
- هر فایل PHP با `<?php` شروع شود و closing tag غیرضروری `?>` نداشته باشد.
- فایل UTF-8 و newline انتهایی داشته باشد.
- namespace، class، interface، trait و enum نام‌گذاری پایدار و معنادار داشته باشند.
- از type declaration برای parameter، return type و property تا حد امکان استفاده شود.
- API عمومی بدون دلیل `mixed` یا type مبهم نداشته باشد.
- `declare(strict_types=1);` در پروژه‌هایی که policy پروژه آن را تأیید کرده است استفاده شود؛ اعمال سراسری آن باید با compatibility پروژه بررسی شود.

### PSR-4 و Composer

namespace باید با مسیر فایل مطابقت داشته باشد. نمونه:

```json
{
    "autoload": {
        "psr-4": {
            "Ts\\Project\\": "src/"
        }
    }
}
```

پس از تغییر autoload:

```bash
composer dump-autoload
```

در production:

```bash
composer install --no-dev --optimize-autoloader
```

### Dependency و SemVer

- dependency فقط در صورت نیاز واقعی اضافه شود.
- `composer.lock` در application و محصولاتی که build قابل تکرار دارند commit شود.
- constraintها نه بیش از حد بسته و نه بی‌دلیل باز باشند.
- upgrade dependency باید changelog، compatibility، security advisory و regression risk داشته باشد.
- SemVer به‌عنوان مدل versioning استفاده شود؛ breaking change، feature و bug fix باید قابل تشخیص باشند.

### PHPDoc

PHPDoc باید complement signature باشد، نه جایگزین آن. برای public API، پیچیدگی‌های type، generic-like annotations یا رفتار غیر بدیهی مستند شود. type خلاف signature ممنوع است.

### Exception handling

- Exception برای failure واقعی استفاده شود.
- catch فقط در لایه‌ای انجام شود که recovery، translation، logging یا cleanup معنا دارد.
- exception را بدون action دوباره throw یا swallow نکنید.
- پیام exception شامل secret، password، token یا داده شخصی نباشد.
- برای domain errorهای قابل انتظار، نوع exception مناسب تعریف شود.

### Naming

| عنصر | الگو |
|---|---|
| Class | `PascalCase` |
| Method | `camelCase` |
| Variable | `camelCase` |
| Constant | مطابق convention پروژه، ترجیحاً `UPPER_SNAKE_CASE` |
| Namespace | `Vendor\Package\...` |
| Interface | نام معنادار؛ suffix `Interface` فقط اگر convention پروژه آن را می‌طلبد |

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

| ابزار | کاربرد |
|---|---|
| PHP | نسخه پشتیبانی‌شده پروژه و dependencyها |
| Composer 2.x | dependency و autoload |
| PHP_CodeSniffer | coding standards |
| WordPress Coding Standards | برای WordPress |
| PHPStan | static analysis |
| PHPUnit | unit/integration tests |
| PHP CS Fixer | فقط در صورت policy پروژه |

نسخه دقیق باید در `composer.json`، lockfile یا مستندات release ثبت شود و از عبارت مبهم `latest` استفاده نشود.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. minimum PHP version را مشخص کنید.
2. namespace و PSR-4 را طراحی کنید.
3. `composer.json` را ایجاد و dependencyها را حداقلی نگه دارید.
4. `composer validate` را اجرا کنید.
5. autoload را تولید و تست کنید.
6. public APIها را type کنید.
7. PHPDocهای لازم را اضافه کنید.
8. PHPCS و PHPStan را اجرا کنید.
9. PHPUnit را اجرا کنید.
10. exception pathها را تست کنید.
11. dependency audit را انجام دهید.
12. production install را با `--no-dev` آزمایش کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- namespace و مسیر PSR-4 ناسازگار.
- commit نکردن lockfile در پروژه قابل build تکرار.
- `mixed` و type ضعیف در تمام API.
- PHPDoc خلاف implementation.
- catch کردن exception و نادیده گرفتن آن.
- dependency فقط برای چند خط utility.
- upgrade dependency بدون regression test.
- قرار دادن configuration و secret در source code.

## 7. مثال‌های کد یا نمونه واقعی

```php
namespace Ts\Project\Service;

final class UserService
{
    public function __construct(
        private UserRepository $repository
    ) {
    }

    public function findByEmail(string $email): ?User
    {
        return $this->repository->findByEmail($email);
    }
}
```

PHPDoc در جایی اضافه شود که اطلاعاتی فراتر از signature منتقل می‌کند:

```php
/**
 * @return list<User>
 */
public function findActiveUsers(): array
{
    return [];
}
```

## 8. نکات امنیتی و عملکردی

dependencyها باید از نظر vulnerability بررسی شوند. secretها خارج از repository نگهداری شوند. error detail به user نهایی نمایش داده نشود. در production autoload optimized استفاده شود. عملیات I/O، query و network در loopهای بزرگ کنترل شوند.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- PSR-1: https://www.php-fig.org/psr/psr-1/
- PSR-12: https://www.php-fig.org/psr/psr-12/
- PSR-4: https://www.php-fig.org/psr/psr-4/
- Composer: https://getcomposer.org/doc/
- PHP Manual: https://www.php.net/docs.php

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] minimum PHP version مشخص است.
- [ ] PSR-1/PSR-12 رعایت شده است.
- [ ] PSR-4 و autoload معتبر است.
- [ ] public API type-safe است.
- [ ] PHPDoc دقیق و غیرمتناقض است.
- [ ] dependencyها ضروری و versioned هستند.
- [ ] lint، static analysis و test موفق‌اند.
- [ ] exception handling هدفمند است.
- [ ] secret و داده حساس در کد نیست.
- [ ] production install قابل تکرار است.

## به‌روزرسانی بعدی

