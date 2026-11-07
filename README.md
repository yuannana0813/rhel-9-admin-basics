# rhel-9-admin-basics
My first RHEL 9 basic administration practice.（我的第一个 RHEL 9 基础运维实践）
这是我的 RHEL 9 基础运维实践项目，用于记录每周的学习进度与实操结果。

## 第一周：环境搭建与远程连接

**目标**：使用 VMware 安装 RHEL 9.2 并完成 SSH 远程连接。
### 实操步骤记录

#### 步骤 1：在 VMware 中创建虚拟机
1. 打开 VMware，点击“创建新的虚拟机”。
2. 选择“典型（推荐）”，点击下一步。
3. 选择“安装程序光盘映像文件(iso)”，浏览并选中下载好的 `rhel-9.2-x86_64-dvd.iso`。
4. 客户机操作系统选择 **Linux**，版本选择 **Red Hat Enterprise Linux 9 64位**。
5. 虚拟机名称填写 `RHEL-9-Lab`，位置选择一个磁盘空间充足的盘（建议非 C 盘）。
6. 磁盘大小默认 20GB 即可，选择“将虚拟磁盘拆分成多个文件”。
7. 点击“自定义硬件”：
   - **内存**：建议分配 2GB (2048MB) 或以上。
   - **处理器**：1 个处理器，2 个核心即可。
   - **网络适配器**：**关键！** 选择 **NAT 模式**（这样虚拟机就能自动共享主机的网络上网）。
8. 点击“完成”，开启虚拟机。
<img width="522" height="285" alt="image" src="https://github.com/user-attachments/assets/4c9395a7-5ab7-4301-ac22-57a7575649b2" />

#### 步骤 2：安装 RHEL 9.2 系统
1. 虚拟机启动后，使用键盘上下键选择第一项 `Install Red Hat Enterprise Linux 9.2`，按回车。
2. 选择语言：简体中文（或 English），点击“继续”。
3. **安装信息摘要界面**（关键步骤）：
   - **软件选择**：选择 **“最小安装” (Minimal Install)**。*（注：最小安装没有图形界面，非常适合练习纯命令行运维技术）*。
   - **安装目的地**：点击进去，直接点击左上角的“完成”即可（默认自动分区）。
   - **KDUMP**：保持默认开启。
   - **网络和主机名**：打开右上角的开关，确保处于“已连接”状态，主机名可改为 `rhel-lab.local`，点击“完成”。
   - **Root 密码**：点击进入，设置一个你记得住的密码（比如 `Root@123456`）。*注意：密码太简单需要点两次“完成”确认。*
   - **创建用户**：暂时不建，直接用 root。
4. 点击“开始安装”，等待进度条走完（大约需要 10-20 分钟）。
5. 安装完成后，点击“重启系统”。
<img width="957" height="852" alt="image" src="https://github.com/user-attachments/assets/67f1287c-d290-4dc2-adf1-cb0c3c13d49c" />

#### 步骤 3：进入系统与获取 IP 地址
1. 重启后，会看到一个黑框框，输入用户名 `root`，回车，再输入你刚才设置的密码（**输入密码时屏幕不会显示任何字符，这是正常的**，输完直接回车）。
2. 登录成功后，输入命令获取本机的 IP 地址：
   ```bash
   ip a
   <img width="850" height="357" alt="image" src="https://github.com/user-attachments/assets/e1bd7581-02db-498e-bbea-364a73a4f897" />
这是我的连接成功了
   <img width="942" height="331" alt="image" src="https://github.com/user-attachments/assets/78a844c4-0343-4e67-89a4-c7bb43fdb979" />

基础操作和创建文件
<img width="818" height="537" alt="image" src="https://github.com/user-attachments/assets/e064c613-eaef-48f5-b9a5-2cc3f36be17c" />

删除文件
<img width="632" height="237" alt="image" src="https://github.com/user-attachments/assets/6c51b0c3-862f-4562-b018-4633e0b2f127" />
