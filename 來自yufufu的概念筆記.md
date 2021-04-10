# 概念

- [awesome 系列](https://github.com/veggiemonk/awesome-docker)
- [dry,ctop 好用的 cli](https://hackernoon.com/docker-cli-alternative-dry-5e0b0839b3b8)
- 要先開 鯨魚(`hyperKit` OS 之上的一層 VM) 才能 跑容器
- 以後用 alpine linux(超輕量化 OS) 來寫 dockerfile
- 可用`docker-php-ext-enable`來裝 php 擴展
- [compose to k8s](https://kubernetes.io/zh/docs/tasks/configure-pod-container/translate-compose-kubernetes/) , [cli to compose](https://composerize.com/),[走進專案,幫你產生 Dockerflie](https://github.com/cloud66-oss/starter)
- [不同 compose 溝通方案](https://ithelp.ithome.com.tw/articles/10218037), [不同 pod 溝通方案]()
- Docker 有分`早期的版本docker-io 企業版本的Docker EE`和`免費社區版本的Docker CE`
- Docker Machine 簡單來說，就是一個可以讓你快速在不同平台上建立 Docker engine 的 command tool。
- [docker statless 不儲存持久型資料,起動即用](http://www.dockerinfo.net/2227.html)
- [docker network 簡介](https://godleon.github.io/blog/Docker/docker-network-bridge/) (lo ,eth0 ,veth(虛擬網卡))
- [Traefik](https://docs.traefik.io/basics/) 幫你解掉惱人的 network
- [Weave net]() 由 weaveworks 公司开发的解决 Docker`跨主机网络`的解决方案

```
Entrypoints
a port (80, 443...)
SSL (Certificates, Keys, authentication with a client certificate signed by a trusted CA...)
redirection to another entrypoint (redirect HTTP to HTTPS)

Frontends
規則mapping表 Entrypoints ==> Backends

Backends
backend負責將來自一個或多個前端的流量負載平衡到一組http服務器。
```

- [多階段構建 multi-stage]()
- [縮小 img 的智慧](http://www.docker.org.cn/docker/176.html)
- [Supercronic](https://github.com/aptible/supercronic) 專為容器設計的 cron
- [CNI/CRI/CSI ]() container network interface
- [Helm]() 生成 (Bake) Kubernetes 部署文件

```
Helm 等同於前端開發常用的 Npm，
只不過安裝的東西不是套件而是一個運行服務Chart，
而 K8S 這邊把整包服務稱作 Chart，
事實上類似 package.json 定義出 Chart.yaml 來描述系統的架構。
```

- [惡搞/var/run/docker.sock](https://blog.fundebug.com/2017/04/17/about-docker-sock/)
- K3s == 輕量化
- 即，需要容器启动预处理的，都可以使用 `docker-entrypoint.sh` 机制
- [kubeadm 安裝好像很簡單](https://k2r2bai.com/2016/09/29/kubernetes/deploy/kubeadm/)
- EE 有的 Universal Control Plane (UCP) , Img 儲存的 Docker Trusted Registry (DTR)
- [kinD](https://kind.sigs.k8s.io/) 還看不懂
- docker stack deploy 好像會取代 docker compose

### 比較這三種 集群管理器 Container Manager

- 以複雜度和功能來看 `Cloud Foundry` > `Kubernetes(K8S)` > `Docker Swarm`
- Docker Swarm 在"一堆主機"上 啟動容器，然後型成一個叢集(Cluster)的一個工具

# 生命週期

```bash
# 一般來說
(Dockerfile) ==build=> (Image) ==create=> (deadContainer) ==start=> (aliveContainer)
(Image)rmi ==create=> (deadContainer)rm <=kill== (aliveContainer)

# 快速法
(Image) ==run=> (aliveContainer)

```

# 命令

```sh
# --- 查看 ------ images > ps -a > ps -----------------------------------------------
docker images #列出所有本機 映像檔(images)
docker ps -a #查看 容器(container) 已啟動的 + 含未啟動
docker ps #查看 容器(container) 已啟動的
docker logs 容器名稱 # 查看底下運行東西的log

# --- 使用相關 ---- run = create + start -----------------------------
# 把image拿來 建立() && 啟動() 容器
docker run -d --name 取個名字 鏡像名稱

# 把某Registry上面的img拉下來直接 onDemaon跑起
docker run -d --name 取個名字 git.XXXX.com.tw:4567/XXXXX/tf-job:master

# 進出容器
docker exec -it 容器名稱 /bin/bash # 進容器 (指令:使用/bin/bash)
exit # 從 容器 出來

# --- 終止 啟用---------------------------------
docker stop 45dfgdgs4d35f #終止
docker start 45dfgdgs4d35f #啟用

# --- 移除 ---(-f是強制的意思)--------------------------------------------------
docker rmi -f 45dfgdgs4d35f #移除 映像檔(image) or tag (docker images看到的)
docker rm -f 45dfgdgs4d35f #移除 容器(container) (docker ps -a看到的)
docker kill -f 45dfgdgs4d35f #移除 正在運行的容器 (docker ps 看到的)
docker image prune -a # 清除所有沒在用的img
docker system prune -a # 殺得什麼都不剩

# --- 把東西放到容器內 -----------------------------------------
#把東西放到 容器 內(容器ID可由 ps指令查詢)
docker cp 檔案.php 容器ID(1FS11D8F):容器內的路徑 

# --- 其他 -------------------------------------
#daemon 有點類似 進入無窮迴圈(防止關閉)
-d == 背景執行

# 服務要開機起來指令
docker run -d --restart unless-stopped -p 80:9000 realtime

# --- 加掛port,volumn,network ------------------------------------
docker run -d \
--net=host \
--expose=81 -p 81:80 \
-v ~/Git/docker專案:/var/www/docker專案 \ # Volumn
--name 容器名稱 \ # 容器名稱
git.XXXXXX.com.tw:4567/XXXXXX/img名稱 # Registry位置
```

# 版本 build 相關

```bash
# 修改img名稱 tag (容器原本只有ID)77
docker tag -it 45dfgdgs4d35f 自己命名
docker tag 映像id zero85258/gitlab_ci

### 把 容器commit 保存
docker commit 容器id 提交後的新名字
docker commit -m "提交訊息" -a "作者名稱" 45dfgdgs4d35f 名稱

### 倉庫的 pull/push
docker pull 專案
docker push 倉庫名/專案:tag版本號
```

# Dockerfile

- 有點像批次檔的概念,一口氣執行多的 docker 命令

### 如何執行

```sh
# 先touch Dockerfile #建Dockerfile檔
# cd 到存放 Dockerfile 的路徑中
# 執行 docker build 指令。

# 如此一來，不用透過人工操作，
# Docker 會自動執行 Dockerfile 裡面的步驟，幫我建立 Docker Image

# 創建映像檔
docker build .
docker build -t iMaGe名稱:tAg名稱 .
```

### 語法

```Dockerfile
FROM 來源鏡像 #就是pull下來的image

ADD #添加文件
COPY 本地文件 容器路徑 #拷貝文件

# --- RUN , CMD , ENTRYPOINT 差異---------------------
RUN 執行命令|創建新的鏡像層，RUN 經常用於安裝軟件包。
CMD 設置容器啟動 後默認執行的 命令其參數，但 CMD 能夠被 docker run 後面跟的命令行參數替換。
ENTRYPOINT 配置容器啟動時 運行的命令。


RUN apt-get install -y nginx #執行CMD命令(會有layer)
CMD ["npm","start","--production"] #執行CMD命令
ENTRYPOINT ["/usr/sbin/nginx","-g","daemon off;"] #在前台執行,而不是daemon執行

# ----------------------------------------------------
EXPOSE 80 443 #暴露端口(假如東西是伺服器)
VOLUME mount point

WORKDIR 一進入容器的初始路徑
MAINTAINER 維護者
ENV 設定環境變量

USER 指定用戶id


# --- 實際範例 --------------------------------------------
FROM ubuntu
MAINTAINER 維護者
```

# Volume

```sh
#掛載(-v)
docker run -d --name 自己命名 -v 容器內部地址

#檢查 容器狀態
docker inspect 容器名

#   ($PWD是指當前目錄 , -d是指daemon)
docker run -p 本機端口:容器端口 -d -v 本機目錄:容器目錄 nginx
docker run -p 80:80 -d -v $PWD/html:/usr/share/nginx/html nginx

#從 B容器 加載東西 到 A容器(--volumes-from)
docker run --volumes-from B容器 A容器 /bin/bash
```

---

# 多容器 docker-compose

```bash
-d #背景執行

docker-compose up -d mysql redis nginx # 啟動相關容器
docker-compose ps # 查看容器進程
docker-compose exec 容器名字 sh # 進入相關容器
docker-compose up -d mysql redis nginx＃
docker-compose up -d mysql redis nginx

# 出問題的話,先暫停了它
docker-compose stop

# 設置完docker-compose.yml檔 不需重新build 只要下
docker-compose up -d --force-recreate
```

# cron 方案(supercronic)

```bash
# install
export SUPERCRONIC_URL=https://github.com/aptible/supercronic/releases/download/v0.1.8/supercronic-linux-amd64
export SUPERCRONIC=supercronic-linux-amd64
export SUPERCRONIC_SHA1SUM=be43e64c45acd6ec4fce5831e03759c89676a0ea

curl -fsSLO "$SUPERCRONIC_URL" && echo "${SUPERCRONIC_SHA1SUM} ${SUPERCRONIC}" | sha1sum -c - && chmod +x "$SUPERCRONIC" && mv "$SUPERCRONIC" "/usr/local/bin/${SUPERCRONIC}" && ln -s "/usr/local/bin/${SUPERCRONIC}" /usr/local/bin/supercronic

# usage
supercronic /專案路徑/crontab
```

# 特別個案

```bash
# CentOS 建造容器時要 下特別參數
docker run -d -e "container=docker" --privileged=true -v /sys/fs/cgroup:/sys/fs/cgroup 5a4b4c4cbcc2 /usr/sbin/init
```

# docker-compose.yml 常見

```yaml
version: "3"

services:
nginx:
image: nginx
volumes:
- "./available-sites/:/etc/nginx/conf.d/:ro"
- "./dmp:/code/ats"
- "./tf:/code/tf"
- "./艾tm.testing.local:/code/atm.testing.local"
ports:
- "80:80"
mongo:
image: "mongo:3.4"
redis:
image: redis
艾tm:
build:
context: ./atm/
volumes:
- "./atm:/app/"
depends_on:
- mongo
- redis
- nginx
艾_db:
image: mysql:5.6
environment:
- MYSQL_ALLOW_EMPTY_PASSWORD=true
- MYSQL_DATABASE=ats
ports:
- "3306:3306"
艾:
build:
context: ./ats/
volumes:
- "./ats:/code/ats"
depends_on:
- ats_db
- nginx
tf_db:
image: mysql:5.6
environment:
- MYSQL_ALLOW_EMPTY_PASSWORD=true
- MYSQL_DATABASE=tf
tf:
build:
context: ./tf/
volumes:
- "./tf:/code/tf"
depends_on:
- tf_db
- nginx
realtime:
build:
context: ./realtime/
depends_on:
- mongo
- redis
```

# 情境

```bash
# 動完dockerfile,只更動指定服務(就不用全數重跑)
docker-compose build tf
```

# 自動化方向

### env

可以用`docker --env FILENAME` or `docker-compose.yml 的 env-file` 解掉

### Dockerfile 統一復用

- 可下條件 makefile 才達成

### `storage`或是`特定檔案` 沒辦法跟著專案 (理想上 container 重啟,死掉,版控切換,這些東西都不能遺失,所以該設計成 stateless,東西存在 nas 之類的)

- ex:像是素材(CDN??),log(elk 方案),key(aws param store),client_secret.json,

# 直接把 img 當作執行檔(不當 service)

```Dockerfile
# Dockerfile
FROM alpine
RUN apk add --no-cache curl
ENTRYPOINT [ "curl", "-s", "https://ip.cn" ]
```

```sh
docker build -t alpine-fu . # 建構
docker run --rm alpine-fu # 當作執行檔 回傳 {"ip": "111.111.111.111", "country": "", "city": ""}
```
