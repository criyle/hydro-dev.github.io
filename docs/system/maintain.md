# 维护

## PM2

使用一键安装脚本安装的 Hydro 使用 PM2 对进程进行管理。

### 进程名称

可以通过下面的指令查看当前 PM2 正在管理的所有进程。

```sh
pm2 ls
```

一键安装脚本默认会创建下面几个进程：

- `hydrooj`： Hydro 主进程
- `hydro-sandbox`： Hydro 评测沙箱
- `mongodb`： MongoDB 数据库

后文的指令中将用 `<name>` 替代此处的进程名称，用 `<id>` 替代进程 ID（进程 ID 可通过 `pm2 ls` 查看）。（尖括号同样需要替换）

### PM2 基本指令

```sh
pm2 start <name> # 启动进程
pm2 stop <name> # 关闭进程
pm2 restart <name> # 重启进程
pm2 del <name> # 删除进程
pm2 log <name> # 查看进程日志
pm2 log <name> --lines=100 # 查看该进程的后 100 行日志
pm2 start "<command>" --name <name> # 创建名为 <name> 的进程，进程执行内容为 <command>
pm2 attach <id> # 与进程交互
pm2 save # 保存对 PM2 进行的修改（在添加、修改、删除进程后需要执行该指令）
```

Hydro 主进程同样支持多进程启动。

:::warning
请不要盲目使用多进程启动 Hydro，在低端设备上会降低性能且成倍提高内存占用。
:::

```sh
pm2 start hydrooj -i <n> # 以 n 进程启动 Hydro 主进程
```

## 更新

Hydro 系统会不定期发布更新，可以使用下面的命令获取更新。

```sh
yarn global upgrade-interactive --latest # 在交互式界面中选择想要更新的组件
pm2 restart hydrooj # 更新完后需重启 hydrooj
```