## 功能实现

### &#x20;目前有很多台服务器，服务器上面有若干个站点，需求是再同一个站点上修改不同服务器不同站点的相同文件（站点程序相同）

### 使用php的lib ssh2扩展，可以实现远程登录服务器，执行各种shell操作


    $connection = ssh2_connect('shell.example.com', 22);
    ssh2_auth_password($connection, 'username', 'password');
    $stream = ssh2_exec($connection, "cd /hom");
    $errorStream = ssh2_fetch_stream($stream, SSH2_STREAM_STDERR);

    // Enable blocking for both streams
    stream_set_blocking($errorStream, true);
    stream_set_blocking($stream, true);

    // Whichever of the two below commands is listed first will receive its appropriate output.  The second command receives nothing
    echo "Output: " . stream_get_contents($stream);
    echo "Error: " . stream_get_contents($errorStream);

    // Close the streams        
    fclose($errorStream);
    fclose($stream);


