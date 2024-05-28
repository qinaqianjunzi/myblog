### nginx判断是否手机端或则PC端

>     #判断是否是pc端 
>     if ($http_user_agent !~* "android|bb\d+|meego).+mobile|avantgo|bada/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox
>     |netfront|operam(ob|in)i|palm( os)?|phone|p(ixi|re)/|plucker|pocket|psp|series(4|6)0|symbian|treo|up.(browser|link)|vodafone|wap|windows ce|xda|xiino") {
>     	###
>     	###	代码
>     	###
>
>     }
>
>
>
>     #判断是否是h5端
>     if ($http_user_agent ~* "android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox|
>             netfront|operam(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows ce|xda|xiino") {        
>             ###
>     	###	代码
>     	###		
>         }

#### 判断pc端的话执行伪静态

> #### 判断请求的url中包含`xxxx` 或则`yyyy`，直接到一个不存在的地址
>
> `rewrite '.xxxx|yyyy.' /xxxx999xxxx;`

#### 完整的代码,将代码插入站点的配置文件中就可以实现了

>     #判断是否是pc端 并判断是否包含特定的字符串，并返回404
>     if ($http_user_agent !~* "(android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox
>       |netfront|operam(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows ce|xda|xiino") {      
>         # rewrite '.xxxx|yyy.' /xxxx999xxxx;
>         # return 404;
>     }

