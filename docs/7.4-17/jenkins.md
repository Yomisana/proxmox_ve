# Proxy
> 如果有開放外網時 Proxy的相關設定
## nginx 設定檔
> 如果出現 Proxy 錯誤
```
server {
    listen      80;
    listen      [::]:80;
    server_name jenkins.example.com;

    location / {
        return 301 https://jenkins.example.com$request_uri;
    }
}
server {
    listen                  443 ssl http2;
    listen                  [::]:443 ssl http2;
    server_name jenkins.example.com;
    location / {
        proxy_pass http://192.168.xx.x:8080;
        proxy_read_timeout  90;
        proxy_set_header X-Forwarded-Host $host:$server_port;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
    }
    # SSL
    # 如果你有hppts簽證設定可以新增在此
    # 我是設定在 /etc/nginx/config/ssl.conf *.example.com 簽證
    include                 config/ssl.conf;
}
```
config/ssl.conf
```
# ssl
ssl_certificate         /etc/letsencrypt/live/example.com/fullchain.pem;
ssl_certificate_key     /etc/letsencrypt/live/example.com/privkey.pem;
ssl_trusted_certificate /etc/letsencrypt/live/example.com/chain.pem;
```
## jenkins URL 設定
> 如果出現 您的 Reverse Proxy 設定好像有點問題喔。
> 此設定只需要設定成本地IP與Jenkins Port 即可
> http://192.168.xx.xx:8080/


# 主端點 與 下屬端點問題與見解
> 如果你的端點為個人或是公司內部使用(單機做部署，無多台部署主機時)並且不會開放對外(公開給網際網路上的用戶隨心所欲使用)，那"可能"不需要分主端點與下屬端點問題。
> 如果你單機做部署，但是也想要安全性高點的話...依據 Jenkins 的官網說明，你可以在 linux 上創建一個獨立的使用者帳戶並且用它來部署(其他使用者來部署這塊沒有嘗試過，有興趣的人可以嘗試看看)

## 主端點問題
> 如果你的 主端點不需要建置只是控制下屬端點的話那主端點的硬體配置可以用比較低階。
> 例如官方的最低規格建議:
> CPU: 單核(使用虛擬機時)，不侷限(你用 最低階的 Intel Atom 也可)
> RAM: 256MB
> DISK: 1GB(如果有下屬端點，那麼主端點並且存放 ``"項目作業檔"`` 與 ``"各類TOKEN,SSH key,certificate...etc"``)

## 下屬端點
> 只需要在 主端點上 設定好 下屬端點的名稱與遠端的目錄路徑為何(遠端目錄這邊指的是你的下屬端點主機的目錄，而非主端點的目錄!)  
> 在主端點的創建好下屬端點後，在下屬端點頁面上可以看到各項系統的設定指令。(注意!這邊顯示的會是你設定的 [jenkins URL 設定](#jenkins-url-設定))  
> 如果為外網端點可能需要改成 你外網所登入的url網址  
> 在下屬端點上設定後通常就可以了，只是好像需要設定一個 cron 或是 工作排程器 讓他能持續與 主端點做連線