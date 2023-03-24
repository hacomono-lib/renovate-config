# @hacomono/renovate-config

hacomono 製品で利用している renovate オプションを使いやすくカスタマイズしたもの

## 使用方法

renovate.json に以下を記載します

```json
{
    "extends": [
        "github>hacomono-lib/renovate-config:base",
        "github>hacomono-lib/renovate-config:npm"
    ]
}
```

## extends で指定できる文字列と効果

### `"@hacomono:base"`

renovate の共通設定を定義しています.

hacomono では、以下のルールに則って定義しています

- npm などの主要パッケージは、 patch バージョンアップは自動的にマージし、それ以外は必ずレビュアーによる確認を行う
- github-actions などの CI/CD 向けのパッケージは、全て自動的にマージする
- マージされなかった PR は、repository ごとの担当者に自動的にアサインされる

### `":npm"`

node package modules の更新ルールを定義しています.

利用には、以下の設定が必要です

1. repository の設定を以下の通りに行う
   - auto merge を true にする
   - すべての pull request をレビュアー必須にする
2. 以下を GitHub Apps に追加
   - `renovate approve` をレビュー必要人数分
   
### '":npm-lockfile"'

package-lock.json や yarn.lock の更新ルールを定義しています

### `":github-actions"`

GitHub Actions で使用するモジュールのバージョンを更新します.

Ci/Cd が通ればどのバージョンでも自動的にマージされます

### `":pre-commit"`

`.pre-commit.config.yml` で指定する pre-commit の hooks のバージョンを更新します

Ci/Cd が通ればどのバージョンでも自動的にマージされます
