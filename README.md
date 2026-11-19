# dsh-plugin-index

Plugin index (format 1) for **DeepSeek Harness**: lists the bundles I publish, so they can be installed straight from DSH's **Discover** tab.

```text
https://raw.githubusercontent.com/lcf2212dev/dsh-plugin-index/main/index.json
```

## How to add it in DSH

1. Open **Plugins** in the sidebar.
2. Under **Experimental plugins**, turn on **Custom plugin indexes** — the page then has **Installed** and **Discover** tabs.
3. Open **Discover** and click **Add index source**.
4. Paste the URL above and confirm.

DSH fetches and validates the index; search, filters, and the **Install** button appear right after. Installation uses the exact version spec (Git with a pinned commit), with DSH's normal trust dialog.

## What is in the index

| Package | Version | Repository |
|---|---|---|
| `@dsh-burn-plugins/dsh-bots` (Bits) | 0.4.0 | [dsh-bits](https://github.com/lcf2212dev/dsh-bits) |
| `@dsh-burn-plugins/dsh-claude-delegate` | 0.2.1 | [dsh-claude-delegate](https://github.com/lcf2212dev/dsh-claude-delegate) |
| `@dsh-burn-plugins/dsh-figma-mcp-oauth` | 0.1.0 | [dsh-figma-mcp-oauth](https://github.com/lcf2212dev/dsh-figma-mcp-oauth) |
| `@dsh-burn-plugins/dsh-image-creator` | 0.1.0 | [dsh-image-creator](https://github.com/lcf2212dev/dsh-image-creator) |
| `@dsh-burn-plugins/dsh-image-viewer` | 0.1.0 | [dsh-image-viewer](https://github.com/lcf2212dev/dsh-image-viewer) |
| `@dsh-burn-plugins/dsh-mobile` (DSH in your pocket) | 1.1.0 | [dsh-android](https://github.com/lcf2212dev/dsh-android) |
| `@dsh-burn-plugins/dsh-remote-control` | 1.0.0 | [dsh-remote-control](https://github.com/lcf2212dev/dsh-remote-control) |

The two image bundles call the `claude_delegate` tool with the `fable` model, so they need `dsh-claude-delegate` 0.2.1 or later installed alongside them; the 0.1.0 release, still listed, rejects that model.

The two phone bundles do not include their Android apps: build the APK from the repository (`dsh-mobile`: `mobile/scripts/build-apk.sh`; `dsh-remote-control`: `app/build.sh`, then point `apkPath` at it). `dsh-remote-control` also ships the Shizuku helper APK.

## How to update an entry

The index pins the commit that was published. To ship a new version:

1. Publish the version in the plugin repository and get the full 40-character commit SHA.
2. In `index.json`, add an object to `versions` with the `version` from `package.json`, the new `commit`, and a `publishTimestamp` (Unix, in seconds).
3. Validate and commit/push. DSH re-reads the index (10-minute cache; there is a refresh button in Discover).

The validator is the same one DSH uses: `parseMarketIndex` from `@deepseek-ai/dsh-plugin-market-index`.

## Format

[Format 1](https://github.com/deepseek-ai/deepseek-harness): `format`, `title`, `description`, `metadata` (categories, labels, sort keys) and `plugins[]`; each plugin has `name`, localized texts, `icon`, `author`, `homepage`, `repository`, and `versions[]` with `version`, `publishTimestamp`, `source` (`npm` or `git` + commit), and `engines.dsh`.

## License

[MIT](LICENSE).
