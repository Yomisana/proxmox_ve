# 伺服器硬體資訊
CPU: 8core
RAM: 8G

# 優化設定檔
- 優化設定檔時記得把數據庫資料給備份起來
```
# Yomisana - 優化資料庫v2.1 2023-11-03
[mariadb]
# 設定給多少記憶體給SQL把資料儲存在記憶體上,所以將直接影響讀寫的效率.
innodb_buffer_pool_size = 2G
# innodb_log_file_size 為 innodb_buffer_pool_size 的 25%
innodb_log_file_size = 512M 
# 多少執行緒(1-4: 差不多 建議:8 最好:64)
innodb_buffer_pool_instances = 8
# Insert資料的上限(如果需要匯入資料很多時，可以避免失敗)
max_allowed_packet = 1G
# 最大連線數(預設100有點小，最高可設定16384，設大可避免連線不足的問題)
max_connections = 300
# 加速Order By或Group By的運作
tmp_table_size = 1G
# 記憶體資料表大小
max_heap_table_size = 1G
# phpmyadmin 建議參數
query_cache_type = 1
query_cache_size = 1G
query_cache_limit = 64M
long_query_time = 1
slow_query_log = ON
```
