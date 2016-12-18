# Apache(httpd) , PHP,  MySQL サーバ インストール

```bash
sudo yum install httpd mysql-server php php-mysql php-mbstring -y
```

# httpd, MySQL 起動

```bash
sudo /sbin/chkconfig mysqld on
sudo /sbin/chkconfig httpd on
sudo /etc/init.d/mysqld start
sudo /etc/init.d/httpd start
```

# WordPress インストール

```bash
wget http://ja.wordpress.org/latest-ja.tar.gz ~/
tar zxvf ~/latest-ja.tar.gz
sudo cp ~/wordpress/* /var/www/html/ -r
sudo chown apache:apache /var/www/html -R
```

# DB 事前設定 (データベース, ユーザー)

```bash
mysql --user=root
```

```sql
CREATE DATABASE wordpress;
GRANT ALL PRIVILEGES ON wordpress.* TO
"wpuser"@"localhost"
IDENTIFIED BY "wppassword";
FLUSH PRIVILEGES;
quit;
```

# ブラウザで WordPress の設定画面にアクセス
http://インスタンスの Public DNS//wp-admin/setup-config.php
例) http://ec2-0-1-2-xxx.ap-northeast-1.compute.amazonaws.com/wp-admin/setup-config.php

## うまく見えない場合

- Security Groupで 80(HTTP)は有効になっていますか？
- httpd は正しく起動していますか？
