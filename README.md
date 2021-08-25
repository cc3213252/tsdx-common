# React私服库

* 项目创建
```bash
npx tsdx create tsdx-common
```

* 安装库
```bash
npm i
cd example
npm i
npm start
```

* 使用
库修改后，example需要重新启动才能生效  

## 私服相关

* 安装： docker run -tid -p 8081:8081 --privileged=true -v /Users/cyd/data/nexus-data:/var/nexus-data docker.io/sonatype/nexus3  
* [nexus上npm私服配置](https://www.cnblogs.com/caonw/p/13212226.html)  
* 注意还需要额外配置一下Security-Realms，把npm Bearer Token Realm添加进去  
* 需要发布的库上配置
```json
  "publishConfig": { // 将发布的仓库指定到私有仓库
    "registry": "http://localhost:8081/repository/npm-hosted/"
  },
```
* 发布命令如下
```bash
npm version patch   // 普通业务代码更新Patch即可
npm run build
npm adduser --registry=http://localhost:8081/repository/npm-hosted/
npm publish
```
* [npm registry管理工具nrm](https://www.cnblogs.com/sghy/p/6840925.html)，正常不需使用这个工具    

## 测试私服库

* npx create-react-app react-demo  
* 增加.npmrc文件，配置npm源  
```bash
registry=http://localhost:8081/repository/npm-group/
```
* npm login -d registry=http://localhost:8081/repository/npm-group/
* npm add tsdx-common --save
* 修改文件后，需要重新执行登陆，重启服务才生效  
  
## 碰到问题

*  /Users/cyd/Desktop/study/react/tsdx/tsdx-common/example/index.tsx: Invalid Version: undefined  
example中parcel版本问题，改为"parcel": "1.12.3", 即可  

无法使用npm login -d registry=http://localhost:8081/repository/npm-group/登陆，报405，使用npm adduser命令
后就ok了  

不要在主目录下创建工程测试，会碰到库依赖问题，换个地方测试库就没问题  