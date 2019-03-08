# Nginix
Learning nginix


## # Installation

### Basic NGINIX instalation

#### 1. Update your system  
```sudo apt-get update```  
```sudo apt-get upgrade```  

#### 2. Install standard version of NGINX without any modules with APT package manager  
```sudo apt-get install nginx```  

#### 3. After installing we can check if the nginx process run by:  
```ps aux | grep nginx```  

#### 4. Next we can check the if and port of the server  
```ifconfig```  

------

### Instalation with modules  

#### 1. Update your system  
```sudo apt-get update```  
```sudo apt-get upgrade```  

#### 2. Download the latest stable version from [nginix.org](https://nginx.org/en/download.html)
``` wget https://nginx.org/download/nginx-1.15.9.tar.gz ```  
Copy the link in the latest stable version and download it with wget or curl

#### 3. Extract the .tar.gz directory by typing 
```tar -zxvf nginx-1.15.9.tar.gz```  
then go to the extracted folder  
```cd nginx-1.15.9```

#### 4. Configure the downloaded project

  ##### 4.1. Install the compiler  
```sudo apt-get install build-essential```

  ##### 4.2. Run the configure script
```./configure```  

  ##### 4.3. We gonna get some error which we have to handle manualy  
Search the missed modules and install them with APT package manager. In this case there are:  
```sudo apt-get install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev```

  ##### 4.4. Run the configure script again
```./configure```  
Now there shouldn't be any errors

#### 5. Configure the flags for custom nginx (modules)
Custom cofig  
```./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module```  

#### 6. Now we can compile the config with  
```make```  

#### 7. After compiling the config we can now install
```make install```

#### 7. We can now check if we have the installed version aviable
```nginx -V```

#### 8. Run the nginx
```nginx```

#### 9. Check if the nginx process is run  
```ps aux | grep nginx```  
  
## # Adding an Nginix Service  
[Site with systemd init file](https://www.nginx.com/resources/wiki/start/topics/examples/initscripts/)  

#### 1. Create a init file with
```nano /lib/systemd/system/nginx.service```  
and then copy the init script inside and change the PIDFile, ExecStartPre, ExecStart for your paths
```[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStartPre=/usr/bin/nginx -t
ExecStart=/usr/bin/nginx
ExecReload=/usr/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

### 2. Start and check the status  

```systemctl start nginx```  
```systemctl status nginx```

### 3. Enable startup on boot  

```systemctl enable nginx```  
  
 

## # Creating a Virtual Host

### 1. Edit the nginx.conf file

```nano nginx-1.15.9/conf/nginx.conf```  

### 2. Add the demo customization

Port 80  is for HTTP requests  
Port 443 is for HTTPS requests  

```
events {}

http {
    listen: 80;
    server_name: 178.128.197.101;

    root: /sites/demo;
}
```

### 3. Reload nginx  
If you want to check if the syntax is ok you can use  

```nginix -t```  

Next we can restart or reload the server, restarting means that the nginx is shutted down and then booted up again, reload just checks if the new file is ok an then it reloades the nginx without shutiing it down.   

```systemctl reload nginix```


