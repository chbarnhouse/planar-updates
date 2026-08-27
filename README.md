# planar-updates

One file, `latest.json`, naming the newest published version of Planar.

## Why this repo is public when the builds are not

Planar's builds live in a **private, invite-only** repo. An in-app update check
needs *something* fetchable without a credential, and the alternative — shipping
a GitHub token inside every copy of the app so it can read the private repo —
puts an extractable secret in the hands of everyone who downloads it.

So the split: the **version number** is public, the **build** is not. Planar
reads this file, compares it to itself, and tells you when a newer version
exists. Downloading it still requires the invitation you already have. Nothing
here is a binary, source, or anything else the app's existence didn't already
imply.

The app never downloads or replaces itself, and the check is **off by default** —
Settings → General → Updates, or on demand from the menu bar.

## Format

```json
{
  "version": "0.2.0",
  "notes": "Optional one-line summary, shown in the notice."
}
```

`version` is compared numerically, component by component, so `0.10.0` correctly
beats `0.9.0`.

## Publishing

`scripts/release.sh` in the app repo prints the exact command after a build.
Skipping this step is silent: friends still get GitHub's release email, but the
app keeps reporting the previous version as current.
