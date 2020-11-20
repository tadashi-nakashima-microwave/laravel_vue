

今どきのWEBシステム開発
コンテナとサーバレス


■自己紹介

エンジニア歴15年、最近子供が生まれた一児の父。

これまでのキャリアでは、組み込み系のシステムを開発する案件が多く
WEBシステム開発の経験は浅い
そのため、最近は、WEBシステム開発案件に入ると、キャッチアップに苦労している



■このセッションでできるようになること
・Dockerを使って、フロント、バックエンド、DBの3層アーキテクチャの開発環境を構築することができるようになる
・上記で構築したアーキテクチャをそのままAWSのサーバレスのサービスにデプロイできるようになる。


■背景
最近の開発案件は、2000年あたりのITバブル時に創業した企業から降りてくる案件が
多い印象がある。


そのような企業の多くは、オンプレミス（自前で構築・運用するサーバー）で構築した
モノリシック（１つのサーバーで多くのサービスが動いている）な古いシステムで、
使用しているフレームワークも古く、以下のような課題がある。

・近年の複雑化する機能要求に素早く追随できない
・急激な需要の増加に対応できない



現在抱えている課題
・言語バージョン及びフレームワークが古い 。技術的負債が大きく改修の工数が増える。
・複数の サービス プロダクト が混在して 同じシステムに同居しているためお互いの負荷が影響してしまう。
・オンプレミス 構成 の構成だと ビジネスモデルと あっていないため 費用対効果が薄い 。

プロジェクトの目的
・費用対効果が高く、障害が起きにくいシステムを構築する
・サービス同士が影響しない環境にする
・シンプルな構成に作り直すことで改修やテストのコストを減らし、システム運用をしやすくする


このような状況の中、求められるエンジニアの要件が変化してきている。



①市場の変化に合わせて柔軟かつ迅速にビジネスモデルを変更できず、デジタル競争の敗者になってしまう
②システムの維持管理費が高額化することで技術的負債を抱え、業務基盤そのものの維持・継承が困難になる
③保守運用の担い手が不足することで、サイバーセキュリティや事故・災害によるシステムトラブルやデータ滅失などのリスクが高まる

DXレポート ～ITシステム「2025年の崖」克服とDXの本格的な展開～
https://www.meti.go.jp/shingikai/mono_info_service/digital_transformation/20180907_report.html



■目的

■対象者
・エンジニアを目指している人
・これからVue.jsやLaravelなどを学ぼうとしている人
・Linuxを学ぼうとしている人
・Dockerを学ぼうとしている人
・DevOpsを学ぼうとしている人
・すでに案件に入っていて、スキルアップしたい人
・AWSを理解しようとしている人
・Vue.jsやLaravelで作成したプログラムをAWSにアップしようとしている人


■今、開発現場で何が起きているのか？

・事例①
　大手ECパッケージ開発会社

　　開発環境、ステージング環境、本番環境の環境差分が2000箇所以上あり、
　　人の手で修正しなければならない。

　　新しいメンバーがプロジェクトに参画し、自分用の開発環境を構築する際に
　　手順書通り行ってもなかなかうまくいかず、環境構築まで1週間かかる。

　　本番サイトをリニューアルするたびに担当者が徹夜して対応。
　　毎回、リリース作業ミスが発生。

　　限定商品販売時などのセールの際に、サイトにアクセスが集中して、
　　サイトに接続できない状況が発生。


・事例②
　大手施設情報検索＆予約サイト
　　飲食店、薬局、整体、エステなど、会員数2800万人が利用するサービスを展開

　　日曜日の昼間に基幹システムに不具合が発生し、飲食店、薬局、整体、エステなどの
　　予約サービスがすべて止まるという大規模障害が発生した。


・事例③
　AWSの大規模障害
　2019/8/23に東京リージョン（ap-northeast-1）にて、データセンターで
　冷却システムに不具合が発生し、サーバーの温度が上昇したために、電源が停止。

　コンテナ化していたサービスは早く復旧ができた。
　AWS Fargateを使用しているサービスは自動復旧できた。

AWS障害、“マルチAZ”なら大丈夫だったのか？　インフラエンジニアたちはどう捉えたか、生の声で分かった「実情」
https://www.itmedia.co.jp/news/articles/1908/28/news127.html


■今、開発現場で求められているもの

１．コンテナ化(DevOps、マイクロサービス)
２．サーバレス


■モノリスとマイクロサービス

これなら分かる！ マイクロサービス（入門編）～モノリスと比較した特徴、利点と課題
https://codezine.jp/article/detail/11055


■コンテナとは


日本企業のコンテナー導入率は14.2％、Kubernetesは54.7％に--IDC調査
https://japan.zdnet.com/article/35153647/


