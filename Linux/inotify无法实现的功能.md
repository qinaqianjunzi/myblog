### 强大的inotify

#### 昨天使用inotify-tools工具做了文件监控的脚本，部署在服务器上面，今天就发现了问题，inotify没办法记录那个user，那个program对文件进行的操作，还有具体的操作内容。

#### 在StackOverflow上找了找大神的发言

`inotify_event doesn't have a field for that. Since inotify is asynchronous you can't catch the user in the act either.`

#### 大致意思是inotify暂时没有那些功能，由于inotify是异步的，不能再操作的时候捕获用户信息

#### 如果想要实现这个功能，就需要使用c和c++编程了
