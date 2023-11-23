# Linux操作系统上连接并使用iSCSI卷

##

{% embed url="https://help.aliyun.com/zh/csg/user-guide/use-volumes-on-a-linux-ecs-instance" %}
转自阿里云
{% endembed %}

### 连接卷 <a href="#title-zsl-thq-5j8" id="title-zsl-thq-5j8"></a>

1.  执行如下命令，安装iscsi-initiator-utils。



    ```shell
    sudo yum install iscsi-initiator-utils
    ```

    如果使用的是Debian或者Ubuntu操作系统，请执行如下命令安装。

    ```shell
    sudo apt-get install open-iscsi
    ```
2.  验证iSCSI守护进程是否正在运行。

    *   如果是RHEL7，请执行如下命令：

        ```shell
        sudo service iscsid status
        ```

    如果执行以上命令，未返回running状态，则执行`sudo /etc/init.d/iscsi start`命令启动iSCSI守护进程。
3.  （可选）设置CHAP认证。

    **说明**

    如果在创建iSCSI卷时，启用了CHAP认证，则需要在高级设置对话框中设置CHAP认证信息后，才能使用iSCSI卷。

    1.  执行如下命令打开iscsid.conf配置文件。

        ```shell
        vi /etc/iscsi/iscsid.conf
        ```
    2.  找到CHAP Settings，删除相关配置项前面的注释符#，并设置用户和密码。

        * 用户为创建iSCSI卷时设置的入站CHAP用户。
        * 密码为创建iSCSI卷时设置的入站CHAP密码。


4.  发现iSCSI卷。

    *   IPv4方式执行如下命令：

        ```shell
        iscsiadm -m discovery -t st -p <目标IPv4地址>:3260
        ```



    3260为访问端口，保持不变；


5.  挂载iSCSI卷。

    *   IPv4方式执行如下命令：

        ```shell
        iscsiadm -m node -T <目标名称> -p <目标IPv4地址>:3260 -l
        ```



    目标名称为iSCSI卷的目标名称，发现iSCSI卷的命令返回中获取。

    **说明**

    由于iSCSI 协议限制，请勿将一个iSCSI卷挂载到多个Linux客户端。

### 查看卷 <a href="#title-p76-tqu-nsl" id="title-p76-tqu-nsl"></a>

1. 执行fdisk -l或lsblk命令查看iSCSI卷。

### 卸载卷 <a href="#title-ddh-2pq-dyh" id="title-ddh-2pq-dyh"></a>

当不再使用iSCSI卷时可以通过以下命令行进行卸载。

*   IPv4方式执行如下命令：

    ```shell
    iscsiadm -m node -T <目标名称> -p <目标IPv4地址>:3260 -u
    ```

