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
        └── how-sms-verification-works.md
```

## Verify after publish

View Source on a page that links to https://getverifycode.com/ and confirm there is no `rel="nofollow"` on the brand link.
