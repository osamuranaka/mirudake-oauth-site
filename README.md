# 見るだけスマホ解決室｜Google OAuth公開サイト

Music TherapyのGitHub Pages運用と同じ構成を使う、見るスマホ専用サイトです。

## 想定構成
- GitHubリポジトリ：osamuranaka/mirudake-oauth-site（新規作成、Public）
- カスタムドメイン：https://mirudake-api.ants-biz.jp/ （DNS・公開前の候補。現時点では未開通）
- プライバシーポリシー：https://mirudake-api.ants-biz.jp/privacy/
- 利用条件：https://mirudake-api.ants-biz.jp/terms/
- Google Cloudプロジェクト：youtube-analytics-512307
- Google OAuthクライアント：見るスマホ用の既存Desktopクライアントを維持
- Music Therapy側のGitHub／DNS／Google Cloud／トークンは変更しない

## 手順
1. 公開前にindex.html/privacy/index.html/terms/index.htmlの記述が実際の管理・データ利用方針と一致するか確認する。
2. GitHubアカウントosamuranakaでmirudake-oauth-siteをPublicとして作成する。
3. ZIPを解凍し、index.html、privacy/index.html、terms/index.html、style.css、.nojekyll、CNAMEをリポジトリのルートに配置する。READMEは公開不要。
4. Settings > Pages > Build and deploymentでDeploy from a branch、main、/(root)を設定。
5. Settings > Pages > Custom domainに mirudake-api.ants-biz.jp を登録。DNSより先にGitHub側で設定。
6. ants-biz.jpのDNS管理画面でホスト mirudake-api に CNAME osamuranaka.github.io を追加。既存musictherapy-apiなどのレコードは変更しない。
7. DNS・GitHub Pagesの公開が正常になったらEnforce HTTPSを設定。上記3 URLのアクセスを検証。
8. Google Search Consoleにおけるants-biz.jpの所有権確認状態を調べる。未確認なら指示どおり確認する。
9. Google Cloud > Google Auth Platform > Branding（youtube-analytics-512307）にホーム・プライバシーURL等を登録。ドメインはants-biz.jp。実際のUIの要件と審査案内を確認する。
10. Audienceで「本番環境」に切り替えられるか確認。実際の公開・検証要求に従う。
11. 本番切替後、古いtoken.jsonを安全に保全した上で、見るスマホアカウントのみを再認証して新しいトークンを取得する。
12. 接続・自動更新検証後に11月9日分のZIP復旧と11月16日03:00の定期実行条件を確認する。

## 重要事項
- Publicリポジトリへ token.json、client_secrets.json、Google Analytics実データ、YouTube内部レポート等を絶対にアップロードしない。
- アプリ利用者が個人に限られていてもOAuthスコープの検証やGoogle APIポリシーが免除されるとは限らない。
- OAuthの公開状態変更だけで失効済みrefresh tokenは復活しない。
- 自動更新の失敗が今後絶対に起こらないとは保証できない。
- GitHubリポジトリ作成、Pages・DNS設定、Google Cloud設定はこのZIP作成時点では未実施。

参考：
https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
https://support.google.com/cloud/answer/13807376?hl=en
