---
description: Agent実行用Issueを対話的に作成
---

# Create Issue Command

Agent実行用のIssueをテンプレートベースで対話的に作成します。

## 使用方法

```bash
/create-issue
```

このコマンドを実行すると、対話的にIssue作成のための情報を収集します。

## 対話フロー

### 1. Issue タイトル

```
Issue タイトルを入力してください:
例) ユーザー認証機能の実装
```

### 2. Issue タイプ選択

```
Issue タイプを選択してください:
1. 🆕 feature (新機能)
2. 🐛 bug (バグ修正)
3. ♻️  refactor (リファクタリング)
4. 📝 docs (ドキュメント)
5. ⚡ performance (パフォーマンス改善)
6. 🔒 security (セキュリティ)
7. 🧪 test (テスト追加)

選択 (1-7):
```

### 3. 要件入力

```
要件を入力してください (完了したら空行):
- ログイン画面の実装
- JWT認証の実装
- ユーザーモデルの作成
- ユニットテスト作成
<Enter>
```

### 4. 技術スタック (オプション)

```
使用する技術スタックを入力してください (任意):
例) React, TypeScript, Firebase Auth
```

### 5. 制約事項 (オプション)

```
制約事項があれば入力してください (任意):
例) パスワードリセット機能は別Issueで実装
```

### 6. Agent実行設定

```
Agent自動実行を有効にしますか? (y/n):
```

- `y`: 🤖agent-execute ラベルを自動付与（作成後すぐにAgentが実行開始）
- `n`: 手動でラベルを追加するまでAgent実行しない

### 7. 優先度設定

```
優先度を選択してください:
1. 🔴 High (高)
2. 🟡 Medium (中)
3. 🟢 Low (低)

選択 (1-3):
```

### 8. 担当者指定 (オプション)

```
担当者を指定しますか? (GitHubユーザー名、空でスキップ):
```

## 生成されるIssue

### Issue Body テンプレート

```markdown
# [タイプ] タイトル

## 📋 要件

- [ ] 要件1
- [ ] 要件2
- [ ] 要件3

## 🛠️ 技術スタック

- React
- TypeScript
- Firebase Auth

## ⚠️ 制約事項

- パスワードリセット機能は別Issueで実装

## 📊 成功条件

- [ ] TypeScript エラー: 0件
- [ ] テストカバレッジ: ≥80%
- [ ] 品質スコア: ≥80点
- [ ] セキュリティスキャン: 脆弱性0件

## 🤖 Agent実行設定

- **自動実行**: 有効
- **優先度**: High
- **期待実行時間**: 3-5分

---

**ラベル**: 🤖agent-execute, 🆕feature, 🔴priority-high

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

## 実行例

### Example 1: 新機能Issue作成

```bash
/create-issue
```

```
🤖 Agent Issue Creator

Issue タイトルを入力してください:
> ユーザープロフィール編集機能

Issue タイプを選択してください:
1. 🆕 feature
...
> 1

要件を入力してください (完了したら空行):
> プロフィール編集画面UI
> プロフィール更新API
> バリデーション実装
> ユニットテスト作成
>

技術スタックを入力してください (任意):
> React, TypeScript, REST API

制約事項があれば入力してください (任意):
> パスワード変更は別機能として実装

Agent自動実行を有効にしますか? (y/n):
> y

優先度を選択してください:
1. 🔴 High
2. 🟡 Medium
3. 🟢 Low
> 2

担当者を指定しますか? (GitHubユーザー名、空でスキップ):
>

✅ Issue作成完了
Issue番号: #123
URL: https://github.com/owner/repo/issues/123

🤖 Agent実行が開始されます (約3-5分)
進捗確認: npm run agents:parallel:exec -- --issue 123 --dry-run
```

### Example 2: バグ修正Issue作成

```bash
/create-issue
```

```
Issue タイトルを入力してください:
> ログイン時にトークンが更新されない

Issue タイプを選択してください:
> 2 (bug)

要件を入力してください:
> トークンリフレッシュロジック修正
> エラーハンドリング追加
> E2Eテスト追加
>

Agent自動実行を有効にしますか? (y/n):
> y

優先度を選択してください:
> 1 (High)

✅ Issue作成完了
Issue番号: #124
URL: https://github.com/owner/repo/issues/124

