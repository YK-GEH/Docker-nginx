# ベースイメージとしてNginxを使用
FROM nginx:latest

# カスタムのNginx設定ファイルをコンテナ内にコピー
COPY ./default.conf /etc/nginx/conf.d/default.conf

# Webコンテンツをコピー
COPY ./html /usr/share/nginx/html

# コンテナが使用するポート
EXPOSE 80 