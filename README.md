### Ansible 面板

### 项目简介
本项目是一个基于 Flask 和 Ansible 实现的主机管理面板，支持批量添加主机、批量执行命令等功能。通过网页界面，用户可以方便地管理多台主机，并查看执行日志。


### 功能介绍
1. **主机管理**：
   - 批量添加主机：支持一次性添加多台主机，每行一个，格式为 `编号 地址 用户名 端口 密码`。
   - 删除主机：可以删除不再需要管理的主机。

2. **命令执行**：
   - 向选定的主机或所有主机发送命令，并在页面上实时显示执行日志。

4. **待实现的功能**：
   - 交互式执行命令


### 使用方法
1. **Docker部署**：

```
docker run -d \
  --name ansible \
  -p 5000:5000 \
  -e ANSIBLE_HOST_KEY_CHECKING=False \
  -e ADMIN_USERNAME=admin123 \
  -e ADMIN_PASSWORD=admin123 \
  -v ./ansible:/app/db \
  ghcr.io/sky22333/ansible
```

2. **访问面板**：
   - 打开浏览器，输入`http://IP:5000`访问面板<br>默认用户名`admin123`，默认密码`admin123`<br>通过环境变量修改用户名和密码。

3. **添加主机**：
   - 在主机管理页面，使用批量添加功能，输入多台主机信息，点击“添加主机”按钮。

4. **执行命令**：
   - 在命令执行页面，输入要执行的命令，选择目标主机（单个或多个），点击`发送到选中主机`或`发送到所有主机`。

5. **命令说明**：
   - 暂不支持交互式执行命令
     
| **支持的命令**         | **示例**                                           | **说明**                           |
|---------------------|--------------------------------------------------|----------------------------------|
| **文件操作命令**    | `ls`, `cp`, `mv`, `rm`                          | 用于列出、复制、移动和删除文件       |
| **脚本执行**        | `./script.sh`                                  | 执行指定的Shell脚本             |
| **远程脚本**        |  `bash <(wget -qO- https://github.com/xx/shell/raw/main/xx.sh)`   | 执行指定的远程shell脚本              |
| **管道和重定向**    | `echo "Hello, World!"  grep "Hello" > output.txt`  | 使用管道和重定向进行数据处理        |
| **条件和循环**      | `if [ -f "file.txt" ]; then echo "File exists"; fi` | 使用条件语句执行相应操作           |
| **复杂命令**        | `cd /path/to/directory; ./run_script.sh`       | 组合多个命令，使用分号分隔          |
| **环境变量**        | `VAR=value your_command`                         | 设置环境变量并执行命令              |


6. **日志返回码**：

| 返回码 | 含义                         |
| ------ | ---------------------------- |
| 0      | 执行成功                         |
| 1      | 一般错误                     |
| 2      | 误用的命令                   |
| 126    | 命令无法执行                 |
| 127    | 命令未找到                   |
| 128    | 无效的退出状态               |
| 130    | 脚本被用户中断               |
| 137    | 进程被杀死                   |
| 255    | 退出状态未定义               |



7. **数据库说明**：
   - 项目使用 SQLite 数据库存储主机信息和命令日志，数据库文件默认存储在 `db/ansible.db`，可保留主机信息迁移。

