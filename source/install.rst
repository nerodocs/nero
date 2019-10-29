安装各种软件
================================

Nodejs
--------------------------

NodeJS 13.x

.. code-block:: bash:

    curl -sL https://rpm.nodesource.com/setup_13.x | bash -

`NodeJs安装`_

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

Mysql
----------------------------

`Mysql用户手册`_


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

Nginx
---------------------------

上传文件大小
``````````````````````

在nginx.conf中增加一句:

.. code-block:: bash:
    client_max_body_size 30m;

一般配置
````````````````````````

.. code-block:: bash:

    server  {
        listen          80;
        server_name     nero.readthedocs.io;
        rewrite    ^ https://nero.readthedocs.io$request_uri? permanent;
    }

    server {
        listen       443 ssl;
        server_name  nero.readthedocs.io;
        ssl_certificate nero.readthedocs.io.crt;
        ssl_certificate_key nero.readthedocs.io.key;
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        #charset koi8-r;
        access_log  /var/log/nginx/nero.readthedocs.io.access.log  main;
        error_log  /var/log/nginx/nero.readthedocs.io.error.log  error;

        location /{
            proxy_pass http://app_server/;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-Port $server_port;
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_connect_timeout 90;
            add_header Access-Control-Allow-Origin "$http_origin";
            add_header Access-Control-Allow-Methods 'GET, POST, PUT, DELETE, OPTIONS';
            add_header Access-Control-Allow-Credentials 'true';
            add_header Access-Control-Allow-Headers 'Accept,token, Authorization,DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,user';
            if ($request_method = 'OPTIONS') {
                add_header 'Access-Control-Allow-Origin' "$http_origin";
                add_header 'Access-Control-Max-Age' 1728000;
                add_header 'Access-Control-Allow-Credentials' 'true';
                add_header 'Access-Control-Allow-Methods' 'GET, POST, DELETE, PUT, OPTIONS';
                add_header 'Access-Control-Allow-Headers' 'JSESSIONID_AGENT,Accept,token, Authorization,DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,user';
                add_header 'Content-Type' 'text/plain charset=UTF-8';
                add_header 'Content-Length' 0;
                return 200;
            }

        }
    }

请求头中有下划线
`````````````````````````

在nginx.conf中增加一句:

.. code-block:: bash:

    underscores_in_headers on;

Websocket配置
```````````````````

.. code-block:: bash:

    server  {
        listen         221;
        server_name    192.168.0.123;

        location / {
            proxy_pass              http://127.0.0.1:8083;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }

        error_log           /var/log/nginx/ws_route_error.log;
        access_log          /var/log/nginx/ws_access.log main;
    }



.. _NodeJs安装: https://github.com/nodesource/distributions#debmanual
.. _MongoDB安装文档: https://docs.mongodb.com/manual/administration/install-community/
.. _MongoDB配置文档: https://docs.mongodb.com/manual/reference/configuration-options/
.. _Mysql用户手册: https://dev.mysql.com/doc/