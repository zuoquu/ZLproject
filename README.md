# zl框架构图说明
20190824  
开始构建  
20190902  
经过一段时间折磨基础构成，过程忘了记录洛。  
20190904  
完成了登陆模块，使用在模板中{#dblogin#传值,传值}就可以了，但是必需要传值，两个值  
20190905  
完成首页显示  
20190907  
原geshi 高亮在php>7中不是很好用，固更换prismjs高亮，并完美添加。暂无行号显示。  
20190908-9  
更新页面显示，个人资料列表。完善部分函数。  
20190910  
文章回复，文章列表，聊天，及回复，修复部分错误显示。  
20190911-12  
添加文章处理，增删添改，回复删除  
20190913  
添加搜索，注册移植key，修复文章头像显示。  
20190915  
完成信箱功能。  
20190916  
凌晨3.38完成了，用户处理。程序也差不多陆陆续续完成了。历时14天。  
添加最后编辑时间显示。  
打包370多k，其中有340左右是高亮文件，剩余30左右是网站源文件，及初始模板。  
后续断断续续维护更新  
20190919  
添加字节color，作为颜色切换，更换deurl,template，增加数据判断。  
20190925  
完善版本更替，用新类替换之前的函数。并添加识别css  
20190926  
增加聊天文章搜索页面nav，添加图片  
20191002  
更新md文件，转义，能正常github显示。  
更新模板wap color 屏蔽帖子  
20191112
添加续贴后自动换行。
增加一个ubb [pb]屏蔽内容不显示存在[/pb]
20191124
添加登陆回复可见ubb,因此，dbubb类中的deubb解析增加一个链接数据库参数。使用 deubb($arr,$dbh)。
20191204
添加高亮行号。
# 使用文档
所有的模板标签处于html内，并且必须遵循php逻辑，符号，标签。规则。  

所有模板不支持镶嵌，如{echo#{trim#传值}}  
正确使用姿势。可以赋值。  
$a={trim#传值};//注意有;  
{echo$#$a}  

所有{% %}内的内容均支持php原型代码，需要转化可以利用dbmain类，和dempdeal类。  

模板开头必须以{(term)}开头，因为在{(term)}之前需要设定title。  

为了和之前站点数据图片文件，同步，因此和之前文件夹位置同步。所有文夹件原应该在zl文件下。为了能正常显示固和zl文件夹同一目录。如果新建站点。请建在zl目录下。并修改文件upload.php保存地址，和filter.func.php文件中的本地表情替换。  

由于多个模板，为了区分字符串，函数，可能会加入$作为个别区分函数字符串。  

# 基础文档
所有文件均会指向p.php文件处理转化。  
class类里面，zqdb类和func类使用文档在文件中。  
# script单独使用
# 点击输入到框
\<a href="#" onclick="atAdd('{% {echo$# $dbusers[1]} %}');return false">@\<\/a\>  

# 实例化文档
dbubb类，dball类均可实例化类，单独使用，如果重复使用，可以实例化使用。  
建议，重复的函数，最好重新实例化比如文章头像和回复头像，一起使用也可以，避免出现不必要的，可以选择其中一个，重新实例化。  

# 模板文档
# {u#http://zl88.net}
这个转化为html标签，\<a href="http://zl88.net"\>http://zl88.net\<\/a\>  
# {u#zl88.net,主流}
这样会转化为 \<a href="zl88.net"\>主流\<\/a\>  
ps:不支持传入函数  
# {u$#函数,主流}
转化为 echo "\<a href='".函数."'\>主流\<\/a\>";  
# {u2$#函数,函数}  
和上面类似。  
如:  
$row = {u$#函数,函数} 注意没有;  
# {img#链接}
和a链接一样。  
# {img$#函数}
转化为 echo '\<imgsre="'.$函数.'"\>';弥补上面不支持函数缺陷。  
# {img$#函数,size:宽\*长}
设置长宽。  
# {echo#内容(no函数)}
转化为 echo '输出内容';  
# {echod#内容(no函数)}
转化为 echo "输出内容";  
ps:单引号，时不支持匹配单引号，双引号时不支持匹配双引号。  
# {echo$#函数(yes函数)}
转化为 echo $函数;为了弥补1，2模块不支持函数。  
# {echou#网址(yes函数),主流(yes函数)}
转化为 echo '\<a href="网址(函数)">主流(函数)\<\/a\>';  
ps:只支持函数。  
# {% %}
这两个符号会自动转化为 \<?php ?\>  
# {(term)}
转化为<\/title><\/head>\<body\>  
# {(end)}
这个符号转化为}，因为都有的花括号转化后都需要一个结束的右括号。  
# {if#条件}
这个会自动转化为 if(条件){ 。所以需要上面的结束符。  
# {elseif#条件}
转化为 }elseif(条件){  
# {else#}
转化为 }else{。  
# {ifisset#条件}
转化为 if(isset(条件){  
# {!ifisset#条件}
转化为 if(!isset(条件){  
# {ifempty#条件}
转化为 if(empty(条件){  
# {!ifempty#条件}
转化为 if(!empty(条件){  
# {for#传值}
转化为 for(传值){  
# {while#传值}
转化为 while(传值){  
# {foreach#传值}
转化为 foreach(传值){  
# {empty#传值}
转化为empty(传值)，注意没得;  
# {trim#传值}
转化为trim(传值),注意没得;  
# {emptr#传值}
为empty和trim结合版，转化为empty(trim(传值)),注意没得;  
# {catalog#}
模板固定函数。返回数组，获取网址上的catalog目录。  
# {date#函数}
转化为date('Y-m-d H:i',函数);所以不能单独用，赋值函数o。  

# db模板文档
# {#dblogin#登陆名,密码}
这个数组登陆模块，使用必须传值:  
输出结果，就是登陆结果。  
# {#dbloginout}
退出。注销。  
# {#dbtitle}
title标签显示内容，不传值显示默认  
# {#dbtitle#传值(no函数)}
显示的是传值的title  
# {#dbtitle$#函数}
显示的是函数的title  
# {#dbindexlists}
首页列表显示，需要配合while()使用，该模块只是执行过程没有值，需要fetch:  
{#dbindexlists}//返回值为$res固定  
{while#$res1=$res->fetch()}  
这里输出$res1[];  
{(end)}  
# {#dbreplys#$tid(必须)}
回复列表显示，和上面函数一样的用法。  
# {#dbshows}
文章内容显示，直接返回$dbshows数组$dbshows[title]，需要配合{echo#$dbshows[1]}  
注:固定函数$dbshows  
# {#dbtopics#函数(必须)}
该函数是处理内容函数，类似ubb,高亮。  
使用先处理，再输出{% {#dbtopics#$dbreads[5]} {echo$#$dbtopics} %}  
注:固定函数$dbtopics  
# {#dbusers#函数(必须)}
可以为空，但是必须传值为空时:{#dbusers#$u}  
$u不赋值。  
读取用户表。返回是$dbusers数组，两种情况，如果未传值，则通过cookie name 读取，未设置，则报错，如果有传值，必须是数字存在的id。  
# {#dbviews#$tid(必须),$view(必须)}
浏览量更新功能。//两个函数固定,tid 和 view两个字段函数。  
# {#dbimgurl#函数(必须)}
头像处理函数，返回函数$dbimgurl  
# {#dbclassify#函数(必须)}  
分类处理，返回函数$dbclassify已经解析好了的。  
# {#dbchecklogin}
检测是否登陆。  
# {#dbwritetext#标题函数,内容函数}
文章写入数据。  
# {#dbwritereply#函数(内容),$tid}
写回复，函数必须。  
# {#dbchats}
读取chat表，处理过程，没有返回值，虚结合foreach使用。  
# {#dbwritechat#$chat(必须)}
写入聊天函数必须。  
# {#dbindexchats}
首页聊天3条显示，无返回值，需结合foreach使用。  
# {#dbadd,数组,方式}
添加数据，方式可选择 xu xiu 固定  
数组:续写["内容"]，修改["内容","标题"]  
# {#dbqxusers}
固定返回$dbqxusers数组，权限组，同dbusers  
# {#dbdelete#$tid(必须),方式(选择)}
删除数据。需要选择方式，待选 reply text  
# {#dbmove#$tid(必须),$move(必须)}
移动文章。  
# {#dbupload#$files[名字],$数组}
上传文件，数组传值[type,tid,内容]  
# {#dbsearch#函数(必须)}
论坛搜索支持模糊搜过，id tid   
# {#dbmessages#$fs}
信箱方式综合显示，$fs 为wd未读 yd已读 at爱特。没有返回值，需要配合foreach使用，类似，dbindexlists模板。  
# {#dbmesreads}
信箱内容读取，直接固定返回$dbmesreads;直接使用  
# {#dbmesreply#$s_id,内容}
信箱发信息。传入接受id，和内容。  
# {#dbmesnums}
直接返回函数$dbmesnums,输出未读信息条数。  
# {#dbupduser#$garr(数组)} 
修改用户信息，包括管理权限，元素较多，传入数组。  
# {#dbset#$函数}
使用同move,功能设置帖子状态  
# {#dbtopicstates#$函数}
传值判断函数，从而显示文章状态。直接返回固定函数$dbtopicstates，配合使用。  