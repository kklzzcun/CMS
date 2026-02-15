LZCMS 是一个国内开发的轻量级内容管理系统（CMS），基于 PHP 和 MySQL，适用于企业官网、博客、新闻网站等类型的网站建设。其设计理念强调简洁、轻便、易于部署，因此被一些小型企业和个人站长广泛采用

发现者:周家洋

登录后台后访问URL:http://x.x.x.x./index.php/admin/admin/edit.html处的头像上传，经代码审计发现

![image-20250701170455364](C:\Users\酸菜鱼\Desktop\CVE\lzcms\assets\image-20250701170455364.png)

此处没有对文件上传的类型做出限制，并且返回文件上传后的地址。

![image-20250701172205833](C:\Users\酸菜鱼\Desktop\CVE\lzcms\assets\image-20250701172205833.png)

![image-20250701171739145](C:\Users\酸菜鱼\Desktop\CVE\lzcms\assets\image-20250701171739145.png)

上传图片处http://x.x.x..x/index.php/admin/upload/upimage.html，抓包修改filename=1.html再修改text/html,在下面添加xsspayload：<sCriPt>alert(/xss/)</sCriPt>放包后根据返回的地址拼接访问即可触发弹窗。

![image-20250701172814951](C:\Users\酸菜鱼\Desktop\CVE\lzcms\assets\image-20250701172814951.png)

![image-20250701172604813](C:\Users\酸菜鱼\Desktop\CVE\lzcms\assets\image-20250701172604813.png)



























































