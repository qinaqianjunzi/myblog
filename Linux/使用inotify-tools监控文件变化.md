#### 最近网站总是被频繁挂马，莫名的加载了外部的js文件，然后就跳转到灰产的网站，发现了一部分原因，有宝塔漏洞的，也有nginx漏洞导致的被劫持，文件被修改。

#### 一个可靠的文件监控系统就非常有必要，看了网上的关于文件系统的介绍，决定选择linux系统级的文件监控工具inotify

#### 安装

` yum install inotify-tools`

` apt-get install inotify-tools`

#### 主要使用***inotifywait***\*\* 方法执行，所以专门写了shell脚本，再任务计划里面跑\*\*

    #!/bin/bash
    #qianqianjunzi521@gmail.com

    killall inotifywait
    path=/www/wwwlogs/inotify/
    log_file=${path}$(date +%Y%m%d).log
    [ ! -d ${path} ] && mkdir -p ${path}
    [ ! -f ${log_file} ] && touch ${log_file}
    #execute script and log
    inotifywait -mr --timefmt '%d/%m/%y/%H:%M:%S' --format '%T %w %f %Xe' -e modify,delete,create,attrib,move /www/wwwroot -o ${log_file} --exclude 'runtime' -d

    inotifywait -mr --timefmt '%d/%m/%y/%H:%M:%S' --format '%T %w %f %Xe' -e modify,delete,create,attrib,move /www/server/mysql -o ${log_file} -d

    inotifywait -mr --timefmt '%d/%m/%y/%H:%M:%S' --format '%T %w %f %Xe' -e modify,delete,create,attrib,move /www/server/nginx -o ${log_file} -d

    inotifywait -mr --timefmt '%d/%m/%y/%H:%M:%S' --format '%T %w %f %Xe' -e modify,delete,create,attrib,move /www/server/panel -o ${log_file} --exclude 'data|cache|tmp|temp|log|__pycache__' -d

    inotifywait -mr --timefmt '%d/%m/%y/%H:%M:%S' --format '%T %w %f %Xe' -e modify,delete,create,attrib,move /etc/systemd/system -o ${log_file} -d

    inotifywait -mr --timefmt '%d/%m/%y/%H:%M:%S' --format '%T %w %f %Xe' -e modify,delete,create,attrib,move /var/lib -o ${log_file} --exclude 'rsyslog|chrony' -d

#### 将脚本加入任务计划，每天凌晨执行一次，这样日志的输出内容会少很多，方便阅读
