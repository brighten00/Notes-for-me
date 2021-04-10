# Linux 生態

- Open Source Software == OSS
- Free Open Source Software == FOSS
- EPEL 計畫
- EPEL 源,REMI 源
- GNU 工具鍊
- gcc 可以用來`編譯`C 和 C++：但是 gcc`只能連結`C 庫，不能連結 C++庫；
- g++ 可以連結 C++庫，但是它是通過調用 gcc 來編譯，因此：它也可以編譯 C 和 C++，但它能編譯的條件是要先存在 gcc。
- [各種領域的優秀開源軟體](https://www.linuxlinks.com/links/Software/)

# Make

- [常用的指令](https://blog.csdn.net/LEON1741/article/details/54846170)
- `makefile`文件就是編譯程序用的腳本

# devel

```sh
# 包主要是供開發用，至少包括以下2個東西:
1. 頭文件
2. 鏈接庫
有的還含有開發文檔或演示代碼。
# 以 glib 和 glib-devel 為例:
如果你安裝基於 glib 開發的程序，只需要安裝 glib 包就行了。
但是如果你要編譯使用了 glib 的源代碼，則需要安裝 glib-devel。
```

# rpm

```
SRPM源碼包 程式效率高,因為沒經過編譯,程式碼還可以自己亂改,但安裝很久(要經過編譯)
檔名格式xxx.src.rpm
腳本安裝包 = shell腳本 +SRPM(可以腳本設定好一次安裝)

RPM安裝包 可直接安裝,不需編譯,原本就是2進制包,(有依賴性!!!!!)
檔名格式xxx.rpm

distribution 代表 軟體管理機制 使用指令 線上升級機制(指令)
Red Hat/Fedora RPM rpm, rpmbuild YUM (yum)
Debian/Ubuntu DPKG dpkg APT (apt-get)

RPM安裝包命名規則 :
包名-1.1.1(版本)-1發佈次數.el6.centos(linux平台).i686(硬體平台).rpm
```

---

# PHP 生態

# PEAR

PHP 擴充功能的函式庫集合
裡面的功能被包裝成 一個一個的 Package

- Pear 是 PHP 的上層擴展(php 寫的)
- Pecl 是 PHP 的底層擴展(C 寫的)。 (需要把.so 檔加入 ini)
- phpize 是用來`擴展`(這個動詞具體是啥意思)php 擴展模塊的，通過 phpize 可以建立 php 的外掛模塊
- `autoconf` 及 `automake` 這兩套工具來協助我們自動產生 Makefile 文件，並且讓開發出來的軟件可以像大多數源碼包那樣，只需`"./configure", "make","make install"`就可以把程序安裝到系統中
- [gcc g++](https://github.com/zero85258/MyNOTE/blob/69df3a2ad73795853a0ba1e7705f9bbd177f1198/%E7%B6%B2%E8%B7%AF%E6%B4%A8%E9%AB%98%E6%89%8B/Back-End%E5%BE%8C%E7%AB%AF%20-%20Linux%E7%94%9F%E6%85%8B.md)

```bash
wget https://pecl.php.net/get/yaml-1.3.0.tgz #下載
tar -xzvf yaml-1.3.0.tgz #解壓縮
cd yaml-1.3.0 #進資料夾
phpize #編譯
./configure # 一般用来生成 Makefile。它会检测你是不是有CC或GCC，并不是需要CC或GCC，它是个shell脚本。
make # 是用来编译的，它从Makefile中读取指令，然后编译。 (有時要用make CFLAGS="-Wno-error"來填坑)
make install # 是用来安装的，它也从Makefile中读取指令，安装到指定的位置。
```

- php-devel 是擴展包
- php-pear
- go-pear 安裝 PEAR 用的

# 在 docker 安裝環境

```bash
# 安裝pear ext
docker-php-ext-install pdo pdo_mysql mbstring json zip mcrypt soap exif

# 安裝pecl ext
apk add $PHPIZE_DEPS # phpize
pecl install mongodb # 安裝
docker-php-ext-enable mongodb xdebug #(等於去ini加extension=mongodb.so)
```

# 套件&擴展

- `Whoops` 就是 laravel 的 debug 畫面
- `Monolog` PHP 最流行的日志庫
- `Phar`(PHP Archive)它是 PHP 的 extension，就像是 Java 的 jar 一樣可以用來打包程式碼，可讓專案易於散佈並安裝使用
- `Swoole` PHP 的異步網絡通信引擎(常跟 nodeJs 比較)
- `php ob函式`

### composer.json composer.lock

```json
{
  "require": {
    "google/apiclient": "1.0.*@beta",
    "guzzlehttp/guzzle": "~4.0",
    "doctrine/dbal": "~2.4"
  },

  "autoload": {
    "classmap": ["my_library"]
  }
}
```

# require 'vendor/autoload.php' 就可以開始;

---

# Java 生態

- 別再他媽寫 Java 8 以下的(感覺就像 php5.6)
- Java SE 可以分作四個主要的部份：JVM、JRE、JDK 與 Java
- jre == java 執行環境（Java Runtime Environment，簡稱 JRE），包含了 jvm
- jar == java tar 包含所有必需的依賴項，類和資源的可`執行檔`
- war == 可以 綁到 webServer 上的 jar
- jit == 編譯器
- opensdk/JDK (包含 jar 等等...)
- tomcat
- Servlet == java 平臺上的 CGI 技術
- `build.gradle` == `Pom.xml` == `composer.json`
- `gradlew`是对 gradle 的包装和配置, gradlew == gradle Wrapper
- Spring-core: 最主要的模組,是 Spring 核心
- Spirng-Context: 提供 DI 依賴注入 功能
- JMS==協議,ActiveMQ==實現
- mybatis 感覺就是 laravel query builder
- \*.properties 有點像是 環境變數,設定檔
- [spring 專案用產生的吧](https://start.spring.io/)
- EJB(Enterprise JavaBeans)定義了一組可重用的元件：開發人員可以利用這些元件，像搭積木一樣建立分散式應用。
- sdkman 為安裝、切換、列出和移除 SDK 提供了一個簡便的方式,它允許開發者為 JVM 安裝不同的 SDK
- Java 中的 Stream 是對`函數式編程`中 pipeline 的實現 Stream 函數式庫
- 現代 java == 函數式編程，lambda 表達式，stream 處理 api，初始化技術(模塊系統)，Rx 響應式編程(Spring WebFlux 編寫響應式 Rest API)，局部變量類型變量；

# 執行 jar 檔

```sh
# docker
docker run --rm -it -v "$PWD":/usr/src/myapp -w /usr/src/myapp openjdk:8 bash # 可用於直接執行jar
docker run --rm -it -p 8080:8081 -v "$PWD":/var/lib/jetty/webapps -u=root jetty bash # 可用於http
docker run --rm -u gradle -v "$PWD":/home/gradle/project -w /home/gradle/project gradle gradle <gradle-task> # 可用於快速跑task,CI整合

# 編譯
gradle build

# 動態模式run
gradle bootrun

# maven
./mvnw clean package # 建構jar檔
java -jar build/libs/gs-accessing-mongodb-data-rest-0.1.0.jar # 執行
./mvnw spring-boot:run # 動態模式run
```

```sh
# mac下執行
./JavaApplicationStub
```

# 產生專案

```sh
gradle init # 產生gradle周邊
gradle init --type java-application
gradle tasks --all
```

# spring 全家桶

```
1.spring framework
包括了ioc依賴注入，Context上下文、bean管理、springmvc等眾多功能模塊，

2.spring boot
它的目標是簡化Spring應用和服務的創建、開發與部署，簡化了配置文件，
使用嵌入式web伺服器，含有諸多開箱即用的微服務功能，可以和spring cloud聯合部署。
Spring Boot的核心思想是約定大於配置，應用只需要很少的配置即可，簡化了應用開發模式。

3.Spring Data
是一個數據訪問及操作的工具集，封裝了多種數據源的操作能力，包括：jdbc、Redis、MongoDB等。

4.Spring Cloud(微服務,分布式系統 全家桶)
集成了zuul網關、服務發現、配置管理、消息總線、負載均衡、hystrix斷路器、數據監控等各種服務治理能力。
sleuth提供了全鏈路追蹤能力，config組件提供了動態配置能力，
bus組件支持使用RabbitMQ、kafka、Activemq等消息隊列，

5. Spring Security
主要用於快速構建安全的應用程式和服務，在Spring Boot的基礎上oauth2,JWT,SSO
```

# lifeCycle Spring

1. 用戶發送請求 到 DispatcherServlet 控制器
2. DefaultAnnotationHandlerMapping 把接收到的 URL 對應到相對的 DefaultAnnotationHandlerAdapter
3. DefaultAnnotationHandlerAdapter
4. SeckillController
5. ModelAndView/Seckill/List
6. InternalResourceViewResolver
7. Model
8. list.jsp

# gradle >>> maven(醜) == Ant(醜)

```sh
# install sdkman
curl -s "https://get.sdkman.io" | bash
source "/Users/zero85258/.sdkman/bin/sdkman-init.sh"
sdk version

# install gradle
wget https://services.gradle.org/distributions/gradle-6.3-bin.zip -P /tmp
unzip -d /opt/gradle /tmp/gradle-*.zip
# vim ~/.bashrc && source ~/.bashrc
export GRADLE_HOME=/opt/gradle/gradle-6.3
export PATH=${GRADLE_HOME}/bin:${PATH}

gradle -v

# install maven
wget http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.0.5/binaries/apache-maven-3.0.5-bin.tar.gz
tar xvf apache-maven-3.0.5-bin.tar.gz
mv apache-maven-3.0.5 /usr/local/apache-maven
rm apache-maven-3.0.5-bin.tar.gz

# Next add the env variables to your ~/.bashrc file
export M2_HOME=/usr/local/apache-maven
export M2=$M2_HOME/bin
export PATH=$M2:$PATH

source ~/.bashrc

mvn -version
```

# 坑

```sh
# mac
export JAVA_HOME=/Library/Java/Home
```

```sh
# 查看有哪些版本 jdk
ls /Library/Java/JavaVirtualMachines

# 使用jdk8 (pentaho)
export JAVA_HOME=/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home

# 使用jdk14
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-14.0.1.jdk/Contents/Home

# 使用jdk11 (Grail)
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home

# 執行pdi spoon
.~/Downloads/data-integration/Data Integration.app/Contents/MacOS/JavaApplicationStub
```

# grail 採坑紀錄

```sh
./gradlew clean assemble
less build/stacktrace.log
grails run-app
domain-class == enetity
./grailsw console
grails run-app -Dgrails.env=cigna
```

---

# Python 生態

- [awesome 系列](https://github.com/vinta/awesome-python)
- [專門找 pkg 的網站 pypi](https://pypi.org/)
- Django (ROR 系列)
- Flask (微框架)
- [RxPY](https://github.com/ReactiveX/RxPY) 響應式編程 pkg
- Tornado (寫異步方案的？)
- NUMpy 多維資料分析
- BeautifulSoup4 爬蟲
- jieba 中文斷詞
- [monpa](https://github.com/monpa-team/monpa?fbclid=IwAR098lsbve8xTf5G6iHJtZCF6aScNM06TVnt5Nn6HWABuwP5wk4708P4I3w) 台灣非常之優秀的段詞
- [scikit-learn](https://scikit-learn.org/stable/)
- [coursera](https://www.coursera.org/learn/neural-networks-deep-learning/home/welcome) AI 旁聽好棒棒
- [pandas]() excel
- [Matplotlib 套件的 pyplot]() 資料視覺化的基石
- [package 結構的絕佳典範](https://github.com/aws/aws-cli/tree/develop/awscli)
- 使用 `pipenv + Pipfile` 別在他媽用 requirement.txt 了
- 歷史演進 pip > pipenv > poetry
- Conda 是套件管理系統，也可用來建立虛擬環境，不過因為 Anaconda (感覺比較偏統計)

### 消化中

```
For applications that are deployed or distributed in installers, I just use Pipfile.
For applications that are distributed as packages with setup.py, I put all my dependencies in install_requires.
Then I make my Pipfile depend on setup.py by running pipenv install '-e .'.
[Update 2019-08-23] I keep the dev packages in Pipfile nowadays, only the runtime dependencies get to live in setup.py.
```

```sh
# python3.7 -c "import sysconfig; print(sysconfig.get_path('purelib'))" # 取得site-packages path
export PYTHONPATH=$PYTHONPATH:/usr/local/Cellar/opencv/3.4.5/lib/python3.7/site-packages
```

# offline install

```sh
virtualenv -p $(python3.7) venv/ # 產生env環境
pip download -r requirements.txt -d wheelhouse # export pipPkgBundle
pip install -r wheelhouse/requirements.txt --no-index --find-links wheelhouse # import pipPkgBundle
```

# 坑

```py
ImportError: cannot import name # 循環載入 https://zhuanlan.zhihu.com/p/74018704
Package(一堆.py) ==__init__=> module/class > function
```

---

# JS 生態

- [moment 好用的時間]()
- [lodash]()
- [NodeJS 用的 JobQueue Kue](https://github.com/Automattic/kue)
- [facebook/flux](https://github.com/facebook/flux)
- [RxJS]() 未來幾年內會非常紅的 Library，RxJS 提供了一套完整的非同步解決方案，讓我們在面對各種非同步行為，不管是 Event, AJAX, 還是 Animation 等，我們都可以使用相同的 API (Application Programming Interface) 做開發(可以把 RxJS 想成處理 非同步行為 的 Lodash)
- [cropper]()
- [tiny_mce]()
- [CKEditor]()
- [簡單易懂的爬蟲](https://andy6804tw.github.io/2018/02/11/nodejs-crawler/)

# gulp grunt webpack 等等等

- 任務管理器 grunt > gulp
- 模塊打包加載工具 webpack

# NodeJS 相關

[Node Stream](https://www.eebreakdown.com/2016/10/nodejs-streams.html)

# 潮物

- [hen 潮的 chart](https://nivo.rocks/choropleth/)
- [lottie](https://airbnb.io/lottie/#/community-showcase)

# package.json

```json
{
"name": "analytics",
"version": "1.0.0",
"description": "",
"main": "index.js",
"scripts": {
"test:serve": "serve ./test",
"start": "nodemon start ./server/server.js",
"build": "webpack",
"build:production": "webpack -p"
},
"author": "",
"license": "ISC",
"dependencies": {
"gagagag": "git+ssh://git@git.gag.com.tw:gagagag/gagagag.git",
"bluebird": "^3.5.3",
"body-parser": "^1.17.1",
"ua-parser-js": "^0.7.12",
"cookie-parser": "^1.4.3",
"compression": "^1.6.2",
"cors": "^2.8.3",
"ejs": "^2.5.6",
"express": "^4.15.2",
"fingerprintjs2": "^2.0.6",
"geo-from-ip": "^1.1.2",
"htmlencode": "0.0.4",
"isbot": "^2.1.0",
"lodash": "^4.17.10",
"mmdb-reader": "^1.1.0",
"mongodb": "^2.2.26",
"mongoose": "^5.3.16",
"mongoose-float": "^1.0.4",
"mysql": "^2.13.0",
"node-unique-array": "0.0.6",
"pluck": "0.0.4",
"redis": "^2.7.1",
"request": "^2.81.0",
"uglify-js": "^3.0.3",
"uuid": "^3.0.1",
"winston": "^2.3.1"
},
"devDependencies": {
"babel-core": "^6.2
```
