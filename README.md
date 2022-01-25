# laravel-vue-spa

SPA アプリケーションの構築  
実務で使用した環境の簡易的な再現

## 構成

### API server コンテナ（SPA バックエンド、ユーザー管理）

- nginx
- php 8
- laravel (passport, breeze)
- mysql 8

#### コンテナ初期化

```bash
composer install
chown -R www-data:www-data storage/
cp .env.example .env
php artisan key:generate
```

.env 編集（DB コンテナ接続設定）

```
DB_HOST=db
DB_DATABASE=dev_db
DB_PASSWORD=root
```

```bash
php artisan migrate:refresh --seed
php artisan passport:keys
```

### SPA クライアントコンテナ（SPA フロントエンド）

- typescript
- vue 3.2
- vue-router
- element-plus（UI フレームワーク）

#### いつか対応するかも

- vuelidate  
  element-plus 標準ではバリデーションに async-validator が使用されていますが  
  vuelidate を導入して利用すると、rules ごとのエラーメッセージなどにも対応できます

#### コンテナ実行

```
yarn
yarn dev
```

### その他

#### 認証

- Authorization Code Grant Flow with Proof Key for Code Exchange（PKCE 4）

##### Demo ユーザー

demo@example.com / demo@demo
