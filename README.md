LZCMS is a lightweight Content Management System (CMS) based on PHP and MySQL, suitable for building websites such as corporate portals, blogs, and news platforms. Its design philosophy emphasizes simplicity, lightweight structure, and ease of deployment, making it widely adopted by small businesses and individual webmasters.

Discovered by: Jiayang Zhou 

Through code auditing, a ThinkPHP 5.x log leakage vulnerability was discovered in LZCMS.
Vulnerable file path: thinkphp/library/think/log/driver/File.php

At line 43, log files are saved using the format: {path}/{year-month}/{day}.log. If no access control is configured, attackers can enumerate log file paths via URL.

At line 67, information such as the current request URI (including GET parameters), execution time, throughput, memory usage, number of files (useful for load analysis), request method, server address, client IP, log level, and log content is written to the logs.
If the $log contains $_POST data, exception stack traces, database configurations, etc., all of it will be recorded into the log file.

From lines 80 to 83, logs of different severity levels are written separately without any access control.

Relevant code snippet is as follows

![1.png](https://raw.githubusercontent.com/kklzzcun/CMS/main/assets/1.png)
