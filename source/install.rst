安装各种软件
================================

Nodejs
--------------------------

NodeJS 13.x

.. code-block:: bash:

    curl -sL https://rpm.nodesource.com/setup_13.x | bash -

`NodeJs安装`_

.. _NodeJs安装: https://github.com/nodesource/distributions#debmanual

MongoDB
--------------------------

安装MongoDB
```````````````````````
`MongoDB安装文档`_

配置MongoDB
```````````````````````

`MongoDB配置文档`_

.. code-block:: bash

    use admin;

    db.createUser({
        user: "admin",
        pwd: "passwrod",
        roles: ["readWrite","userAdminAnyDatabase", "dbAdmin"]
    });

    db.updateUser(
        "username", 
        {
            roles: [{
                    role: "readWrite",
                    db: "dbname"
                },{
                    role: "dbAdmin",
                    db: "dbname"
                }
            ]
        };
    ）

.. _MongoDB安装文档: https://docs.mongodb.com/manual/administration/install-community/
.. _MonggoDB配置文档: https://docs.mongodb.com/manual/reference/configuration-options/

Mysql
----------------------------

`Mysql用户手册`_

.. _Mysql用户手册: https://dev.mysql.com/doc/

Mysql 配置
````````````````````

.. code-block:: properties:
    
    # 字符集
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci

    # 默认引擎
    default-storage-engine = innodb

    # 时区设置
    system_time_zone = '+8:00'

Mysql 用户授权
`````````````````````

.. code-block:: bash:

    grant all privileges on *.* to 'root'@'localhost' identified by 'passwrod' with grant option;

    flush privileges;

Maven
-----------------------------

下载解压
````````````````````````

.. code-block:: bash:

    # 下载
    $ wget http://www.gtlib.gatech.edu/pub/apache/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.zip

    # 解压
    $ unzip apache-maven-3.6.2-bin.zip

配置环境变量
``````````````````

编辑 /etc/profile 文件 sudo vim /etc/profile，在文件末尾添加如下代码：

.. code-block:: bash:

    export MAVEN_HOME=/opt/apache-maven-3.6.2
    export PATH=${PATH}:${MAVEN_HOME}/bin

保存文件，并运行如下命令使环境变量生效：

.. code-block:: bash:

    $ source /etc/profile