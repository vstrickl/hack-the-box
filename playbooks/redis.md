# Redis

1) Connect to target
    `$ redis-cli -h <target_ip>: <port>`

2) Get database info
    ![Database Info](../images/Screenshot%202025-01-23%20at%2012.59.15 PM.png)

3) Select Database
    - In our case we're going to select db 0 by running
    ![How to Select a Database](../images/Screenshot%202025-01-23%20at%2012.59.24 PM.png)

4) Get the Value of the Target Key
    - List all keys in the DB: `keys *`
    - Get the value of the key: `gey <key>`