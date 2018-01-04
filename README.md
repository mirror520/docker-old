# docker
一些用到的Docker配置

## 建立Docker network
- 臺中市政府各機關連線內部系統時，會使用虛擬IP連線，但可能會造成IP衝突，所以建議創一個Network bridge，放到不會衝突的虛擬IP。
- sudo docker network create --driver bridge --subnet 10.77.0.0/16 tccg-network

## 建立Let's Encrypt Volume，並取得伺服器SSL憑證
- sudo docker volume create letsencrypt
- sudo docker run --rm -it -p 443:443 -v letsencrypt:/etc/letsencrypt certbot/certbot certonly
- select Standalone

## 蒐集Docker logs可透過gelf日誌引擎，透過gelf via UDP送到E.L.K
### 先啟動ELK
- cd ~/docker/elk
- sudo docker-compose up -d
### 再啟動Server
- cd ~/docker
- sudo docker-compose up -d

## 透過vnc連到Desktop Container，再透過內網連到phpmyadmin或kibana等
### 平常啟動後關掉Container
- sudo docker stop vnc
### 需要連到phpmyadmin或kibana等時，開啟Container
- sudo docker restart vnc
### 透過VNC Client連到Desktop Container
- 開啟後進入瀏覽器
- 網址輸入：http://phpmyadmin/
- 網址輸入：http://kibana:5601/

## Angular-Cli Container
### 建立Docker Image
- cd docker/angular
- sudo docker build -t ar0660/angular .
### Angular-Cli操作
- sudo docker run --rm -v ~/workspace/mis-secretariat:/app ar0660/angular ng [CMD]...
### yarn操作
- sudo docker run --rm -v ~/workspace/mis-secretariat:/app ar0660/angular yarn [CMD]...
### 產生ng serve Container，一直掛載在伺服器上
- Dockerfile中，需把--public-host參數，指向domain name（含port）
- sudo docker run --name angular **-d** -p 80:4200 -v ~/workspace/mis-secretariat:/app ar0660/angular
- sudo docker logs -f angular

## c9sdk Container
### 建立Docker Image
- cd docker/c9sdk
- sudo docker build -t ar0660/c9sdk .
### 設定帳號密
- 變更Dockerfile內CMD的--auth參數
### 產生Docker Container
- sudo docker run --name c9sdk -d -p 3000:3000 -v ~/workspace/api:/workspace ar0660/c9sdk
- sudo docker logs -f c9sdk
