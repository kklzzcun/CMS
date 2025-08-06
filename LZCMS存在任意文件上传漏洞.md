LZCMS 是一个国内开发的轻量级内容管理系统（CMS），基于 PHP 和 MySQL，适用于企业官网、博客、新闻网站等类型的网站建设。其设计理念强调简洁、轻便、易于部署，因此被一些小型企业和个人站长广泛采用

发现者:周家洋

经代码审计发现在application/common/model/Upload.php中第19行仅获取了上传的文件，但没有对文件类型进行任何验证，成功上传后直接在数据包中返回路径。攻击者可以上传任何类型的文件，包括 `.php` 或其他可能被执行的恶意文件

![image-20250705231127920](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705231127920.png)

![image-20250705232533041](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705232533041.png)

登录到后台后，源码分享的源码分享处可直接上传，根据返回的路径直接访问即可

![image-20250705231334849](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705231334849.png)





![image-20250705232249324](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705232249324.png)

![image-20250705232811177](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705232811177.png)

































