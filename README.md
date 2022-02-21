# JAXDisk
JAXDisk is a IndexDB backed Web file system. It provides async/sync access to the file system. To reduce the complexity of storage DB, root dirs are **disk** object that has own dedicated IndexDB. Only **disk** dirs is allowed in root path.
## Async API
### New dir
```javascript
async JAXDisk.newDir(path:string, ?allowDisk:boolean=false, ?recursive:boolean=true ):boolean
```
**Description**: Asynchronously create a new dir at *[path]*, return a <Promise>, fulfills **true** on success.  
**Arguments**:
- **path**: string, the path to make new dir
- **allowDisk**: boolean, when true, new disk will be created if the path is a disk. default: fase.
- **recursive**: recursively create dir if upper dir is not exist.

### Delete item
```javascript
async JAXDisk.del(path:string, ?allowDisk:boolean=false, ?recursive:boolean=true):boolean
```
**Description**: Asynchronously delete a entry (file or dir) at *[path]*, return a <Promise> fulfills **true** on success.  
**Arguments**:
- **path**: string, the path to delete
- **allowDisk**: boolean, when true, disk will be delete if the path is a disk. default: fase.
- **recursive**: recursively delete dir contents if path is a dir.

### Read file contents
```javascript
async JAXDisk.readFile(path:string, ?encode:string):Uint8Array||string
```
**Description**: Asynchronously read a file's full contents. return a <Promise> fulfills witch file content on success. Error will be throwed if item at path is not a file.  
**Arguments**:
- **path**: string, file path to read.
- **encode**: string, if been set, fulfill with string content, only "utf8" supported by now.

### Write file
```javascript
async JAXDisk.writeFile(path:string, data:Uint8Array|File|string, ?encode:string):boolean
``` 
**Description**: Asynchronously write a file's full contents. return a <Promise> fulfills witch true on success. Error will be throwed if item at path is not a file.  
**Arguments**:
- **path**: string, file path to write.
- **data**: Uint8Array|File|string, content to write.
- **encode**: string, if been set, convert data to string, only "utf8" supported by now.

### Get entry info:
```javascript
async JAXDisk.getEntry(path:string):object|null
```
**Description**: Asynchronously get a entry (file or dir)'s infomation. return a <Promise> fulfills witch info-object on success, with **null** if path is not exist.  
**Arguments**:
- **path**: string, file path to write.  
```javascript
//dir info:
{
	name:string,//Dir name
	dir:1,//This is a dir
	createTime:number,//Dir create time
}
//file info:
{
	name:string,//File name,
	createTime:number,//File create time,
	modifyTime:number,//Last modify time
	size:integer,//File size
}
```

