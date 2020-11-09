## HOMESTEAD ON WSL2

project issue: https://github.com/laravel/homestead/issues/1484

**Main setup**
```
> cd Code/homestead
> sudo ./bin/wsl-init 
> [sudo] password for halo:
> What is your WSL user name? 
> halo 
> What is your WSL user group? 
> (Same as username if you're unsure) halo 
> Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [107 kB]
etc...
```
 **Create Sites from Homestead Configuration**

Add a new top level configuration item in your  `Homestead.yaml`  configuration such as:
```
wsl_sites:
    -   map: vcdt.test
        to: /mnt/c/Users/halo/Code/vcdt/public
```

```
$ ./bin/homestead wsl:create-sites
```
The sites from  `wsl_sites`  will be created.

**Create Databases from Homestead Configuration**

WSL will read from the normal  `databases`  configuration in  `Homestead.yaml`
```
databases:
    - homestead
    - vcdt
    - laminas
```

```
$ ./bin/homestead wsl:create-databases
mysql: [Warning] Using a password on the command line interface can be insecure.
mysql: [Warning] Using a password on the command line interface can be insecure.
mysql: [Warning] Using a password on the command line interface can be insecure.
mysql: [Warning] Using a password on the command line interface can be insecure.
mysql: [Warning] Using a password on the command line interface can be insecure.
mysql: [Warning] Using a password on the command line interface can be insecure.
WSL Databases have been created!
```
The databases from  `databases`  will be created.


change php version
`sudo update-alternatives --config php`




    ip addr show`enter code here` eth0
    ip addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
    netstat -nr | gerp '^0\.0\.0\.0' | awk '{print $2}'  

https://github.com/microsoft/WSL/issues/4210#issuecomment-648570493
I give you a new idea: Instead of changing the IP, add a designated IP.

In Windows 10, run CMD or Powershell with administrator privilege, and then execute the following two commands:

:: Add an IP address in Ubuntu, 192.168.50.16, named eth0:1  
`wsl -d Ubuntu -u root ip addr add 192.168.50.16/24 broadcast 192.168.50.255 dev eth0 label eth0:1`

:: Add an IP address in Win10, 192.168.50.88  
`netsh interface ip add address "vEthernet (WSL)" 192.168.50.88 255.255.255.0`

In the future, you will use 192.168.50.16 when you access Ubuntu, and 192.168.50.88 when you access Win10.  
You can save the above two lines of commands as a .bat file, and then put it into the boot area, and let it execute automatically every time.


**wsl commands**

https://docs.microsoft.com/en-us/windows/wsl/reference


 run specific distro :  `wsl -d Ubuntu18`
 set default distro :  `wsl -s Ubuntu18`
 list wsl distros :  `wsl --list --verbose`
 run command on specific distro : 

      wsl -d Ubuntu-20.04 -u root service nginx start
      wsl -d Ubuntu-20.04 -u root service php7.4-fpm start
      wsl -d Ubuntu-20.04 -u root service mysql start
