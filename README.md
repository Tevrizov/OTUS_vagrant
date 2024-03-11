Обновление ядра



1. Подключаемся по ssh к созданной виртуальной машины:
для подключения к ВМ вводим vagrant ssh

##################################################################################################################################################################

2. Проверяем текущую версию ядра:
uname -r

--
[vagrant@kernel-update ~]$ uname -r
4.18.0-516.el8.x86_64

##################################################################################################################################################################

3. Подключим репозиторий, откуда возьмём необходимую версию ядра:
sudo yum install -y https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm 

--
[vagrant@kernel-update ~]$ sudo yum install -y https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm 
Failed to set locale, defaulting to C.UTF-8
CentOS Stream 8 - AppStream                                                                                                                                             7.5 kB/s | 4.4 kB     00:00    
CentOS Stream 8 - BaseOS                                                                                                                                                5.5 kB/s | 3.9 kB     00:00    
CentOS Stream 8 - Extras                                                                                                                                                6.8 kB/s | 2.9 kB     00:00    
CentOS Stream 8 - Extras common packages                                                                                                                                6.1 kB/s | 3.0 kB     00:00    
Extra Packages for Enterprise Linux 8 - x86_64                                                                                                                           24 kB/s |  29 kB     00:01    
Extra Packages for Enterprise Linux 8 - Next - x86_64                                                                                                                    26 kB/s |  35 kB     00:01    
elrepo-release-8.el8.elrepo.noarch.rpm                                                                                                                                  7.9 kB/s |  13 kB     00:01    
Dependencies resolved.
==========================================================================================================================================================================
 Package                                           Architecture                              Version                                              Repository                                       Size
==========================================================================================================================================================================
Installing:
 elrepo-release                                    noarch                                    8.3-1.el8.elrepo                                     @commandline                                     13 k

Transaction Summary
==========================================================================================================================================================================
Install  1 Package

Total size: 13 k
Installed size: 5.0 k
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                1/1 
  Installing       : elrepo-release-8.3-1.el8.elrepo.noarch                                                                                                                                         1/1 
  Verifying        : elrepo-release-8.3-1.el8.elrepo.noarch                                                                                                                                         1/1 

Installed:
  elrepo-release-8.3-1.el8.elrepo.noarch                                                                                                                                                                

Complete!

##################################################################################################################################################################


4. Установим последнее ядро из репозитория elrepo-kernel:
sudo yum --enablerepo elrepo-kernel install kernel-ml -y

*Параметр --enablerepo elrepo-kernel указывает что пакет ядра будет запрошен из репозитория elrepo-kernel.
Уже на этом этапе можно перезагрузить нашу виртуальную машину и выбрать новое ядро при загрузке ОС.

--
[vagrant@kernel-update ~]$ sudo yum --enablerepo elrepo-kernel install kernel-ml -y
Failed to set locale, defaulting to C.UTF-8
ELRepo.org Community Enterprise Linux Repository - el8                                                                                                                  114 kB/s | 203 kB     00:01    
ELRepo.org Community Enterprise Linux Kernel Repository - el8                                                                                                           791 kB/s | 2.2 MB     00:02    
Dependencies resolved.
==========================================================================================================================================================================
 Package                                            Architecture                            Version                                                Repository                                      Size
==========================================================================================================================================================================
Installing:
 kernel-ml                                          x86_64                                  6.7.9-1.el8.elrepo                                     elrepo-kernel                                  121 k
Installing dependencies:
 kernel-ml-core                                     x86_64                                  6.7.9-1.el8.elrepo                                     elrepo-kernel                                   39 M
 kernel-ml-modules                                  x86_64                                  6.7.9-1.el8.elrepo                                     elrepo-kernel                                   34 M

Transaction Summary
==========================================================================================================================================================================
Install  3 Packages

Total download size: 73 M
Installed size: 115 M
Downloading Packages:
(1/3): kernel-ml-6.7.9-1.el8.elrepo.x86_64.rpm                                                                                                                          202 kB/s | 121 kB     00:00    
(2/3): kernel-ml-modules-6.7.9-1.el8.elrepo.x86_64.rpm                                                                                                                  4.3 MB/s |  34 MB     00:07    
(3/3): kernel-ml-core-6.7.9-1.el8.elrepo.x86_64.rpm                                                                                                                     3.0 MB/s |  39 MB     00:12    
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                   5.4 MB/s |  73 MB     00:13     
ELRepo.org Community Enterprise Linux Kernel Repository - el8                                                                                                           1.6 MB/s | 1.7 kB     00:00    
Importing GPG key 0xBAADAE52:
 Userid     : "elrepo.org (RPM Signing Key for elrepo.org) <secure@elrepo.org>"
 Fingerprint: 96C0 104F 6315 4731 1E0B B1AE 309B C305 BAAD AE52
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-elrepo.org
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                1/1 
  Installing       : kernel-ml-core-6.7.9-1.el8.elrepo.x86_64                                                                                                                                       1/3 
  Running scriptlet: kernel-ml-core-6.7.9-1.el8.elrepo.x86_64                                                                                                                                       1/3 
  Installing       : kernel-ml-modules-6.7.9-1.el8.elrepo.x86_64                                                                                                                                    2/3 
  Running scriptlet: kernel-ml-modules-6.7.9-1.el8.elrepo.x86_64                                                                                                                                    2/3 
  Installing       : kernel-ml-6.7.9-1.el8.elrepo.x86_64                                                                                                                                            3/3 
  Running scriptlet: kernel-ml-core-6.7.9-1.el8.elrepo.x86_64                                                                                                                                       3/3 
dracut: Disabling early microcode, because kernel does not support it. CONFIG_MICROCODE_[AMD|INTEL]!=y
dracut: Disabling early microcode, because kernel does not support it. CONFIG_MICROCODE_[AMD|INTEL]!=y

  Running scriptlet: kernel-ml-6.7.9-1.el8.elrepo.x86_64                                                                                                                                            3/3 
  Verifying        : kernel-ml-6.7.9-1.el8.elrepo.x86_64                                                                                                                                            1/3 
  Verifying        : kernel-ml-core-6.7.9-1.el8.elrepo.x86_64                                                                                                                                       2/3 
  Verifying        : kernel-ml-modules-6.7.9-1.el8.elrepo.x86_64                                                                                                                                    3/3 

Installed:
  kernel-ml-6.7.9-1.el8.elrepo.x86_64                           kernel-ml-core-6.7.9-1.el8.elrepo.x86_64                           kernel-ml-modules-6.7.9-1.el8.elrepo.x86_64                          

Complete!

##################################################################################################################################################################

5. Обновляем конфигурацию загрузчика:
vagrant@kernel-update ~]$ sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
done
[vagrant@kernel-update ~]$

##################################################################################################################################################################

6. Выбираем загрузку нового ядра по-умолчанию:
sudo grub2-set-default 0

##################################################################################################################################################################

7. Перезагружаем нашу виртуальную машину с помощью команды sudo reboot

##################################################################################################################################################################

8. После перезагрузки снова проверяем версию ядра:

tep@tep-home:~/tmpvm$ vagrant ssh
Last login: Mon Mar 11 08:14:42 2024 from 10.0.2.2
[vagrant@kernel-update ~]$ uname -r
6.7.9-1.el8.elrepo.x86_64
[vagrant@kernel-update ~]$ 

##################################################################################################################################################################


ИТОГ:

было:
4.18.0-516.el8.x86_64
стало:
6.7.9-1.el8.elrepo.x86_64

