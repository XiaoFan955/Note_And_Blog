#### 批量更新某一字段的数据

~~~sql
update table_name set column_name=(column_name,'old','new');
'比如将图片存储路径的localhost替换成服务器域名
~~~

#### 修改字段长度

~~~sql
alter table table_name modify column column_name type; 
'比如将url字段由varchar(100)改为varchar(200)
~~~

