# Publish GetVerifyCode Guides on GitBook

Content is ready in this repo. GitBook account creation needs a normal browser (Cursor’s browser hits OAuth errors).

## 1. Create the GitBook org / site

1. Open https://app.gitbook.com/join in Chrome.
2. Prefer **Continue with GitHub** and authorize the **GetVerifyCode** org account, or use `hello@getverifycode.com` / `support@getverifycode.com` if you have that mailbox.
3. Name the organization **GetVerifyCode**.
4. Create a docs site / space titled **GetVerifyCode Guides**.

## 2. Import this repository (Git Sync)

1. In the space, open **Git Sync**.
2. Connect GitHub → repository **GetVerifyCode/guides** → branch **main**.
3. Initial direction: **Repository → GitBook**.
4. Start sync. Confirm these pages appear:
   - GetVerifyCode Guides (`README.md`)
   - How SMS Verification Works (`how-sms-verification-works.md`)

## 3. Publish

1. Publish the site as public.
2. Prefer the hostname `getverifycode.gitbook.io` if GitBook still offers that style URL, or use the site URL GitBook assigns.
3. After publish, View Source on a page that links to https://getverifycode.com/ and confirm there is **no** `rel="nofollow"` on the brand link.

## 4. Optional CLI later

```bash
npm install -g @gitbook/cli
gitbook login
gitbook organizations list
```

Then create / update pages via change requests if you prefer docs-as-code edits from the terminal.
