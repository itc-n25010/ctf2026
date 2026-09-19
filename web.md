# Webサーバ構築マニュアル

### Apacheインストール

```bash
sudo apt update
sudo apt install apache2 -y
sudo apt install apache2-utils -y
```

### Apache起動確認

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```

ブラウザで以下のURLにアクセスし、「Apache2 Ubuntu Default Page」が表示されるか確認

```bash
http://<サーバーIP>
```

## Basic認証

### ユーザー作成

```bash
sudo htpasswd -c /etc/apache2/.htpasswd user1
```

### 設定ファイル編集

```bash
sudo vi /etc/apache2/sites-available/000-default.conf
```

<VirtualHost *:80>の中に以下を追加

```bash
<Directory /var/www/html>
    AuthType Basic
    AuthName "Restricted Area"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```

### Apache設定の確認

```bash
sudo apachectl configtest
```

### 再起動

```bash
sudo systemctl restart apache2
```

### 動作確認

```bash
curl http://localhost
```
認証がかかっていれば、401 Unauthorizedになる

```bash
curl -u user1:password http://localhost
```
認証成功でHTMLが表示される。

- ブラウザで確認する場合
```
http://<IPアドレス>
```
アクセス時にユーザー名とパスワードの入力画面が表示されれば成功。