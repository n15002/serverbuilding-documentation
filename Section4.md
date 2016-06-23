RedMineのインストール
-----

ここ見ればできんじゃね
http://blog.redmine.jp/articles/3_2/install/centos/

`sudo curl -O https://cache.ruby-lang.org/pub/ruby/2.2/ruby-2.2.5.tar.gz -x https://172.16.40.1:8888`


```
~/k/ansible-test ❯❯❯ sudo vagrant destroy
The provider 'virtualbox' that was requested to back the machine
'default' is reporting that it isn't usable on this system. The
reason is shown below:

VirtualBox is complaining that the kernel module is not loaded. Please
run `VBoxManage --version` or open the VirtualBox GUI to see the error
message which should contain instructions on how to fix this error.
~/k/ansible-test ❯❯❯ VBoxManage --version                                                                               ⏎
WARNING: The vboxdrv kernel module is not loaded. Either there is no module
         available for the current kernel (4.4.0-24-generic) or it failed to
         load. Please recompile the kernel module and install it by

           sudo /sbin/rcvboxdrv setup

         You will not be able to start VMs until this problem is fixed.
5.0.20r106931
~/k/ansible-test ❯❯❯ sudo /sbin/rcvboxdrv setup                                                                     ⏎
Stopping VirtualBox kernel modules ...done.
Recompiling VirtualBox kernel modules ...done.
Starting VirtualBox kernel modules ...done.
~/k/ansible-test ❯❯❯ VBoxManage --version
5.0.20r106931
```

sudo vi ~/.subversion/servers
