## 跳过权限校验
skip-grant-tables
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Bzy8@9Irgd';
 FLUSH PRIVILEGES;

# 删除所有表
```mysql
SELECT CONCAT('DROP TABLE IF EXISTS ', table_name, ';') FROM information_schema.tables WHERE table_schema = 'your_database_name';
```

# 创建数据库
```mysql
-- 创建数据库
CREATE DATABASE mydatabase;
-- 创建 用户
CREATE USER 'TognixAdmin'@'%' IDENTIFIED BY 'Bzy8@9Irgd';
-- 选择数据库
USE mydatabase;
-- 设置数据字符集
CREATE DATABASE mydatabase CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
-- 授权数据库
GRANT ALL PRIVILEGES ON 数据库名称.* TO '用户名'@'主机名' IDENTIFIED BY '密码';
-- 刷新
FLUSH PRIVILEGES;

-- 临时禁用二进制日志对权限的校验
SET GLOBAL log_bin_trust_function_creators = 1;

```