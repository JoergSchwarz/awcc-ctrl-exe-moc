# Skills & Lessons

本プロジェクトで得たコーディング/運用の学びを簡潔に記録します。非規範（方針は AGENTS.md）。増えたら将来分割を検討します。

## Coding（Rust/Win32）

- windows クレート（0.52系）の多くの API は `Result` を返す。
  - `LoadIconW`/`LoadCursorW`/`CreatePopupMenu` は `?` または `match` で扱う。
  - `AppendMenuW`/`TrackPopupMenu`/`DestroyMenu` は引数型（`IntoParam`）や `Option<*const RECT>` に注意。
- 非表示ウィンドウ＋トレイの最小構成:
  - 隠しウィンドウ作成 → `Shell_NotifyIconW` 追加 → 右クリックでポップアップ → 終了時に削除。
  - `WM_USER + n` の独自メッセージで衝突回避。
- ワークスペースは edition 2021 に合わせ `resolver = "2"` を設定。

## Toolchain / Build（Windows GNU + MSYS2）

- MinGW は MSYS2 の UCRT64 環境で導入（`mingw-w64-ucrt-x86_64-toolchain`）。
- PATH 恒久設定は GUI（`sysdm.cpl`）または PowerShell の .NET API を使用（`setx` は 1024 文字制限に留意）。
- PowerShell の実行ファイル検索は `Get-Command` または `where.exe` を使用（`where` は `Where-Object` の別名）。

## Docs / CI / 運用

- markdownlint に準拠（フェンスに言語、リスト前後の空行、番号整形）。
- Mermaid は `<name>` などの角括弧を避け、`NAME` 等の表記が安定。
- 単独開発時のエージェントコミットは PR 必須（自己レビュー＋CI通過）。
