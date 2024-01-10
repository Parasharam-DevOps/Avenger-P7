**Install Redis**

Once you're running Ubuntu on Windows, you can follow the steps detailed at Install on Ubuntu/Debian to install recent stable versions of Redis from the official packages.redis.io APT repository. Add the repository to the apt index, update it, and then install:

    curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
    
    echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee 
    /etc/apt/sources.list.d/redis.list
    
    sudo apt-get update
    sudo apt-get install redis

**Start the Redis server like so:**

 
    sudo service redis-server start


**Connect to Redis**
You can test that your Redis server is running by connecting with the Redis CLI:

    redis-cli 

https://redis.io/docs/install/install-redis/install-redis-on-windows/

