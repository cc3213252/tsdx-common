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

## 碰到问题

🚨  /Users/cyd/Desktop/study/react/tsdx/tsdx-common/example/index.tsx: Invalid Version: undefined  
example中parcel版本问题，改为"parcel": "1.12.3", 即可  
