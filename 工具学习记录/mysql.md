## 跳过权限校验
skip-grant-tables
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Bzy8@9Irgd';
 FLUSH PRIVILEGES;

## 解除禁用
`mysqladmin flush-hosts -uroot -p'$OUQ3QzD'`

# 删除所有表
```mysql
SET GROUP_CONCAT_MAX_LEN = 32768;
SELECT CONCAT('DROP TABLE IF EXISTS ', GROUP_CONCAT(table_name), ';') 
INTO @drop_statement 
FROM information_schema.tables 
WHERE table_schema = 'tognix';

PREPARE stmt FROM @drop_statement;
EXECUTE stmt;
DEALLOCATE PREPARE stmt;

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

-- 修改登录主机限制
UPDATE mysql.user SET Host = '%' WHERE User = 'root' AND Host = 'localhost';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;

```
## 索引和外键
  
索引和外键是数据库中两个重要但不同的概念，它们各自有不同的用途和功能：

### 索引（Index）

1. **目的**： 索引用于加快数据库查询的速度。通过在一个或多个列上创建索引，数据库可以更快地定位和检索数据。
    
2. **工作原理**： 索引是对数据库表中一列或多列值进行排序的数据结构（通常是B树或哈希表）。有了索引，数据库在查找特定值时可以使用高效的搜索算法，而不必逐行扫描整个表。
    
3. **类型**：
    
    - **主键索引**：自动在设为主键的列上创建，保证列的唯一性和记录的易查性。
    - **唯一索引**：保证列中的数据唯一。
    - **普通索引**：加快访问速度，不保证数据的唯一性。
    - **全文索引**：用于加快文本搜索。
4. **性能影响**： 虽然索引可以提升查询速度，但它也会占用额外的存储空间，并且可能减慢数据的插入、删除和更新操作，因为索引本身也需要维护。
    

### 外键（Foreign Key）

1. **目的**： 外键用于在两个表之间建立链接，并强制数据完整性。它确保一个表中的数据引用另一个表中的有效数据。
    
2. **工作原理**： 外键是一个表中的字段，它是另一个表的主键。这种关系帮助维护跨表的数据一致性，防止产生没有参照完整性的孤立数据。
    
3. **约束**：
    
    - **级联更新**：如果主键表中的数据被更新，相关的外键数据也会自动更新。
    - **级联删除**：如果主键表中的数据被删除，相关的外键数据也会被删除，防止留下没有意义的数据。
4. **数据完整性**： 外键关键在于它们维护了数据的引用完整性。例如，如果你有一个订单表和一个客户表，订单表中的客户ID列可以设置为客户表的主键的外键，确保每个订单都关联到一个有效的客户。
    

### 索引与外键的关联

虽然索引和外键是为了不同目的而设计的，但在实际使用中，它们经常一起工作以提高效率和完整性。例如，外键字段通常会被自动或建议索引，因为数据库在执行关联查询或维护数据完整性时需要高效地查找外键值。如果外键列没有被索引，那么每次更新或检查外键约束时，数据库可能需要执行全表扫描，这会大大降低性能。

总之，索引主要用于提高查询效率，而外键用于保证数据之间的逻辑关系和完整性。在数据库设计和优化时，合理使用这两者可以显著提高数据库的性能和数据质量。