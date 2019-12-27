### GO环境配置
使用到了gomod管理依赖包，需要Go的版本大于1.12

![](http://img.hixuxu.com/2019-11-26-074450.png)

设置GOPATH和GOPROXY,并打开GO111MODULE
```
# 启用 Go Modules 功能
export GO111MODULE=on
# 配置 GOPROXY 环境变量
export GOPROXY=https://goproxy.io

go mod init
```
### 安装kubebuilder
```
mkdir -p  $GOPATH/src/hiningmeng.cn && cd $GOPATH/src/hiningmeng.cn
git clone https://github.com/kubernetes-sigs/kubebuilder
cd kubebuilder
make build
cp bin/kubebuilder $GOPATH/bin
```

### 创建Project
```
# export GO111MODULE=on

kubebuilder init --domain=hiningmeng.cn
```
### 创建API
```
kubebuilder create api --group k8s --version v1 --kind AppService
```
创建出Resource和Controller，选择Y即可
![](http://img.hixuxu.com/2019-11-26-073848.png)

其中主要的两个文件如下：
![](http://img.hixuxu.com/2019-11-26-074021.png)

### 开始开发一个CRD
这个CRD功能主要为开发一个抽象的AppService对象，能够控住Depolyment和Service，并且能够暴露Nodeport端口被访问。

![](http://img.hixuxu.com/2019-11-26-074916.png)
#### 创建结构体
结构体的定义在appservice_types.go文件中，需要修改的就是AppServiceSpec的结构体。



