<img width="660" height="105" alt="image" src="https://github.com/user-attachments/assets/7d847ab3-c5d8-407e-a9ce-bf87e76c2017" /># 第三周：企业离线环境——本地 YUM/DNF 软件源配置

## 🎯 实验背景与目标
在企业生产环境中，为了安全，服务器通常处于无外网状态（内网隔离）。本次实验模拟离线环境，通过挂载 RHEL 9 的 ISO 镜像文件，配置本地 DNF 软件源，解决离线环境下的软件安装与依赖问题。

## 🛠️ 实操步骤记录
 1. 挂载 ISO 镜像文件
将光盘设备（或本地 ISO 文件）挂载到系统的指定目录。
确认镜像文件确实在 /root 目录下，并且看准文件名
ls -lh /root/*.iso
<img width="660" height="105" alt="image" src="https://github.com/user-attachments/assets/7f8796a1-b39f-4af5-8456-10544f29e2b7" />

2.创建挂载点
mkdir -p /mnt/iso

3. 【核心命令】使用 -o loop 参数，将本地的 ISO 文件挂载到 /mnt/iso
mount -o loop /root/rhel-9.2-x86_64-dvd.iso /mnt/iso
<img width="840" height="82" alt="image" src="https://github.com/user-attachments/assets/67f947c9-7043-4c75-846a-30bb17d66a8a" />

4.验证挂载是否成功（敲完这行，屏幕上必须打印出 BaseOS 和 AppStream！）
ls /mnt/iso
<img width="887" height="117" alt="image" src="https://github.com/user-attachments/assets/64defa03-ad03-40e1-9f0a-d000205d23a6" />

5.备份原来的源（如果之前没敲过）
mkdir -p /etc/yum.repos.d/backup
mv /etc/yum.repos.d/*.repo /etc/yum.repos.d/backup/ 2>/dev/null
<img width="897" height="97" alt="image" src="https://github.com/user-attachments/assets/6ed05ce8-6dd3-419e-9409-f2cb2d5b25a1" />

6. 写入本地源配置（直接复制这一大段粘贴到终端，回车）
cat > /etc/yum.repos.d/local.repo << 'EOF'
[local-baseos]
name=Local BaseOS
baseurl=file:///mnt/iso/BaseOS
enabled=1
gpgcheck=0

[local-appstream]
name=Local AppStream
baseurl=file:///mnt/iso/AppStream
enabled=1
gpgcheck=0
EOF
<img width="776" height="288" alt="image" src="https://github.com/user-attachments/assets/0721ed8a-ad46-48a9-adce-a136f935d2b1" />

7. 清理缓存并重新生成（这步需要稍微等几秒钟）
   dnf clean all
   dnf makecache
<img width="922" height="430" alt="image" src="https://github.com/user-attachments/assets/c0e98b58-27e1-464b-9e53-78bf8f97d8a6" />

8. 安装tree 软件
   dnf install tree -y
   <img width="756" height="715" alt="image" src="https://github.com/user-attachments/assets/3891a0d2-381c-480e-9a61-5172613d4e9a" />

9.查看结果
tree /data
<img width="341" height="120" alt="image" src="https://github.com/user-attachments/assets/6fbc804c-f9ac-4e4b-aabc-0fbd52f494e0" />

“实验总结”
*“通过本次配置，不仅解决了离线服务器安装软件的问题，还成功补全了第二周因缺乏软件源导致无法安装 `tree` 工具的遗留任务。”*
