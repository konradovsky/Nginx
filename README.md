# Nginix
Learning nginix

## Basic NGINIX instalation

#### 1. Update your system  
```sudo apt-get update```  
```sudo apt-get upgrade```  

#### 2. Install standard version of NGINX without any modules with APT package manager  
```sudo apt-get install nginx```  

#### 3. After installing we can check if the nginx process run by:  
```ps aux | grep ngnix```  

#### 4. Next we can check the if and port of the server  
```ifconfig```  

## Instalation with modules  


#### 1. Update your system  
```sudo apt-get update```  
```sudo apt-get upgrade```  

#### 2. Download the latest stable version from [nginix.org](https://nginx.org/en/download.html)
``` wget https://nginx.org/download/nginx-1.15.9.tar.gz ```  
Copy the link in the latest stable version and download it with wget or curl

#### 3. Extract the .tar.gz directory by typing 
```tar -zxvf nginx-1.15.tar.gz```  
then go to the extracted folder  
```cd nginx-1.15```

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

