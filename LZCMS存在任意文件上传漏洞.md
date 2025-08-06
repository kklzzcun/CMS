LZCMS is a lightweight Content Management System (CMS) based on PHP and MySQL, suitable for building various types of websites such as corporate portals, blogs, and news sites. Its design philosophy emphasizes simplicity, lightweight architecture, and ease of deployment, making it widely adopted by small businesses and individual webmasters.

Discovered by: Jiayang Zhou

Through code auditing, it was found that in application/common/model/Upload.php at line 19, the uploaded file is retrieved, but there is no validation of the file type. Once the upload is successful, the file path is directly returned in the response. An attacker could upload any type of file, including .php or other potentially executable malicious files.

![image-20250705231127920](https://raw.githubusercontent.com/kklzzcun/CMS/main/assets/image-20250705231127920.png)

![image-20250705232533041](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705232533041.png)


After logging into the admin panel, source code can be directly uploaded in the "Source Code Sharing" section. The uploaded file can then be accessed directly using the returned path.



![image-20250705231334849][(C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705231334849.png)](https://github.com/kklzzcun/CMS/raw/main/assets/image-2025070523134849.png)





![image-20250705232249324](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705232249324.png)

![image-20250705232811177](C:\Users\酸菜鱼\Desktop\CVE\lzcms3\assets\image-20250705232811177.png)



































