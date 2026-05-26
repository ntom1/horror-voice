# horror-voice エージェント運用ルール

<!-- agent-rules:shared-rule-start -->
## 上位ルール参照

このrepoでは、まず上位の共通ルールを必ず適用する。
共通ルールは長く複製せず、作業内容に応じて必要な詳細だけ参照すること。

- Codex向け共通ルール: `/Users/jarvis/AGENTS.md`
- Claude Code向け共通ルール: `/Users/jarvis/CLAUDE.md`
- Development配下共通ルール: `/Users/jarvis/Development/AGENTS.md`
- Skill原本管理: `/Users/jarvis/agent-skills/`
- 詳細ルール索引: `/Users/jarvis/Development/agent-rules/AGENTS.md`

共通ルールとこのrepo固有ルールが矛盾する場合は、より上位の共通ルールを優先すること。
このファイルには、共通ルールを複製せず、このrepo固有の差分だけを書くこと。

Skillを作成・更新する場合は、`~/.agents/skills/` や `~/.claude/skills/` を直接編集せず、必ず `/Users/jarvis/agent-skills/skills-src/<skill-name>/SKILL.md` を原本とすること。
Markdownは、ユーザーから明示的な指定がない限り日本語で作成・更新すること。
<!-- agent-rules:shared-rule-end -->

## このrepo固有ルール

- 目的: お化け屋敷・ホラー演出向けの、ブラウザだけで動く怖い声変換ツールを提供する。
- アプリ構成: `index.html` 単体の静的Webアプリ。音声処理はTone.js（MIT License）とWeb Audio APIで端末内実行し、音声データを外部へ送信しない。
- 起動方法: 静的ファイルとして `index.html` を開ける。ローカルHTTPで確認する場合は `python3 -m http.server <port>` を使う。`~/Development/` 共通ルールにより `9999` は使わない。
- 検証コマンド: JavaScript構文確認は `sed -n '/^  <script>$/,/^  <\\/script>$/p' index.html | sed '1d;$d' | node --check -`、空白差分確認は `git diff --check` を使う。UI/音声変換はブラウザで音声ファイルを読み込み、各プリセットの変換とWAV保存リンク生成を確認する。
- 触ってはいけないファイル/ディレクトリ: 生成されたWAV、録音音声、検証用音声ファイル、ブラウザキャッシュ、`node_modules/` などの一時・生成物はrepoへ追加しない。
- GitHubへpushする前の確認事項: READMEの依存関係・プライバシー・動作確認チェックリストが実装と一致していること、Tone.js CDNが使える場合と読み込めない場合のフォールバックを確認すること、公開repoに音声データや秘密情報が含まれていないことを確認すること。
