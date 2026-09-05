# نکات مهم Git

این سند workflow استاندارد Git برای توسعه تیمی است: branch، commit، pull request، conflict، `.gitignore` و tag/versioning. Conventional Commits قالب `<type>[scope]: description` را تعریف می‌کند و `feat`/`fix` و BREAKING CHANGE را به SemVer مرتبط می‌کند. citeturn0search2

## 2. اهداف و دامنه (Scope)

پوشش: repository workflow، naming، commits، PR، conflict، ignore و release tags. CI/CD پیشرفته خارج از دامنه است.

## 3. استانداردها و اصول اصلی (Best Practices)

Branchهای پیشنهادی: `main` برای کد release، `feature/...` برای feature، `fix/...` برای bug، `hotfix/...` برای production emergency، `docs/...` برای documentation.

Commit نمونه:

```text
feat(admin): add customer search
fix(booking): prevent duplicate appointment
refactor(core): simplify asset loader
docs: update installation guide
chore: update dependencies
```

- commit کوچک و atomic باشد.
- message با imperative و کوتاه باشد.
- breaking change را واضح ثبت کنید.
- قبل از PR branch را با main هماهنگ کنید.
- PR باید description، test evidence و risk داشته باشد.
- force push روی main ممنوع.

نمونه `.gitignore` PHP/WordPress:

```gitignore
/vendor/
/node_modules/
.env
.env.*
!.env.example
*.log
.DS_Store
Thumbs.db
.idea/
.vscode/
*.sql
wp-content/uploads/
```

اگر فایل موردی عمداً باید commit شود، rule دقیق‌تر اضافه کنید؛ `.gitignore` جای secret management نیست.

## 4. ابزارها، کتابخانه‌ها و نسخه‌های پیشنهادی

- Git نسخه stable جدید سازگار با محیط تیم.
- GitHub برای remote و PR.
- Conventional Commits 1.0.0. citeturn0search2
- pre-commit hooks در صورت نیاز.

## 5. مراحل گام‌به‌گام / چک‌لیست عملی

1. `git status`.
2. `git switch -c feature/name`.
3. تغییر کوچک.
4. `git diff` و `git diff --check`.
5. تست.
6. `git add` فقط فایل‌های لازم.
7. commit استاندارد.
8. `git fetch origin`.
9. rebase/merge طبق policy تیم.
10. push و PR.
11. review و CI.
12. merge.
13. tag release.

Conflict:

```bash
git fetch origin
git rebase origin/main
# conflict را اصلاح کنید
git add <file>
git rebase --continue
```

اگر rebase اشتباه شد: `git rebase --abort`.

## 6. اشتباهات رایج و نحوه پیشگیری از آن‌ها (Common Pitfalls)

- commit کردن `.env` یا backup.
- commitهای عظیم و نامفهوم.
- merge مستقیم feature بدون review.
- force push branch مشترک.
- حل conflict با حذف کورکورانه تغییر طرف مقابل.
- tag بدون هماهنگی version محصول.

## 7. مثال‌های کد یا نمونه واقعی

```bash
git tag -a v1.4.0 -m "Release v1.4.0"
git push origin v1.4.0
```

## 8. نکات امنیتی و عملکردی

secretها را با secret manager نگه دارید. history Git را امن فرض نکنید؛ secret لو رفته باید revoke/rotate شود. repositoryهای بزرگ را با binaryهای بی‌دلیل سنگین نکنید.

## 9. منابع و مراجع معتبر برای مطالعه بیشتر

- Conventional Commits: https://www.conventionalcommits.org/en/v1.0.0/
- Git Book: https://git-scm.com/book/en/v2
- GitHub Flow: https://docs.github.com/en/get-started/using-github/github-flow

## 10. چک‌لیست نهایی تأیید (Definition of Done)

- [ ] branch نام مناسب دارد.
- [ ] commitها atomic و استانداردند.
- [ ] secret/backup در repository نیست.
- [ ] test و CI موفق است.
- [ ] PR review شده است.
- [ ] conflictها آگاهانه حل شده‌اند.
- [ ] tag و version هماهنگ‌اند.

## به‌روزرسانی بعدی

