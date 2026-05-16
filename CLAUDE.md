# Task Board — Claude Code ガイド

## プロジェクト概要

Vite + React で作成したタスク管理ボードアプリ。

### 技術スタック

| カテゴリ | 採用技術 |
|---|---|
| UI ライブラリ | React 18 |
| ビルドツール | Vite 5 |
| 言語 | JavaScript (JSX) |
| スタイル | コンポーネント単位の Plain CSS (`ComponentName.css`) |
| 状態管理 | React `useState` (外部ライブラリなし) |
| 永続化 | `localStorage` |
| デプロイ | GitHub Actions → GitHub Pages |

### ディレクトリ構成

```
src/
├── App.jsx              # ルートコンポーネント・状態管理
├── App.css
├── index.css            # グローバルスタイル
└── components/
    ├── TaskInput.jsx    # タスク入力フォーム
    ├── TaskInput.css
    ├── TaskList.jsx     # タスク一覧
    ├── TaskList.css
    ├── TaskItem.jsx     # 個別タスク（チェックボックス・削除）
    └── TaskItem.css
```

### コンポーネント命名規約

- **ファイル名**: PascalCase（例: `TaskItem.jsx`）
- **コンポーネント名**: ファイル名と同じ PascalCase
- **CSS ファイル**: コンポーネントと同名（例: `TaskItem.css`）、同じディレクトリに配置
- **クラス名**: kebab-case（例: `.task-item`, `.delete-btn`）
- **props**: camelCase（例: `onToggle`, `onDelete`）
- 新しいコンポーネントはすべて `src/components/` 以下に配置する

## デプロイ先

**GitHub Pages**: https://yubashoheisamurai.github.io/task-board/

`main` ブランチへのプッシュで GitHub Actions が自動的にビルド＆デプロイする。
ワークフロー: `.github/workflows/deploy.yml`

## 開発コマンド

```bash
npm run dev    # 開発サーバー起動
npm run build  # 本番ビルド
npm run preview # ビルド成果物のプレビュー
```

## Git 運用ルール

### コード変更後は必ずプッシュする

コードを変更するたびに、以下の手順でコミットしてGitHubにプッシュすること。

```bash
git add <変更ファイル>
git commit -m "変更内容の簡潔な説明"
git push origin <ブランチ名>
```

- コミットメッセージは変更の「なぜ」を中心に、英語または日本語で簡潔に書く
- `git add .` や `git add -A` は避け、変更ファイルを明示的に指定する
- `.env` や認証情報を含むファイルは絶対にコミットしない
- `main` ブランチへの直接プッシュは避け、フィーチャーブランチを使う
- force push (`git push --force`) は原則禁止

### ブランチ戦略

- `main` — 本番相当の安定ブランチ
- `feature/<機能名>` — 新機能開発
- `fix/<バグ名>` — バグ修正

## コーディング規則

- コメントは「なぜそうするか」が非自明な場合のみ追加する
- 不要な抽象化・将来の拡張用コードは書かない
- セキュリティ上のリスク（XSS、インジェクション等）に注意する

## 開発フロー

1. フィーチャーブランチを切る
2. 実装する
3. コミット & プッシュ（変更のたびに）
4. Pull Request を作成してレビューを受ける
5. `main` にマージ
