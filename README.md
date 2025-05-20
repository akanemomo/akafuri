# Akafuri

## 環境構築

### Docker ビルド

```
git clone <リポジトリURL>
cd <プロジェクトディレクトリ>
docker-compose up -d --build
```

### Laravel 環境構築

```
docker-compose exec php bash
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan db:seed
composer require doctrine/dbal  # エラー発生時のみ　カラム名変更などに使用
```

### 公開ストレージリンクの作成（画像表示に必要）

Laravelで画像を表示するには、以下のコマンドで
`public/storage` ディレクトリにリンクを作成する必要があります。

```bash
php artisan storage:link
```

### .envファイルの修正について

`.env` は `.env.example` をコピーした後、以下の環境変数を記載してください。

```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel_db
DB_USERNAME=laravel_user
DB_PASSWORD=laravel_pass
```
これらの値は、Dockerで構築するMySQLコンテナの設定（`docker-compose.yml`）と一致させる必要があります。

---

### MySQL 設定（docker-compose.yml）
```yaml
mysql:
  platform: linux/x86_64
  image: mysql:8.0.26
  environment:
    MYSQL_ROOT_PASSWORD: root
    MYSQL_DATABASE: laravel_db
    MYSQL_USER: laravel_user
    MYSQL_PASSWORD: laravel_pass

## 使用技術（実行環境）

- PHP: 7.4.9
- Laravel: 8.83.8
- MySQL: 8.0.34
- nginx: 1.21.1
- Fortify: ログイン機能に使用

## 開発用 URL（仕様ベース、未実装の画面も含む）

- 商品一覧画面（トップ画面）：http://localhost/
- 商品一覧画面（マイリスト）：http://localhost/?tab=mylist ※未実装
- 会員登録画面：http://localhost/register
- ログイン画面：http://localhost/login
- 商品詳細画面：http://localhost/item/:item_id
- 商品購入画面：http://localhost/item/:item_id/purchase
- 住所変更ページ：http://localhost/item/:item_id/address
- 商品出品画面：http://localhost/sell
- プロフィール画面：http://localhost/mypage ※未実装
- プロフィール編集画面：http://localhost/mypage/profile ※未実装
- 購入済み商品一覧：http://localhost/mypage?tab=buy ※未実装
- 出品済み商品一覧：http://localhost/mypage?tab=sell ※未実装
- phpMyAdmin：http://localhost:8080

## ER 図

![ER図](./resources/docs/akafuri_er.png)
Draw.io ファイル：[akafuri_er.drawio](./resources/docs/akafuri_er.drawio)

## 実装済み機能

- 会員登録／ログイン機能（Fortify）
- 商品一覧表示（トップページ）
- 商品詳細ページ
- 商品出品機能（画像／カテゴリ／状態／価格など）
- いいね機能（登録・解除、いいね数表示）
- コメント送信機能（ログインユーザーのみ、バリデーションあり、コメント数表示）
- 送付先住所変更機能（ログインユーザーのみ、バリデーションあり、購入画面に反映）
- 商品購入機能（支払方法選択、登録済住所を使用）

## 今後の予定
- プロフィール登録／編集機能（画像・名前・郵便番号・住所の管理）
- マイページ機能（購入済商品・出品済商品）
- 商品検索／絞り込み機能（キーワード・カテゴリ・状態）

---

以上が **Akafuri** の初期セットアップおよび実装概要です。
