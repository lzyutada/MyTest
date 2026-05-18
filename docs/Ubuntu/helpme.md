# Ubuntu help

## 将用户加入 sudo 组
```
# 将用户追加到系统的 sudo 用户组中
sudo usermod -aG sudo lzyutada
```

## 配置 sudo 执行命令时免密
```
# 打开免密配置文件：
sudo visudo -f /etc/sudoers.d/lzyutada

# 写入免密规则
## 在打开的空白编辑器中，输入以下整行内容
lzyutada ALL=(ALL:ALL) NOPASSWD: ALL

# 验证是否生效
su - lzyutada

```
