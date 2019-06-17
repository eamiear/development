# 调试

基于 VS Code调试

### 配置

打开 VS Code Debug 面板，添加配置 "Add Configuratior"， 选择 () Node.js: Attach，添加配置到 launch.json文件

```json
{
    "type": "node", 
    "request": "attach",
    "name": "Attach",
    "port": 5858
}
```

### 执行脚本

执行程序，并制定端口，端口与launch.json文件中的端口一致。

```node
node --inspect-brk=5858  ../node_modules/webpack/bin/webpack --config ./webpack.config.js

```
