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

## 碰到问题

🚨  /Users/cyd/Desktop/study/react/tsdx/tsdx-common/example/index.tsx: Invalid Version: undefined  
example中parcel版本问题，改为"parcel": "1.12.3", 即可  

无法使用npm login -d registry=http://localhost:8081/repository/npm-group/登陆，报405，暂时用npm adduser登陆  