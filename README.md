# agent-timeline

Claude Code のセッションの進み具合を、チャットの横のパネルとプロンプトの上の帯に表示する mod です。
Claude デスクトップアプリの Code タブで使うことを想定しています。

## 表示するもの

- **プロンプトの上の帯**: 計画の進捗バー、完了したステップ数、経過時間、残り時間の目安、いま進めているステップ。
- **計画の更新の下のカード**: その更新で進捗が何 % から何 % になったか、どのステップが動いたか。
- **タイムラインのパネル**: 計画、直近の指示、直近のまとめ、定期レポート、履歴、作成した PR。
- **子セッション**: このセッションから立ち上げたセッションごとに、状態、進捗、いまのステップ、最新のまとめを 1 行ずつ表示します。行を開くと、その子セッションのパネル全体を表示します。

パネルは `/timeline` で開きます。

## 定期レポート

作業が続いている間、15 分、1 時間、4 時間ごとに短い進捗レポートを作ります。
レポートは haiku が書きます。
渡すのはこの mod が記録した計画と履歴だけで、会話の中身は送りません。
15 分の間にツールの呼び出しがなければ、その回はモデルを呼びません。

`/timeline report` を実行すると、その場で 15 分のレポートを 1 回作ります。

## データの置き場所

各セッションは自分の状態を `~/.claude/agent-board/<セッション ID>.json` に書きます。
親セッションはこのフォルダを読んで、子セッションを表示します。
24 時間以上更新のないファイルは表示しません。

## インストール

ターミナルの Claude Code で次を実行します。

```
/plugin install agent-timeline --marketplace malanjp/agent-timeline
```

マーケットプレイスの追加を聞かれたら `y` で答え、インストール先にはユーザースコープを選びます。

シェルからは次のコマンドでも入れられます。

```bash
claude plugin install agent-timeline --marketplace malanjp/agent-timeline
```

デスクトップアプリでは `/plugin` を使えません。
プロンプト欄の横の + から Plugins を開き、Add marketplace に `malanjp/agent-timeline` を入れてから、Add plugin で追加します。

## 開発

```bash
claude plugin test .
claude plugin validate .
```

## ライセンス

MIT License です。
詳しくは [LICENSE](LICENSE) を見てください。
