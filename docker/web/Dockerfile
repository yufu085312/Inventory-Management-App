# ベースイメージ
FROM node:18 AS builder

# 作業ディレクトリを設定
WORKDIR /app

# パッケージファイルをコピーして依存関係をインストール
COPY package.json package-lock.json ./
RUN npm install

# アプリケーションコードをコピー
COPY . .

# Reactアプリをビルド
RUN npm run build

# 本番用の軽量サーバー
FROM nginx:alpine AS production

# ビルド済みの静的ファイルをNginxで提供
COPY --from=builder /app/dist /usr/share/nginx/html

# nginx.confを適切な場所にコピー
COPY nginx.conf /etc/nginx/conf.d/default.conf

# ポート番号
EXPOSE 80

# Nginxを起動
CMD ["nginx", "-g", "daemon off;"]
