1. 如果coll中有外键，并且此外键作为 搜索 字段，那么可以为外键添加额外的字段。  
例如，billType:{name:String,parentBillType:mongoose.Schema.Types.ObjectId,ref:"billTypes"}  
这是个自连接表，billType的上级也是billType中的一个记录。  
如果要根据parentBillType进行查找，那么首先要将 搜索字符（人类不会使用ObjectId直接搜索） 转换成ObjectId，然后使用$in操作符对parentBillType字段进行查找。  
上述方法需要2次查表。  
改进方法是添加一个parentBillTypeName字段，将对应
