# sustainology-web Frontend

    sudo apt update 
    npm install 
    npm run build
    npm start

`Apply new rules for ignore Linting errors`

    filename --->     .eslintrc.json 
    
    {
        "extends": ["next/core-web-vitals", "plugin:prettier/recommended"],
        "rules": { 
    	"react/no-unescaped-entities": "off",
            "prettier/prettier": [
                "error",
                {
                    "endOfLine": "auto"
                }
            ]
        }
    }

http://20.244.100.78:7008 Sustainology-web Frontend

![image](https://github.com/Parasharam-DevOps/snaatak-p7-repo/assets/132131379/f36d317b-2f04-41d0-b5c8-2c15f574d237)

----

# sustainology-admin-web.Frontend

    sudo apt update 
    npm install 
    npm run build
    npm start

http://20.244.100.78:7002 Sustainology-admin-web Frontend

![image](https://github.com/Parasharam-DevOps/snaatak-p7-repo/assets/132131379/d79b93b6-9e8c-419e-a9f7-e603e34cadae)

----

# sustainology-admin-server Backend

    sudo apt update 
    npm install 
    sudo npm install -g nodemon
    npm start 

http://20.244.100.78:4000 Sustainology-admin-Server Backend

![image](https://github.com/Parasharam-DevOps/snaatak-p7-repo/assets/132131379/bfd643bf-318d-4ce6-bb7e-7e12bb75d699)

----

# Service Files

## sustainology-admin-server.service

    
    sudo vim /etc/systemd/system/sustainology-admin-server.service
    
    sudo systemctl daemon-reload
    
    sudo systemctl enable sustainology-admin-server
        
    sudo systemctl start sustainology-admin-server

```shell
[Unit]

Description=Sustainology Admin Server
After=network.target

[Service]

User=ubuntu
WorkingDirectory=/home/ubuntu/sustainology-admin-server
ExecStart=npm start
Restart=always

[Install]

WantedBy=multi-user.target

```

---

## sustainology-admin-web.service

      sudo vim /etc/systemd/system/sustainology-admin-web.service
      
      sudo systemctl daemon-reload
      
      sudo systemctl enable sustainology-admin-web
      
      sudo systemctl start sustainology-admin-web

```shell
[Unit]
Description=Sustainology Admin Web
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/sustainology-admin-web
ExecStart=npm start
Restart=always

[Install]
WantedBy=multi-user.target
```

---

## sustainology-web.service

    sudo vim /etc/systemd/system/sustainology-web.service
    
    sudo systemctl daemon-reload
    
    sudo systemctl enable sustainology-web
    
    sudo systemctl start sustainology-web

```shell

[Unit]
Description=Sustainology Web
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/sustainology-web
ExecStart=npm start
Restart=always

[Install]
WantedBy=multi-user.target

```

# Service File Status

![image](https://github.com/Parasharam-DevOps/snaatak-p7-repo/assets/132131379/bc2d9a2c-2139-4739-9d97-37a29155742a)









