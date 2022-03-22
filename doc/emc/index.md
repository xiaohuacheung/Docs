# EMC 常见问题


##   EMC Documentum  基本操作

###### 完整启动 EMC Documentum 
	用户：emcadmin
	路径：/home/emcadmin/documentum/dba

	命令1:  ./dm_launch_Docbroker
	命令2:  ./dm_launch_Docbroker91
	命令3:  ./dm_start_emcdb

###### 完整停止 EMC Documentum 
	用户：emcadmin
	路径：/home/emcadmin/documentum/dba
	命令1:  ./dm_stop_Docbroker
	命令2:  ./dm_stop_Docbroker91
	命令3:  ./dm_shutdown_emcdb







## 修改EMC Documentum 数据库密码


###### 停服务
	用户：emcadmin
	路径：/home/emcadmin/documentum/dba
	命令: ./dm_shutdown_emcdb

###### 备份密码
	用户：emcadmin
	路径：/home/emcadmin/documentum/dba/config/emcdb
	命令: cp dbpasswd.txt dbpasswd.txt.20220322 

###### 写入新密码
	用户：emcadmin
	路径：/home/emcadmin/documentum/dba/config/emcdb
	命令: echo "DM_ENCR_TEXT=2wsx@WSX" > dbpasswd.txt 


###### 生成新密码
	用户：emcadmin
	路径：/home/emcadmin/documentum/product/6.6/bin
	命令: ./dm_encrypt_password -docbase emcdb -rdbms -encrypt 2wsx@WSX


###### 启动服务
	用户：emcadmin
	路径：/home/emcadmin/documentum/dba
	命令: ./dm_start_emcdb
     


## DQL查询参考


