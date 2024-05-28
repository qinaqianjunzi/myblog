### 需求

#### 要求插入数据库表name字段判断是否有指定地字符串，如果有不添加，如果没有添加.

#### 本来地想法是通过thinkphp5的查询事件操作，但是默认不支持插入之前的变更数据，而且程序本身是商业版的程序，对操作表的部分做了sg的加密处理，那就只能使用MySQL的触发器了，而且MySQL的触发器支持插入之前的数据处理，更加的符合需求。


## 两个触发器同时运行的sql

>     -- 如果存在触发器则删除，这个代码不能放在delimiter结构体内，部分版本无法识别
>     DROP TRIGGER IF EXISTS preUpdate;
>     -- 创建更新的触发器
>     delimiter $$ -- 临时修改语句结束符
>     create trigger preUpdate BEFORE UPDATE on vod for each row
>     begin
>     -- 	获取cid
>     declare pid int(11);
>     SELECT list_pid INTO pid FROM zanpiancms_list WHERE list_id = NEW.vod_cid;
>     IF pid = 1 THEN
>     IF NEW.vod_cid = 31 THEN
>     IF locate('xxxx',NEW.vod_name) = 0 THEN
>     SET NEW.vod_name=CONCAT(NEW.vod_name,'xxxx');
>     END IF;
>     ELSE
>     IF locate('yyyy',NEW.vod_name) = 0 THEN
>     SET NEW.vod_name=CONCAT(NEW.vod_name,'yyyy');
>     END IF;
>     END IF;
>     ELSEIF pid = 2 THEN
>     IF locate('zzzz',NEW.vod_name) = 0 THEN
>     SET NEW.vod_name=CONCAT(NEW.vod_name,'zzzz');
>     END IF;
>     END IF;	
>     end -- 触发器内容结束
>     $$ -- 结束语句
>     delimiter ; -- 恢复语句结束符
>
>     -- 如果存在触发器则删除，这个代码不能放在delimiter结构体内，部分版本无法识别
>     DROP TRIGGER IF EXISTS preInsert;
>     -- 创建插入的触发器
>     delimiter $$ -- 临时修改语句结束符
>     create trigger preInsert BEFORE INSERT on vod for each row
>     begin
>     -- 	获取cid
>     declare pid int(11);
>     SELECT list_pid INTO pid FROM list WHERE list_id = NEW.vod_cid;
>     IF pid = 1 THEN
>     IF NEW.vod_cid = 31 THEN
>     IF locate('xxxx',NEW.vod_name) = 0 THEN
>     SET NEW.vod_name=CONCAT(NEW.vod_name,'xxxx');
>     END IF;
>     ELSE
>     IF locate('yyyy',NEW.vod_name) = 0 THEN
>     SET NEW.vod_name=CONCAT(NEW.vod_name,'yyyy');
>     END IF;
>     END IF;
>     ELSEIF pid = 2 THEN
>     IF locate('zzzz',NEW.vod_name) = 0 THEN
>     SET NEW.vod_name=CONCAT(NEW.vod_name,'zzzz');
>     END IF;
>     END IF;
>     end -- 触发器内容结束
>     $$ -- 结束语句
>     delimiter ; -- 恢复语句结束符

#### 触发器的创建必须使用root超级用户，其他用户不允许创建，否则会出现报错

![image](https://github.com/qinaqianjunzi/myblog/assets/48326971/9a21f99d-ad73-4086-9f50-8a4be0da6664)

