# Publish GetVerifyCode Guides on GitBook

Content lives in `./guides`. Site structure is declared in `gitbook-docs.yaml` at the repo root.

## Git Sync (site already created)

1. Open your GitBook site → Git Sync.
2. Repository: **GetVerifyCode/guides**, branch **main**.
3. Project directory: **`./`** (repo root, where `gitbook-docs.yaml` lives).
4. Initial direction: **GitHub → GitBook**.
5. Confirm mapping: space **Guides** → `./guides`.
6. Sync, then publish public.
7. Send the public reader URL (not `app.gitbook.com/...`).

## Structure

```text
GetVerifyCode Guides (site)
└── Guides (space, path: guides, default)
    └── content: ./guides
        ├── README.md
        ├── SUMMARY.md
        ├── how-sms-verification-works.md
        ├── when-otp-sms-does-not-arrive.md
        └── testing-sms-otp-before-launch.md
```

## Space branding (GitBook UI)

Git Sync only ships Markdown. In the GitBook space settings, set:

1. Space title: **GetVerifyCode Guides**
2. Logo: GetVerifyCode wordmark or mark (same as the live site)
3. Primary color: `#3f72af` (product accent)
4. Hide any leftover onboarding / “getting started with GitBook” pages

Without those, the public site still looks like a default GitBook template even when content is solid.

## Verify after publish

View Source on a page that links to https://getverifycode.com/ and confirm there is no `rel="nofollow"` on the brand link.
