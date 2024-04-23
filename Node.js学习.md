# Node.js全局变量

常见全局变量:

[文档](https://nodejs.cn/api/globals.html#%E5%85%A8%E5%B1%80%E5%AF%B9%E8%B1%A1)

- \__filename:返回脚本文件的绝对路径
- \__dirname:返回脚本文件所在目录
- process:提供与当前进程互动的接口



# process



方法:

- [memoryUsage()](https://nodejs.cn/api/process.html#processmemoryusage):返回描述 Node.js 进程的内存使用量（以字节为单位）的对象
- cwd(): 返回当前进程的运行目录
- uptime(): 返回当前Node.js已经运行的秒数



属性:

- [env](https://nodejs.cn/api/process.html#processenv): The `process.env` property returns an object containing the user environment. See [`environ(7)`](http://man7.org/linux/man-pages/man7/environ.7.html).可从该对象里找需要的信息
- [arch](https://nodejs.cn/api/process.html#processarch): 返回操作系统的CPU架构
- [version](https://nodejs.cn/api/process.html#processversion): 返回node版本
- platform: 返回node所在的操作系统平台的标识
- [argv](https://nodejs.cn/api/process.html#processargv): 返回数组，其中包含启动 Node.js 进程时传入的命令行参数。
- pid: 返回当前进程id



# path



## [basename](https://nodejs.cn/api/path.html#pathbasenamepath-suffix)获取文件名

path.basename(path [,suffix])

- `path`  <string>
- `suffix` <string> 要删除的可选后缀
- 返回：<string>



`path.basename()` 方法返回 `path` 的最后一部分，类似于 Unix `basename` 命令。忽略尾随 [目录分隔符](https://nodejs.cn/api/path.html#pathsep)。

~~~javascript
path.basename('/foo/bar/baz/asdf/quux.html');
// Returns: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html');
// Returns: 'quux'
~~~





## [dirname](https://nodejs.cn/api/path.html#pathdirnamepath)获取目录名



~~~javascript
path.dirname('/foo/bar/baz/asdf/quux');
// Returns: '/foo/bar/baz/asdf'
~~~

要获取当前目录名称,使用`__dirname`变量.



## [extname]()获取扩展名

`path.extname()` 方法返回 `path` 的扩展名，即 `path` 的最后一部分中从最后一次出现的 `.`（句点）字符到字符串的结尾。如果 `path` 的最后一部分中没有 `.`，或者除了 `path` 的基本名称（参见 `path.basename()`）的第一个字符之外没有 `.` 个字符，则返回空字符串。



~~~javascript
path.extname('index.html');
// Returns: '.html'

path.extname('index.coffee.md');
// Returns: '.md'

path.extname('index.');
// Returns: '.'

path.extname('index');
// Returns: ''

path.extname('.index');
// Returns: ''

path.extname('.index.md');
// Returns: '.md'
~~~



## [parse](https://nodejs.cn/api/path.html#pathparsepath)解析路径



## [format](https://nodejs.cn/api/path.html#pathformatpathobject)从对象返回路径



## [join](https://nodejs.cn/api/path.html#pathjoinpaths)拼接路径



## [resolve](https://nodejs.cn/api/path.html#pathresolvepaths)得到绝对路径

