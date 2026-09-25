# Pull Request Checklist

این checklist برای جلوگیری از ناقص ماندن PR و استانداردسازی review استفاده می‌شود.

## قبل از ایجاد PR

- [ ] هدف و scope تغییر مشخص است.
- [ ] تغییر فقط فایل‌های لازم را شامل می‌شود.
- [ ] تغییرات unrelated حذف شده‌اند.
- [ ] روش تست مشخص و اجرا شده است.
- [ ] regressionهای محتمل بررسی شده‌اند.
- [ ] تغییرات امنیتی و داده‌ای بررسی شده‌اند.
- [ ] documentation در صورت نیاز به‌روزرسانی شده است.

## متن PR

- [ ] مسئله توضیح داده شده است.
- [ ] راهکار و محدوده تغییر مشخص است.
- [ ] test evidence ثبت شده است.
- [ ] migration یا deployment impact در صورت وجود ذکر شده است.
- [ ] برای تغییرات UI، screenshot یا evidence مناسب اضافه شده است.

## Review

- [ ] CI موفق است.
- [ ] lint و static analysis در صورت وجود موفق است.
- [ ] automated tests موفق هستند.
- [ ] reviewer می‌تواند تغییر را بدون context خارج از PR بررسی کند.
- [ ] هیچ secret، credential یا داده حساس وارد نشده است.

## قبل از Merge

- [ ] همه review commentهای لازم پاسخ داده یا resolve شده‌اند.
- [ ] branch با base سازگار است.
- [ ] تغییر نهایی با scope اولیه منطبق است.
- [ ] merge strategy با workflow پروژه سازگار است.
