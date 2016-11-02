1. 如果coll中有外键，并且此外键作为 搜索 字段，那么可以为外键添加额外的字段。  
例如，billType:{name:String,parentBillType:mongoose.Schema.Types.ObjectId,ref:"billTypes"}  
这是个自连接表，billType的上级也是billType中的一个记录。  
如果要根据parentBillType进行查找，那么首先要将 搜索字符（人类不会使用ObjectId直接搜索） 转换成ObjectId，然后使用$in操作符对parentBillType字段进行查找。  
上述方法需要2次查表，第一次是根据字符查找objectid，然后根据objectId进行查找。    
改进方法是添加一个parentBillTypeName字段，将对应的字符字段加入。  
billType:{name:String,parentBillType:mongoose.Schema.Types.ObjectId,ref:"billTypes", **parentBillTypeName:String**}。如此，直接查找parentBillTypeName即可。  
缺点是：create和update的时候要同时更新2个以上字段，略麻烦。但是对于read为主的coll，还是可以接收的。  

