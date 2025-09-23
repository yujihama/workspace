# freqtrade/freqtrade — リポジトリの要点まとめ

以下は GitHub の「freqtrade/freqtrade」リポジトリ（Free, open source crypto trading bot）のページ内容を分かりやすく整理したものです。

---

## 概要
- Freqtrade は Python（3.11+）で書かれたオープンソースの暗号資産（仮想通貨）自動売買ボット。
- 特徴：複数取引所対応、Telegram/WebUI 操作、バックテスト、マネジメント、機械学習による戦略最適化（FreqAI）等。
- 公式サイト：https://www.freqtrade.io
- ライセンス：GPL-3.0
- GitHub 指標（ページ時点）：約 42.3k stars、8.6k forks、複数のブランチ（develop / stable など）

---

## 主要機能
- Python 3.11+ 対応（Windows / macOS / Linux）
- 永続化：sqlite ベース
- Dry-run（実資金を使わないテスト実行）
- バックテスト、プロット機能
- 機械学習による戦略最適化（FreqAI）
- 動的または静的なホワイトリスト／ブラックリストで通貨選別
- 内蔵 WebUI と Telegram による操作
- フィアット表示の損益、パフォーマンスレポート

---

## サポートされる取引所（抜粋）
- Binance, Bitmart, BingX, Bybit, Gate.io, HTX, Hyperliquid（DEX）, Kraken, OKX（MyOKX含む）
- コミュニティで動作確認済み：Bitvavo, Kucoin
- 参考：取引所ごとの特記事項は docs/exchanges.md を参照

対応先は ccxt による多くの取引所が対象だが、全ての環境での動作保証はない。

### 先物（実験的）
- Binance, Gate.io, Hyperliquid, OKX, Bybit など

---

## クイックスタート
- まずは Docker Quickstart（推奨）を参照：https://www.freqtrade.io/en/stable/docker_quickstart/
- ネイティブインストール手順：Installation ドキュメント参照

---

## 基本使用（CLI）
主なサブコマンド（抜粋）:
- trade, create-userdir, new-config, show-config, new-strategy
- download-data, convert-data, trades-to-ohlcv, list-data
- backtesting, backtesting-show, backtesting-analysis
- hyperopt, hyperopt-list, hyperopt-show
- list-exchanges, list-markets, list-pairs, list-strategies
- webserver, install-ui, plot-dataframe, plot-profit
- strategy-updater, lookahead-analysis, recursive-analysis
- 典型的なヘルプ表示：`freqtrade -h`

（詳細は README や CLI ヘルプ参照）

---

## Telegram コマンド（主なもの）
- /start — トレーダー開始
- /stop — トレーダー停止
- /stopentry — 新規エントリー停止
- /status [table] — オープントレード一覧
- /profit [n] — 過去 n 日間の累積損益
- /profit_long、/profit_short — ロング／ショート別
- /forceexit <pair>|all — 即時決済（minimum_roi を無視）
- /performance — 通貨ペア別パフォーマンス
- /balance — 残高表示
- /daily — 日別損益
- /help, /version など

（Telegram は必須ではないが便利）

---

## 開発ブランチとワークフロー
- develop：新機能・開発用（安定を保つ努力ありだが breaking change の可能性あり）
- stable：最新の安定リリース
- feat/*：個別機能の作業ブランチ（一般利用は推奨されない）
- PR は develop ブランチ宛に作成すること（重要）

---

## サポート / コントリビュート
- Discord（コミュニティ）：https://discord.gg/p7nuUNVfP7
- Issue 登録：GitHub Issues（事前検索を推奨）
- Feature request：Issues の enhancement ラベルを確認
- Pull Request：Contributing ドキュメントを必読
- 初心者向け：good first issue ラベルあり

---

## 注意事項（重要）
- これは教育目的のソフトウェア：損失リスクあり。Dry-run を必ず使用して仕組みを理解してから実運用すること。
- 作者・関係者は取引結果について責任を負わない旨が明示されている。
- システム時刻（NTP）を正確に保つことが推奨（取引所との通信問題回避のため）。

---

## 動作環境（推奨最低要件）
ハードウェア（推奨最小）：
- 2 GB RAM, 1 GB ディスク, 2 vCPU（クラウドインスタンス推奨）

ソフトウェア：
- Python >= 3.11
- pip, git
- TA-Lib（技術指標用）
- virtualenv（推奨）
- Docker（推奨）

---

## リポジトリ構成（主なフォルダ／ファイル）
- ディレクトリ：.devcontainer, .github, docs, freqtrade, ft_client, scripts, tests, user_data など
- 重要ファイル：README.md, LICENSE, Dockerfile, docker-compose.yml, pyproject.toml, requirements*.txt, CONTRIBUTING.md

---

## ドキュメント / リソース
- 公式ドキュメント（詳細）: https://www.freqtrade.io
- 取引所別注意点: docs/exchanges.md
- FreqAI（ML 機能）: docs の FreqAI セクション
- リリース・リリース履歴は GitHub Releases を参照

---

## その他のメタ情報
- 言語：Python が約 98%（他に Jinja, PowerShell, Notebook 等）
- コントリビューター数やリリースの履歴あり（ページ参照）

---

必要であれば、次のいずれかを詳細にまとめます：
- インストール手順（Docker / ネイティブ）  
- CLI コマンドの具体的な使い方例（backtesting, trade 実行など）  
- FreqAI の概要と使い方  
どれを詳しく知りたいか教えてください。