【再入門】コンテナ技術とは？基本をわかりやすく解説します
https://www.kagoya.jp/howto/rentalserver/container-03/


■目標
Dockerを使って、3層アーキテクチャ(フロント、バックエンド、DB)を
簡単にローカル開発環境とWEB本番環境にデプロイできるようにする。


■Dockerとは？
コンテナ型仮想化技術を実現するソフトウェア。
「パソコンの中に仮想のパソコンを起動する」



■仮想マシンとの違い
容量が少なくて軽い・起動が速い


■なぜDockerなのか？

・開発環境と本番の環境差分を少なくできる
・環境を汚さない
・簡単に構築と破壊ができる


■DevOpsとは


■必要なもの
・git
・Docker
・VSCode
　拡張機能「Docker」「Remote-Containers」



■Dockerのメリット

・公式のコンテナイメージが利用できる


■Dockerでできないこと

・ホストOSと異なるOSは動作できない
　なぜ、Windows上やMac上でLinuxのコンテナを動作できるのか？

　Windows上では、Windows Subsystem for LinuxというWindows上で
　linuxが動作している。

　Mac OS上でLinuxを動作させている。
　過去のDockerではVirtual Boxを利用してLinuxを動作させて


・基本的にはコンテナの中のOSのGUIが使えない
　(X Windows Systemを使えばできるとの情報もあるが、用途からしたらあまり意味がない。
　　GUIを使いたければ、VirtualBoxなどの仮想マシンを使用するべき)

・スマフォアプリの開発
（Dockerの中で動くのはLinux系OSのみ）

・組み込みシステムの開発
（x86系CPU用のイメージはARM系CPUでは動作しない）

・直接SourceTreeが使えない(ボリュームを使えばできる)



■Dockerを使うデメリット
・ネイティブの場合と比較して動作が遅くなる
　（しかし、仮想マシンの場合と比較してそんなに遅くならない）
　https://qiita.com/ksato9700/items/a8ef8b6395058628fa09
・コンテナイメージを作成する場合には知識が必要になる
　（使うだけの場合には、あまり知識はいらない）


■Dockerを使ってみよう


・nginxのサービスを立ち上げてみる


　docker run --name nginx1 -d -p 8080:80 nginx

　とコマンドを実行し、ブラウザでlocalhost:8080を開く


・解説
ここで行っているのは、
１．nginxの公式イメージをDockerHubからパソコンにダウンロード
２．そのイメージからコンテナを作成、起動
３．コンテナのポート番号80番をホスト側の8080番として公開



docker run --name [コンテナ名] -d -p 8080:80 [イメージ名]

--name 起動するコンテナに名前を付ける
-d バックグラウンド（デタッチド）モードで起動
-p コンテナのポートをホスト側に公開する



・用語について

ホスト　　　：Dockerを動かすパソコンのこと

イメージ　　：コンテナを生成するためのひな形（プログラミングでいうところのクラス）

公式イメージ：DockerHubで公開されている公式なイメージ
　　　　　　　具体的には、Ubuntu、CentOSなどのOS、NginxなどのWebサーバ、MySQLなどのDB、
　　　　　　　WordPressなどのCMS、Java・PHPなどの言語が公開されており、簡単に利用することができる。
　　　　http://www.ossplaza.com/oss_info/docker/docker_image_list.html

コンテナ　　：イメージから生成されたアプリケーション（サービス）


コンテナを停止
docker stop nginx1


コンテナを削除
docker rm nginx1


■コンテナにログインする

docker exec -it [コンテナ名] /bin/bash

docker exec -it nginx1 /bin/bash

exec 実行中のコンテナでコマンドを実行
-itは-iと-tを一緒にしたもので、要はコンテナにターミナルでログインする
-i, --interactive コンテナの STDIN にアタッチ
-t, --tty 疑似ターミナル (pseudo-TTY) を割り当て


■Dockerfileを使って、イメージをカスタマイズする




実際に開発したサービスを動作させるためには、
イメージに作成したプログラムを組み込んで新しいイメージを
作成する必要がある。



・Dockerfileとは
　イメージを作成（ビルド）する際の構成情報を記載するファイルです。


先ほどのnginxのイメージに自作のindex.htmlを追加して新しいイメージを作成してみましょう。



・以下の構成のファイル・フォルダを作成します。

nginx
│  default.conf　←　htmlを表示するためにnginxの設定ファイルを変更
│  Dockerfile
└─app
        index.html　←　今回、追加するhtml




index.html
<html>
<body>
TEST
</body>
</html>





Dockerfile

FROM nginx

