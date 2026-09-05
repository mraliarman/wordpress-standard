# استاندارد Testing و Quality Assurance

این سند چارچوب کنترل کیفیت برای پروژه‌های PHP و WordPress را تعریف می‌کند و test strategy، unit/integration/manual testing، regression، compatibility، accessibility، performance، release evidence و quality gates را پوشش می‌دهد. هدف، انتقال QA از مرحله «آخر کار» به یک فرآیند پیوسته از requirement تا release است.

## 2. اهداف و دامنه (Scope)

دامنه شامل تست کد PHP، WordPress hooks، database، REST/AJAX، frontend، responsive، accessibility، browser compatibility و regression است. تست penetration تخصصی در صورت نیاز باید توسط فرآیند امنیتی جداگانه انجام شود.

## 3. استانداردها و اصول اصلی (Best Practices)

- هر requirement مهم باید acceptance criteria قابل تست داشته باشد.
- unit test برای logic مستقل؛ integration test برای تعامل componentها؛ manual/E2E برای سناریوهای واقعی.
- regression test برای bugهای مهم الزامی است.
- تست happy path به‌تنهایی کافی نیست؛ edge case و permission را نیز بررسی کنید.
- نقش‌های کاربری مختلف WordPress را تست کنید.
- compatibility matrix نسخه‌های پشتیبانی‌شده را مشخص کند.
- test data باید synthetic یا کنترل‌شده باشد.
- test باید deterministic و قابل تکرار باشد.
- flaky test باید owner و برنامه اصلاح داشته باشد.

### Test Pyramid

```text
        E2E / Manual
       Integration
      Unit / Static
```

هرچه test گران‌تر و کندتر است، باید برای سناریوهای ارزشمندتر استفاده شود.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- PHPUnit.
- PHPStan.
- PHPCS/WPCS.
- WP-CLI.
- Playwright یا ابزار E2E مورد تأیید پروژه در صورت نیاز.
- Browser DevTools.
- Lighthouse.
- CI platform مورد استفاده repository.

نسخه ابزارها باید با stack پروژه تثبیت و در CI یکسان‌سازی شوند.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. acceptance criteria را استخراج کنید.
2. risk-based test plan بنویسید.
3. unit testهای logic اصلی را ایجاد کنید.
4. integration pointها را تست کنید.
5. permission و security boundaryها را تست کنید.
6. database migration/update را تست کنید.
7. frontend responsive/RTL/accessibility را بررسی کنید.
8. browser matrix را اجرا کنید.
9. regression suite را اجرا کنید.
10. performance smoke test انجام دهید.
11. failure evidence را ثبت کنید.
12. defect را با reproduction دقیق ثبت کنید.
13. fix را با regression test تأیید کنید.
14. release evidence را نگه دارید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- تست فقط happy path.
- تست فقط با administrator.
- تست روی یک browser.
- وابستگی test به داده production.
- testهای flaky بدون owner.
- پوشش عددی بالا با assertionهای بی‌ارزش.
- حذف regression test پس از fix.
- اجرای manual test بدون ثبت evidence.

## 7. مثال‌های کد یا نمونه واقعی

نمونه PHPUnit:

```php
public function testActiveUserIsReturned(): void
{
    $user = $this->service->findByEmail('user@example.com');

    $this->assertNotNull($user);
    $this->assertSame('user@example.com', $user->email);
}
```

نمونه acceptance criteria:

```text
Given a user with manage_options
When the form is submitted with a valid nonce
Then the record is saved
And the success notice is displayed
And unauthorized users receive a permission error
```

## 8. نکات امنیتی و عملکردی

test environment نباید secret واقعی یا داده مشتری داشته باشد. تست permission، nonce، validation و escaping بخشی از QA است. performance test باید baseline داشته باشد تا regression قابل اندازه‌گیری شود.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- PHPUnit: https://phpunit.de/documentation.html
- WordPress Developer: https://developer.wordpress.org/
- WordPress Coding Standards: https://developer.wordpress.org/coding-standards/
- Playwright: https://playwright.dev/docs/intro
- Lighthouse: https://developer.chrome.com/docs/lighthouse/

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] acceptance criteria تست شده‌اند.
- [ ] unit/integration testهای لازم موفق‌اند.
- [ ] regression test برای bugهای مهم وجود دارد.
- [ ] permission/security cases تست شده‌اند.
- [ ] migration/update تست شده است.
- [ ] RTL/mobile/browser تست شده‌اند.
- [ ] accessibility بررسی شده است.
- [ ] performance smoke test انجام شده است.
- [ ] test evidence ثبت شده است.
- [ ] flaky test unresolved وجود ندارد یا owner دارد.

## به‌روزرسانی بعدی

