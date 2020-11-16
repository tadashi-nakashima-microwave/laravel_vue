FROM node:lts-alpine

# 静的コンテンツを配信するシンプルな http サーバをインストールする
RUN npm install -g http-server \
  && npm install -g @vue/cli \
   && echo y | vue create -d app \
   && cd /app \
   && npm run build

EXPOSE 8080
CMD [ "http-server", "/app/dist" ]

