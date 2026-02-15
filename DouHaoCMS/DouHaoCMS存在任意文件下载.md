（DouHaoCMS）是一个基于 PHP 和 MySQL 开发的轻量级开源内容管理系统（CMS）。它构建于 ThinkPHP 框架之上，主要用于快速开发企业网站、个人博客以及中小型信息展示网站。
该系统的设计强调代码结构的简洁性和部署的便捷性，为用户提供了文章管理、产品管理和系统配置等核心功能模块。

发现者：周家洋

DouHaoCMS 内容管理系统的数据库备份模块 (/app/Lib/Action/admin/backupAction.class.php) 存在严重的安全逻辑缺陷。
尽管该功能位于后台，但由于 download 接口未对用户输入的文件名参数进行路径标准化处理和合法性校验，攻击者（可以构造包含目录遍历符 (../) 的恶意请求，绕过应用目录限制，读取服务器文件系统上的任意文件。
该漏洞的严重性在于，攻击者可直接下载系统的核心配置文件（如数据库连接配置）和安装残留凭据，从而获得明文的数据库账号密码，导致整个站点数据资产完全沦陷


代码审计

Line 162 if(strpos($backup_name,"/"))这里过滤无效，在此if判断中若发现"/"在首位会返回0，被if判断为fals。导致过滤失效返回的是0只有if(strpos($backup_name, "/") !== false)才能绕过检查，而且就算有效只检查参数是否包含斜杠，却完全忽略了 file 参数,虽不是任意文件下载主因，但证明了安全检查的脆弱性
Line 165直接接收 file 参数，未限制 "../" 目录遍历符，也未限制文件后缀
Line 171将未经过滤的 $file 直接拼接到路径中
Line 172-178 致命逻辑错误！开发者使用了逻辑或 "||" 运算符：只要文件存在 (file_exists)，即允许下载，最终执行点：无视文件类型，直接输出系统敏感文件内容
![](https://raw.githubusercontent.com/kklzzcun/CMS/main/DouHaoCMS/assets/xz1.png)
漏洞复现 

Payload: 
http://Target/index.php?g=admin&m=backup&a=download&backup=.&file=../../install/Runtime/Data/temp_data.php 


成功下载并读取 temp_data.php 文件，内容包含数据库的明文账号密码和用户的账号密码

![](https://raw.githubusercontent.com/kklzzcun/CMS/main/DouHaoCMS/assets/xz2.png)
