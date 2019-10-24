安装各种软件
================================

安装Nodejs
--------------------------

NodeJS 13.x

.. code-block:: bash:

    curl -sL https://rpm.nodesource.com/setup_13.x | bash -

`NodeJs安装`_

.. _NodeJs安装: https://github.com/nodesource/distributions#debmanual

安装MongoDB
--------------------------

`MongoDB安装文档`_

.. _MongoDB安装文档: https://docs.mongodb.com/manual/administration/install-community/

Mysql
----------------------------

Mysql 用户授权
`````````````````````

.. code-block:: bash:

    grant all privileges on *.* to 'root'@'localhost' identified by 'TWvoRu4Y5IgYwN1y' with grant option;
    flush privileges;