# ドキュメントルート
ADD app /app
ADD default.conf /etc/nginx/conf.d/default.conf

# ポート設定
EXPOSE 80





default.conf
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /app;

        location / {
        }
}




・カレントディレクトリにあるDockerfileからイメージ(my_nginx)をビルド
docker build . -t my_nginx


・イメージ(my_nginx)からコンテナ(nginx1)を生成して実行
docker run --name nginx1 -d -p 8080:80 my_nginx



・ブラウザでlocalhost:8080を開く



・コンテナを停止
docker stop nginx1


・コンテナを削除
docker rm nginx1


・イメージを削除
docker rmi my_nginx


■Dockerfileの書き方


Dockerfile のベスト・プラクティス
https://docs.docker.jp/develop/develop-images/dockerfile_best-practices.html
https://docs.docker.jp/engine/userguide/eng-image/dockerfile_best-practice.html


公式イメージのサンプル

FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py


FROM は ubuntu:18.04 の Docker イメージからレイヤを作成
COPY は現在のディレクトリから Docker クライアントがファイルを追加
RUN はアプリケーションを make で構築
CMD はコンテナ内で何のコマンドを実行するか指定


・FROM命令　　：元となるイメージファイルを指定する
・COPY命令　　：ホストにあるファイル・フォルダをを新しいイメージにコピーして追加する
・RUN命令 　　：
　FROM命令で指定したベースイメージに対して、追加で実施する処理を記述する
　（よく行うのは、パッケージのインストール、ソースファイルのビルドなどを行う）
　複数の処理がある場合には、できる限り&&で接続して、RUN命令を一つにまとめる。
　複数行に分かれる場合には「\」で指定する

・EXPOSE命令　：外部に公開するポートを指定
・CMD命令 　　：コンテナ起動時に実施する処理を


DockerのRUNとCMDの違い
https://qiita.com/YusukeHigaki/items/044164837daa5e845d50


■練習：vue.jsのコンテナを立ち上げる


Dockerfile

FROM node:lts-alpine

# 静的コンテンツを配信するシンプルな http サーバをインストールする
RUN npm install -g http-server \
  && npm install -g @vue/cli \
   && echo y | vue create -d app \
   && cd /app \
   && npm run build

EXPOSE 8080
CMD [ "http-server", "/app/dist" ]


docker build . -t my_vue
docker run --name vue1 -d -p 8080:8080 my_vue


docker exec -it vue1 sh



・コンテナを停止
docker stop vue1


・コンテナを削除
docker rm vue1


・イメージを削除
docker rmi my_vue




■練習：VSCodeでコンテナ内のファイルを編集する

VSCodeでコンテナを選択して右クリックして、Attach Visual Studio Codeを選択する
/app/src/App.vueを編集

VSCodeでターミナルを開く
npm run build

ブラウザでlocalhost:8080を開く


コマンドラインで行う場合
docker exec -it vue1 sh
cd /app
npm run build



■練習：docker上でgitを使う



■コンテナ同士を連携する①（ネットワークの連携）

docker run -it --name alpine1 -d alpine
docker run -it --name alpine2 -d alpine
docker exec -it alpine2 sh
ping alpine1
接続できない

コンテナ停止＆削除
docker rm -f alpine1
docker rm -f alpine2


docker network create my-network
docker run -it --name alpine1 -d --net my-network alpine
docker run -it --name alpine2 -d --net my-network alpine
docker exec -it alpine2 sh
ping alpine1
接続できる

コンテナ停止＆削除
docker rm -f alpine1
docker rm -f alpine2


docker network ls
docker network rm my-network
docker network ls


コンテナリンクという機能もあるが古い機能で削除される予定
https://docs.docker.jp/engine/userguide/networking/default_network/dockerlinks.html



■Alpine Linuxとは

超軽量なLinux。軽量なのでDockerでよく使われる。

CentOS 約4GB
Ubuntu 約700MB
Alpine 約100MB

超軽量なAlpine Linuxについて調べた
https://qiita.com/ryuichi1208/items/6020cfabc92bd8153654


■コンテナ同士を連携する②（ファイルの連携）





■ローカルPCのフォルダをコンテナと連携する
　（ローカルPCのソースファイルを編集するとコンテナに反映される）
　バインドマウント


■永続ストレージ（volume）について



■docker-compose.ymlを書く




■laravelのコンテナを立ち上げる
複数のコンテナでボリュームを共有する



■3層アーキテクチャを完成させる
複数のコンテナでネットワークを共有する



■サーバレス

https://dev.classmethod.jp/articles/cmdevio2019-container/

https://qiita.com/takanorig/items/3a3a0b43b5be5b4a124f


■必要なもの
AWS CLI
ECS CLI



