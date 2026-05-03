## 添加飞书渠道失败

* ver 2026.04.29
  * openclaw channels add
    * 选择飞书但是添加失败，提示缺少module(qrcode)
    * 解决办法：强制在报错目录重新安装并生成 lock 文件

```
cd /home/lzyutada/.openclaw/plugin-runtime-deps/openclaw-2026.4.29-4e67f35c3cfc/

# 强制初始化并安装

npm init -y

npm install qrcode --save
```