🚨 優先度: High のため、即座にAgent実行されます
```

## GitHub CLI統合

内部的に `gh` コマンドを使用してIssueを作成します:

```bash
gh issue create \
  --title "ユーザープロフィール編集機能" \
  --body "$(cat issue-body.md)" \
  --label "🤖agent-execute,🆕feature,🟡priority-medium" \
  --repo owner/repo
```

## ラベル自動付与

Issue タイプに応じて自動的にラベルが付与されます:

| タイプ | ラベル |
|--------|--------|
| feature | 🆕feature, enhancement |
| bug | 🐛bug |
| refactor | ♻️refactor |
| docs | 📝documentation |
| performance | ⚡performance |
| security | 🔒security |
| test | 🧪test |

優先度に応じたラベル:

| 優先度 | ラベル |
|--------|--------|
| High | 🔴priority-high |
| Medium | 🟡priority-medium |
| Low | 🟢priority-low |

Agent自動実行:

| 設定 | ラベル |
|------|--------|
| 有効 | 🤖agent-execute |

## Issue Templateとの違い

### GitHub Issue Template (手動作成)

- GitHubのWebUI上で手動で作成
- テンプレートに沿って手動入力
- ラベルは手動で付与

### /create-issue コマンド (Claude Code)

- コマンドラインから対話的に作成
- 自動でテンプレート生成
- ラベル自動付与
- Agent実行設定をその場で決定

## バッチ作成

複数Issueを一度に作成する場合は、YAMLファイルから読み込み可能:

### issues.yaml

```yaml
issues:
  - title: ユーザー認証機能
    type: feature
    requirements:
      - ログイン画面
      - JWT認証
    priority: high
    autoExecute: true

  - title: プロフィール編集
    type: feature
    requirements:
      - 編集画面UI
      - 更新API
    priority: medium
    autoExecute: true

  - title: パフォーマンス改善
    type: performance
    requirements:
      - バンドルサイズ削減
      - 遅延読み込み実装
    priority: low
    autoExecute: false
```

### バッチ実行

```bash
# Claude Code内で
/create-issue --batch issues.yaml
```

**期待される出力**:

```
🤖 Batch Issue Creator

issues.yaml を読み込み中...
3件のIssueを作成します

1/3: ユーザー認証機能
   ✅ Issue #125 作成
   🤖 Agent実行開始

2/3: プロフィール編集
   ✅ Issue #126 作成
   🤖 Agent実行開始

3/3: パフォーマンス改善
   ✅ Issue #127 作成
   ⏸️  手動実行待ち

✅ バッチ作成完了
作成数: 3件
Agent自動実行: 2件
手動実行待ち: 1件

詳細: .ai/issues/batch-2025-10-08.json
```

## 設定

### .claude/settings.local.json

```json
{
  "issueCreation": {
    "defaultPriority": "medium",
    "autoExecuteByDefault": true,
    "defaultLabels": ["🤖agent-execute"],
    "requireApproval": false,
    "templates": {
      "feature": ".github/ISSUE_TEMPLATE/feature.md",
      "bug": ".github/ISSUE_TEMPLATE/bug.md"
    }
  }
}
```

## トラブルシューティング

### Q1: `gh` コマンドが見つからない

```bash
# GitHub CLI インストール
brew install gh  # macOS
# または
npm install -g @github/cli

# 認証
gh auth login
```

### Q2: Issue作成権限エラー

```
Error: Resource not accessible by personal access token

対処法:
1. GitHub Token の権限確認
   - repo スコープが必要
2. .env ファイルの GITHUB_TOKEN を確認
```

### Q3: Agent が自動実行されない

```
確認事項:
1. 🤖agent-execute ラベルが付与されているか確認
2. GitHub Actions Workflow が有効か確認
3. ANTHROPIC_API_KEY が Secrets に設定されているか確認
```

## 関連ドキュメント

- [.github/ISSUE_TEMPLATE/agent-task.md](../../.github/ISSUE_TEMPLATE/agent-task.md) - Issue Template
- [docs/AGENT_OPERATIONS_MANUAL.md](../../docs/AGENT_OPERATIONS_MANUAL.md) - Agent運用マニュアル
- [GitHub CLI Documentation](https://cli.github.com/manual/)

---

🤖 このコマンドは対話的にIssueを作成し、Agent実行を効率化します。
