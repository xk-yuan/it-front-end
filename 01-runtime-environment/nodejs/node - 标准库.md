### 标准模块

```
[标准模块]

	：fs
  
  ：events
  
  ：http
  
  ：url
  
  ：util
  
  ：os
  
  ：path
  
  ：Net
  
  ：DNS
  
  ：Domain
```

### 第三方模块

#### mysql

```javascript
[mysql]

  ：mysql # npm install mysql

var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '123456',
  database : 'test'
});
 
connection.connect();

// ...

connection.end();
```

```javascript
[CURD]

var  sql = 'SELECT * FROM websites';
//查
connection.query(sql,function (err, result) {
        if(err){
          console.log('[SELECT ERROR] - ',err.message);
          return;
        }
 
       console.log('--------------------------SELECT----------------------------');
       console.log(result);
       console.log('------------------------------------------------------------\n\n');  
});

connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});


// 增
var  addSql = 'INSERT INTO websites(Id,name,url,alexa,country) VALUES(0,?,?,?,?)';
var  addSqlParams = ['菜鸟工具', 'https://c.runoob.com','23453', 'CN'];

connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
         console.log('[INSERT ERROR] - ',err.message);
         return;
        }        
 
       console.log('--------------------------INSERT----------------------------');
       //console.log('INSERT ID:',result.insertId);        
       console.log('INSERT ID:',result);        
       console.log('-----------------------------------------------------------------\n\n');  
});

// 改
var modSql = 'UPDATE websites SET name = ?,url = ? WHERE Id = ?';
var modSqlParams = ['菜鸟移动站', 'https://m.runoob.com',6];

connection.query(modSql,modSqlParams,function (err, result) {
   if(err){
         console.log('[UPDATE ERROR] - ',err.message);
         return;
   }        
  console.log('--------------------------UPDATE----------------------------');
  console.log('UPDATE affectedRows',result.affectedRows);
  console.log('-----------------------------------------------------------------\n\n');
});

//删
var delSql = 'DELETE FROM websites where id=6';

connection.query(delSql,function (err, result) {
        if(err){
          console.log('[DELETE ERROR] - ',err.message);
          return;
        }        
 
       console.log('--------------------------DELETE----------------------------');
       console.log('DELETE affectedRows',result.affectedRows);
       console.log('-----------------------------------------------------------------\n\n');  
});
```

```
host	主机地址 （默认：localhost）
　　user	用户名
　　password	密码
　　port	端口号 （默认：3306）
　　database	数据库名
　　charset	连接字符集（默认：'UTF8_GENERAL_CI'，注意字符集的字母都要大写）
　　localAddress	此IP用于TCP连接（可选）
　　socketPath	连接到unix域路径，当使用 host 和 port 时会被忽略
　　timezone	时区（默认：'local'）
　　connectTimeout	连接超时（默认：不限制；单位：毫秒）
　　stringifyObjects	是否序列化对象
　　typeCast	是否将列值转化为本地JavaScript类型值 （默认：true）
　　queryFormat	自定义query语句格式化方法
　　supportBigNumbers	数据库支持bigint或decimal类型列时，需要设此option为true （默认：false）
　　bigNumberStrings	supportBigNumbers和bigNumberStrings启用 强制bigint或decimal列以JavaScript字符串类型返回（默认：false）
　　dateStrings	强制timestamp,datetime,data类型以字符串类型返回，而不是JavaScript Date类型（默认：false）
　　debug	开启调试（默认：false）
　　multipleStatements	是否许一个query中有多个MySQL语句 （默认：false）
　　flags	用于修改连接标志
　　ssl	使用ssl参数（与crypto.createCredenitals参数格式一至）或一个包含ssl配置文件名称的字符串，目前只捆绑Amazon RDS的配置文件
```

#### mongodb

```javascript
[mongodb]

  ：mongodb # npm install mongodb

var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/runoob";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
  if (err) throw err;
  console.log("数据库已创建!");
  db.close();
});

// 创建集合
var MongoClient = require('mongodb').MongoClient;
var url = 'mongodb://localhost:27017/runoob';
MongoClient.connect(url, { useNewUrlParser: true }, function (err, db) {
    if (err) throw err;
    console.log('数据库已创建');
    var dbase = db.db("runoob");
    dbase.createCollection('site', function (err, res) {
        if (err) throw err;
        console.log("创建集合!");
        db.close();
    });
});
```

```javascript
[CURD]

// 插入
var dbo = db.db("runoob");
var myobj = { name: "菜鸟教程", url: "www.runoob" };
dbo.collection("site").insertOne(myobj, function(err, res) {
  if (err) throw err;
  console.log("文档插入成功");
  db.close();
});

// 插入多条数据
var myobj =  [
  { name: '菜鸟工具', url: 'https://c.runoob.com', type: 'cn'},
  { name: 'Google', url: 'https://www.google.com', type: 'en'},
  { name: 'Facebook', url: 'https://www.google.com', type: 'en'}
];
dbo.collection("site").insertMany(myobj, function(err, res) {
  if (err) throw err;
  console.log("插入的文档数量为: " + res.insertedCount);
  db.close();
});

// 查询数据
dbo.collection("site"). find({}).toArray(function(err, result) { // 返回集合中所有数据
  if (err) throw err;
  console.log(result);
  db.close();
});

// 更新数据
dbo.collection("site").updateOne(whereStr, updateStr, function(err, res) {
  if (err) throw err;
  console.log("文档更新成功");
  db.close();
});

// 删除数据
dbo.collection("site").deleteOne(whereStr, function(err, obj) {
  if (err) throw err;
  console.log("文档删除成功");
  db.close();
});
```

