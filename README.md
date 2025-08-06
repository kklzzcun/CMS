LZCMS is a lightweight Content Management System (CMS) developed in China, based on PHP and MySQL, suitable for building various types of websites such as corporate portals, blogs, and news platforms. Its design emphasizes simplicity, lightweight architecture, and ease of deployment, making it widely adopted by small businesses and individual webmasters.

Discovered by: Zhou Jiayang

Through code auditing, it was found that in application/common/model/Upload.php, between lines 17 and 29, the code does not perform any validation on the uploaded file types. The uploaded content is saved directly, which allows attackers to upload HTML, PHP, JS, and other malicious files disguised as images, effectively bypassing file type restrictions.
![5.png](https://raw.githubusercontent.com/kklzzcun/CMS/main/assets/5.png)
After logging into the admin panel, visiting the URL:
http://x.x.x.x/index.php/admin/admin/edit.html
leads to the avatar upload functionality.
![6.png](https://raw.githubusercontent.com/kklzzcun/CMS/main/assets/6.png)
There is no restriction on the uploaded file type at this point, and the server returns the URL of the uploaded file. By intercepting the request and modifying filename=1.html and changing the Content-Type to text/html, then appending the XSS payload <sCriPt>alert(/xss/)</sCriPt> in the request body, the file can be uploaded successfully. Accessing the returned URL will trigger the alert popup.
![7.png](https://raw.githubusercontent.com/kklzzcun/CMS/main/assets/7.png)
![8.png](https://raw.githubusercontent.com/kklzzcun/CMS/main/assets/8.png)

