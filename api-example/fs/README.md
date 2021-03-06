#基于 Node.js v6.2.0 的fs API
###fs.access(path, [mode], callback)
```
判断文件存在否，判断文件的能读、写、执行否
mode标识了access要判断的内容是文件的存在、还是rwx（读、写、执行），
不传默认为0。 
```
```javascript
//mode的参数与linux下rwx的代号一致
const fs=require("fs");
console.log(fs.F_OK);//0 默认的，判断文件是否存在
console.log(fs.X_OK);//1 linux下的文件是否可执行属性
console.log(fs.W_OK);//2 文件是否可写
console.log(fs.R_OK);//4 文件是否可读

```
```javascript
//默认情况判断文件是否存在
fs.access('./foo.txt', (err) => {
  console.log(err ? 'no access!' : 'access！');
})
fs.access('./foo.txt',2&4,(err) => {
  console.log(err ? 'no access!' : 'can read&write');
})
```

###fs.accessSync(path[, mode])
```
fs.access的同步方法
```
```javascript
fs.access('./foo.txt',2);
```

###fs.appendFile(file, data,[options], callback)
```
向目标文件中已有的内容后添加内容，目标文件不存在则创建该文件。
```
```javascript
fs.appendFile('foo.txt', 'data to append', (err) => {
  if (err) throw err;
  console.log('The "data to append" was appended to file!');
});
fs.appendFile('foo.txt', 'data to append','utf8',(err) => {
  if (err) throw err;
});
```
###fs.appendFileSync(file, data,[options])
```
fs.appendFile的同步方法
```
```javascript
fs.appendFile('foo.txt', 'data to append','utf8');
```
###fs.chmod(path, mode, callback)
```
修改改文件权限,mode值和linux里chmod设置权限的值一样，
例如777、776
```
```javascript
fs.chmod('foo.txt',777,(err) => {
  if (err) throw err;
});
```

###fs.chmodSync(path, mode)
```
fs.chmod的同步方法
```
```javascript
fs.chmod('foo.txt',777);
```

###fs.chown(path, uid, gid, callback)
```
将指定文件的拥有者改为指定的用户或组，uid用户id，gid组id
```
```javascript
fs.chown('content.txt', 'KingNigel', 'itcast', function(err){
   if(err){console.log(err);}
})
```
###fs.chmodSync(path, mode)
```
fs.chown的同步方法
```
```javascript
fs.chown('content.txt', 'KingNigel', 'itcast');
```

###fs.close(fd, callback)
```
于fs.open配合使用，关闭fs.open()打开的文件,
callback可选参数。
```
```javascript
fs.close(fd);
```
###fs.closeSync(fd)
```
fs.close的同步方法
```
```javascript
fs.closeSync(fd);
```
###fs.createReadStream(path,[options])
```
创建一个将文件内容读取为流数据的ReadStream的对象。options为可选参数

```
#标记api编写的进度
###fs.unlink(path, callback)
```
 删除文件
```
```javascript
fs.unlink('foo.txt', () =>{
    console.log('success') ;
}) ;
```
###fs.unlinkSync(path)

```
fs.unlink的同步方法
```

```javascript
fs.unlinkSync('foo.txt');
```

###fs.rename(oldPath, newPath, callback)

``` 
修改文件名称
```
```javascript
fs.rename('/tmp/foo.text', '/tmp/bar.text', (err) => {
  if (err) throw err;
  console.log('renamed complete');
});
```

###fs.renameSync(oldPath, newPath)
``` 
fs.rename的同步方法
```
```javascript
fs.renameSync('/tmp/foo.text', '/tmp/bar.text');
```

###fs.stat(path, callback)
```
查看文件状态
```
```javascript
fs.stat('foo.txt', function(err, stat){
    console.log(stat);
});
```

###fs.statSync(path)
```
fs.stat的同步方法
```
```javascript
fs.statSync('foo.txt');
```

###fs.exists(path, callback)
```
已经弃用，用 fs.stat() 或 fs.access()代替
```
###fs.existsSync(path)
```
已经弃用，用 fs.statSync() 或 fs.accessSync()代替
```
###fs.open(path, flags,[mode], callback)
```
用于打开文件，
- path为文件路径
- flags表示对文件进行
'r'  - 读取文件模式，如果文件不存在则报错。
'r+' - 读取并写入文件模式，如果文件不存在则报错。
'rs' - 使用同步模式打开并读取文件。用于避免文件系统中的缓存，获取最新的文件，因为会影响效率，慎用，
       不能用于替代fs.openSync()。
'rs+' - 以同步的方式打开，读取并写入文件，应用与'rs'相同。
'w' - 写入文件模式，如果文件不存在则创建，如果文件存在则清空里面的内容。
'wx' - 写入文件模式，如果文件存在则报错，不存在则创建文件。
'w+' - 以读写模式打开文件，如果文件不存在则创建，如果文件存在则清空里面的内容。
'wx+' - 以读写模式打开文件，如果文件存在则报错，不存在则创建文件。
'a' - 以追加模式打开文件，如果文件不存在则创建。
'ax' - 和 ' a ' 模式一样，如果文件存在则报错
'a+' - 以读取追加模式打开文件，如果文件不存在则创建
'ax+' - 和 ' a+ ' 模式一样，如果文件存在则返回失败
- mode    用于创建文件时给文件制定权限，默认0666
```
```javascript
fs.open('./foo.js', 'r', function (err, fd) {
    console.log(fd);
})
```
