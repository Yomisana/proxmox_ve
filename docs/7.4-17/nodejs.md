# Ubuntu 簡單快速安裝 nodejs
> 使用 [https://deb.nodesource.com/](https://deb.nodesource.com/) 來進行安裝
```
~$ sudo apt-get update && sudo apt-get install -y ca-certificates curl gnupg  
~$ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg  
~$ NODE_MAJOR=20  
~$ echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list  
~$ sudo apt-get update && sudo apt-get install nodejs -y  
~$ nodejs -v  
```
# 無須 sudo nodejs 的 nvm 套件
> 安裝 Node 版本管理工具  
> 解決 npm i 需要 sudo 的問題  
## 安裝 nvm 套件
> 安裝 Node 版本管理工具  
```
~$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash  
~$ nvm install node  
~$ source ~/.bashrc 
``` 
> 現在你，無須 sudo npm install 了!  
```~$ npm install```

## 查看當前 nvm 所安裝的 Node.js 版本號
> ~$ ```nvm ls```

## nvm 安裝指定 Node.js 版本號
> ~$ ```nvm install <version>```  
> 例如:  
> ~$ ```nvm install 16.14.2```
## nvm 使用指定 Node.js 版本號
> 注意! 這個只會對於當前的 終端機會話有指定，退出此會話會回到預設Nodejs版本號
> ~$ ```nvm use 16.14.2```

## 設定 nvm 預設 Node.js 版本號
> ~$ ```nvm alias default <version | ex: 16.14.2>```

## 針對單一檔案執行 Node.js 版本號
> ~$ ```nvm run <version | ex: 16.14.2> some_script.js```