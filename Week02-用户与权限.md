# 第二周：企业用户与权限管理模拟

基础知识：
*  `groupadd`：新建用户组（group add）。
*  `touch`：新建空文件（摸一下，文件就有了）。
*   `mkdir`：新建文件夹（make directory）。
*   `useradd`：新建用户（user add）。
*   `passwd`：给用户改密码（password）。
*   `chmod`：改文件权限（change mode）。
*   `chown`：改文件的主人（change owner）。



 🎯 实验目标
模拟企业新员工入职的 IT 运维场景，完成部门划分、账号创建、密码分配、权限控制及软件安装。

 🛠️ 实操步骤记录

任务一：创建部门（用户组）
公司新成立了两个部门：开发部（dev）和人事部（hr）。

<img width="607" height="165" alt="image" src="https://github.com/user-attachments/assets/07b29d94-c402-4116-a07c-ee7b82441875" />


任务二：创建员工账号（用户）
新来了两个员工：张三和李四。张三去开发部，李四去人事部。
 使用 `useradd -g` 将张三分配到开发部，李四分配到人事部。
useradd -g dev zhangsan
useradd -g hr lisi
并使用`id zhangsan`验证员工信息
<img width="578" height="162" alt="image" src="https://github.com/user-attachments/assets/bbaca638-a739-4049-83dd-a7d9dac27202" />

任务三：给员工设密码
1. 敲命令：`passwd zhangsan`
2. 屏幕会提示你输入新密码（比如 `Zhang123`）
3. 它会让你再输一遍确认，再盲打一次回车。看到 `passwd: all authentication tokens updated successfully.` 就成功了。
4. 同样，给李四也设个密码：`passwd lisi`。
<img width="931" height="272" alt="image" src="https://github.com/user-attachments/assets/1d74878b-dfb6-4dff-89f2-f81ca1b8f218" />

任务四：创建部门共享文件夹并分配权限（极其重要！）
开发部需要一个文件夹放代码，且**只能开发部的人看，别人不能看**。
1. 在根目录下建一个 `data` 文件夹
    mkdir /data
2. 在 `data` 里建一个开发部专属文件夹
     mkdir -p /data/dev_share （回车，-p 表示如果没有 data 文件夹就自动创建）
3. 把文件夹的主人改成 root，所属组改成 dev：`chown root:dev /data/dev_share`
4. 设置权限：`chmod 770 /data/dev_share`
   * *（解释一下：770代表 主人有全部权限(7)，同组的人有全部权限(7)，其他人没有任何权限(0)。）*
5. 敲 `ls -ld /data/dev_share` 看看结果，应该是 `drwxrwx---`。
<img width="762" height="188" alt="image" src="https://github.com/user-attachments/assets/c41bae2f-7f88-4a42-bad5-248cea324898" />
