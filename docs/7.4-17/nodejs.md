# Ubuntu 簡單快速安裝 nodejs
> 使用 [https://deb.nodesource.com/](https://deb.nodesource.com/) 來進行安裝
>
> ~$ ```sudo apt-get update && sudo apt-get install -y ca-certificates curl gnupg```  
> ~$ ```curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg```  
> ~$ ```NODE_MAJOR=20```  
> ~$ ```echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list```  
> ~$ ```sudo apt-get update && sudo apt-get install nodejs -y```  
> ~$ ```nodejs -v```  

# 無須 sudo nodejs 的 nvm 套件
> 解決 npm i 需要 sudo 的問題  
## 安裝 nvm 套件
> ~$ ```curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash```  
> ~$ ```nvm install node```  
> ~$ ```source ~/.bashrc```
> ~$ 現在你，無須 sudo npm install 了!
> ~$ ```npm install```

## 查看當前 nvm 所安裝的 Node.js 版本號
> ~$ ```nvm ls```

## 查看當前 nvm 所安裝的 Node.js 版本號
> ~$ ```nvm ls```
