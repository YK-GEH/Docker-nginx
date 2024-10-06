DockerとNginxを使用して、VSCode上でWebサーバを構築する手順

### 概要

- **Docker**：アプリケーションをコンテナとして実行するためのプラットフォーム。
- **Nginx**：Webサーバやリバースプロキシとして利用されるソフトウェア。
- **VSCode**：統合開発環境 (IDE) として開発に使用。

### 手順

### 1. **プロジェクトフォルダの作成**

まず、プロジェクト用のディレクトリを作成し、必要なファイルを準備します。

```bash
bash
コードをコピーする
mkdir nginx-docker
cd nginx-docker
```

### 2. **Dockerfile の作成**

`Dockerfile`をプロジェクトフォルダに作成します。

```
Dockerfile
コードをコピーする
# ベースイメージとしてnginxを使用
FROM nginx:latest

# Nginxの設定ファイルをコンテナ内にコピー
COPY ./default.conf /etc/nginx/conf.d/default.conf

# Webコンテンツをコピー
COPY ./html /usr/share/nginx/html

# コンテナが使用するポート
EXPOSE 80
```

### 3. **Nginx 設定ファイルの作成**

次に、Nginxの設定ファイル `default.conf` を作成します。

```
conf
コードをコピーする
server {
    listen 80;
    server_name localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
}
```

### 4. **HTMLファイルを作成**

簡単なHTMLファイルを `html` ディレクトリに作成します。

```bash
bash
コードをコピーする
mkdir html
```

`html/index.html` ファイルを作成し、次のように記述します。

```html
html
コードをコピーする
<!DOCTYPE html>
<html>
<head>
    <title>Docker Nginx Web Server</title>
</head>
<body>
    <h1>Hello from Nginx running in Docker!</h1>
</body>
</html>
```

### 5. **docker-compose.yml の作成（オプション）**

複数のコンテナを管理する場合、`docker-compose.yml`を作成します。

```yaml
yaml
コードをコピーする
version: '3'
services:
  web:
    build: .
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
```

### 6. **Dockerイメージのビルド**

VSCodeのターミナルで、次のコマンドを実行してDockerイメージをビルドします。

```bash
bash
コードをコピーする
docker build -t my-nginx-app .
```

### 7. **コンテナの起動**

コンテナを起動します。

```bash
bash
コードをコピーする
docker run -d -p 8080:80 my-nginx-app
```

ブラウザで `http://localhost:8080` にアクセスすると、Nginxサーバが正常に動作していることが確認できます。

### VSCodeを活用するポイント

- **Docker拡張機能**：VSCodeのDocker拡張機能をインストールすると、VSCode内でDockerコンテナを簡単に操作できます。
- **Live Serverプラグイン**：VSCodeで開発中のWebページを即座に確認できます。

これで、DockerとNginxを使ってVSCode上で簡単なWebサーバを構築できます。
