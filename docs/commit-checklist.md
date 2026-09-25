# Commit Checklist

هدف این checklist حفظ commitهای کوچک، قابل فهم و قابل بازگشت است.

## قبل از Commit

- [ ] تغییرات فقط مربوط به یک هدف مشخص هستند.
- [ ] فایل‌های موقت، build artifact و secretها بررسی شده‌اند.
- [ ] diff به‌صورت کامل بررسی شده است.
- [ ] test یا validation مرتبط اجرا شده است.

## پیام Commit

ساختار پیشنهادی:

```text
type(scope): short description
```

typeهای رایج:

- `feat`
- `fix`
- `docs`
- `refactor`
- `test`
- `chore`

نمونه:

```text
fix(admin): prevent duplicate customer records
docs(git): add commit checklist
```

## Atomic Commit

یک commit باید تا حد امکان یک تغییر منطقی را نشان دهد.

از ترکیب این موارد در یک commit خودداری کنید:

- feature و unrelated refactor
- bug fix و formatting گسترده
- dependency update و تغییر functionality بدون ارتباط

## بعد از Commit

- [ ] commit قابل توضیح و review است.
- [ ] در صورت نیاز، تست‌های مرتبط در CI قابل اجرا هستند.
- [ ] history پروژه با commitهای غیرضروری آلوده نشده است.
