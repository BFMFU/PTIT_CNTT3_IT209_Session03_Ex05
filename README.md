root@azvps-dynamic:~# sudo mkdir -p /opt/my-app/html
sudo mkdir -p /opt/my-app/logs
root@azvps-dynamic:~# sudo nano /opt/my-app/html/index.html
root@azvps-dynamic:~# sudo chown -R devops:www-data /opt/my-app
root@azvps-dynamic:~# ls -la /opt/my-app/
total 16
drwxr-xr-x 4 devops www-data 4096 Oct  2 08:17 .
drwxr-xr-x 3 root   root     4096 Oct  2 08:17 ..
drwxr-xr-x 2 devops www-data 4096 Oct  2 08:18 html
drwxr-xr-x 2 devops www-data 4096 Oct  2 08:17 logs
root@azvps-dynamic:~# sudo chmod 750 /opt/my-app/
root@azvps-dynamic:~# sudo chmod 750 /opt/my-app/html
root@azvps-dynamic:~# sudo chmod 750 /opt/my-app/logs
root@azvps-dynamic:~# sudo find /opt/my-app/html -type f -exec chmod 640 {} \;
root@azvps-dynamic:~# sudo nano /etc/nginx/sites-available/my-app
root@azvps-dynamic:~# sudo ln -s /etc/nginx/sites-available/my-app /etc/nginx/sites-enabled/my-app
root@azvps-dynamic:~# sudo rm /etc/nginx/sites-enabled/default
root@azvps-dynamic:~# sudo nginx -t
nginx: [warn] conflicting server name "_" on 0.0.0.0:80, ignored
nginx: [warn] conflicting server name "_" on [::]:80, ignored
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
root@azvps-dynamic:~# sudo systemctl reload nginx
root@azvps-dynamic:~# su - devops
devops@azvps-dynamic:~$ whoai
Command 'whoai' not found, did you mean:
  command 'whoami' from deb coreutils (8.32-4.1ubuntu1.3)
Try: apt install <deb name>
devops@azvps-dynamic:~$ whoami
devops
devops@azvps-dynamic:~$ echo "UPDATE TEST" >> /opt/my-app/html/index.html
devops@azvps-dynamic:~$ tail /opt/my-app/html/index.html
<html>
<head>
    <title>My App</title>
</head>
<body>
    <h1>Welcome to My App</h1>
    <p>Nginx is running successfully.</p>
</body>
</html>
UPDATE TEST
devops@azvps-dynamic:~$ curl http://localhost
<!DOCTYPE html>
<html>
<head>
    <title>My App</title>
</head>
<body>
    <h1>Welcome to My App</h1>
    <p>Nginx is running successfully.</p>
</body>
</html>
UPDATE TEST
devops@azvps-dynamic:~$ ls -la /opt/my-app/
total 16
drwxr-x--- 4 devops www-data 4096 Oct  2 08:17 .
drwxr-xr-x 3 root   root     4096 Oct  2 08:17 ..
drwxr-x--- 2 devops www-data 4096 Oct  2 08:18 html
drwxr-x--- 2 devops www-data 4096 Oct  2 08:20 logs
devops@azvps-dynamic:~$
