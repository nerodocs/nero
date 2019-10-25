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

.. _MongoDB安装文档: https://docs.mongodb.com/manual/administration/install-community/
.. _MonggoDB配置文档: https://docs.mongodb.com/manual/reference/configuration-options/

Mysql
----------------------------

Mysql 用户授权
`````````````````````

.. code-block:: bash:

    grant all privileges on *.* to 'root'@'localhost' identified by 'TWvoRu4Y5IgYwN1y' with grant option;
    
    flush privileges;
