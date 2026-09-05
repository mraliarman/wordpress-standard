# استاندارد Git، Branching و Release Workflow

این سند workflow استاندارد Git برای تیم توسعه است و branch strategy، Conventional Commits، pull request، code review، conflict resolution، `.gitignore`، tagging، release branch و rollback را تعریف می‌کند. هدف این است که history پروژه قابل فهم، تغییرات قابل ردیابی و releaseها قابل بازگشت باشند.

## 2. اهداف و دامنه (Scope)

دامنه شامل Git repository، GitHub، branch، commit، PR، review، tag و release artifact است. CI/CD اختصاصی هر زیرساخت در سند deployment جداگانه قابل توسعه است.

## 3. استانداردها و اصول اصلی (Best Practices)

### Branch

```text
main
feature/<short-name>
fix/<short-name>
hotfix/<short-name>
refactor/<short-name>
docs/<short-name>
```

`main` باید همیشه وضعیت قابل release داشته باشد. branchهای feature کوتاه‌عمر و محدود به یک هدف مشخص باشند.

### Commit

Conventional Commits الگوی پیشنهادی است:

```text
feat(admin): add customer search
fix(booking): prevent duplicate appointment
docs: update installation guide
refactor(core): simplify asset loader
chore: update dependencies
```

commit باید atomic باشد و message نتیجه تغییر را روشن کند. breaking change باید صریح ثبت شود.

### Pull Request

PR باید شامل problem، solution، scope، test evidence، risk و در صورت نیاز screenshot باشد. PR بزرگ باید به taskهای کوچک‌تر تقسیم شود.

### Conflict

اول context تغییر مقابل را بفهمید، سپس conflict را حل و تست کنید؛ صرفاً «ours/theirs» را بدون بررسی انتخاب نکنید.

```bash
git fetch origin
git rebase origin/main
git add <file>
git rebase --continue
```

در صورت نیاز:

```bash
git rebase --abort
```

### `.gitignore`

```gitignore
/vendor/
/node_modules/
.env
.env.*
!.env.example
*.log
*.sql
wp-content/uploads/
.DS_Store
Thumbs.db
.idea/
```

`.gitignore` جای secret management نیست؛ secret لو رفته باید revoke/rotate شود.

### Tags

version محصول و Git tag باید همسو باشند:

```bash
git tag -a v1.4.0 -m "Release v1.4.0"
git push origin v1.4.0
```

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- Git نسخه stable سازگار با تیم.
- GitHub برای repository و review.
- Conventional Commits 1.0.0.
- pre-commit hooks در صورت نیاز.
- CI برای lint/test/security checks.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. issue و acceptance criteria را بخوانید.
2. branch مناسب بسازید.
3. تغییرات کوچک و atomic انجام دهید.
4. `git diff --check` اجرا کنید.
5. lint و test را اجرا کنید.
6. commitهای معنادار بسازید.
7. branch را با `main` هماهنگ کنید.
8. PR باز کنید.
9. review و CI را کامل کنید.
10. conflictها را آگاهانه حل کنید.
11. merge طبق policy انجام دهید.
12. release tag ایجاد کنید.
13. artifact و changelog را ثبت کنید.
14. post-release را monitor کنید.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- commit `.env` یا credential.
- commitهای عظیم.
- branch بسیار طولانی.
- force push روی branch مشترک.
- merge بدون CI/review.
- حل conflict با حذف کورکورانه تغییرات.
- tag اشتباه یا version mismatch.
- commit کردن build artifact بدون policy مشخص.

## 7. مثال‌های کد یا نمونه واقعی

```bash
git switch -c fix/customer-search
git diff --check
git add src/ tests/
git commit -m "fix(customer): handle missing phone number"
git fetch origin
git rebase origin/main
git push -u origin fix/customer-search
```

## 8. نکات امنیتی و عملکردی

history Git را امن فرض نکنید. secret حذف‌شده ممکن است در history باقی بماند. secret باید revoke/rotate شود و در صورت نیاز history پاک‌سازی شود. binaryهای حجیم و dependencyهای generated غیرضروری repository را سنگین نکنند.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Git Book: https://git-scm.com/book/en/v2
- Git Documentation: https://git-scm.com/docs
- Conventional Commits: https://www.conventionalcommits.org/en/v1.0.0/
- GitHub Flow: https://docs.github.com/en/get-started/using-github/github-flow

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] branch هدفمند و کوتاه‌عمر است.
- [ ] commitها atomic و استانداردند.
- [ ] secret/backup در repository نیست.
- [ ] `git diff --check` موفق است.
- [ ] lint/test/CI موفق است.
- [ ] PR review شده است.
- [ ] conflictها آگاهانه حل شده‌اند.
- [ ] tag و version هماهنگ‌اند.
- [ ] release artifact قابل ردیابی است.

## به‌روزرسانی بعدی

