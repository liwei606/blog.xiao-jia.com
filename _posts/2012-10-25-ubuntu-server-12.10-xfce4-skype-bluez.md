title: 因为 bluez 不能安装 Skype
tags: ubuntu, skype, bluez
time: 2012-10-25 16:27:55

今天在 Ubuntu Server 12.10 (64 bit) 下面装 Skype，从官网下了 deb 包之后，怎么也装不上：

	$ sudo dpkg -i skype-ubuntu_4.0.0.8-1_amd64.deb 
	Selecting previously unselected package skype.
	(Reading database ... 250805 files and directories currently installed.)
	Unpacking skype (from skype-ubuntu_4.0.0.8-1_amd64.deb) ...
	dpkg: dependency problems prevent configuration of skype:
	 skype depends on ia32-libs; however:
	  Package ia32-libs is not installed.
	
	dpkg: error processing skype (--install):
	 dependency problems - leaving unconfigured
	Processing triggers for desktop-file-utils ...
	Errors were encountered while processing:
	 skype

上面这个错误只是多次尝试中的冰山一角。`ia32-libs` 依赖于 `ia32-libs-multiarch`，进而依赖于 `bluez-alsa:i386`，最后依赖于 `bluez`。究其原因，就是 `bluez` 装不上：

	$ sudo apt-get install bluez
	Reading package lists... Done
	Building dependency tree       
	Reading state information... Done
	Suggested packages:
	  bluez-hcidump
	The following NEW packages will be installed:
	  bluez
	0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
	Need to get 0 B/985 kB of archives.
	After this operation, 2,567 kB of additional disk space will be used.
	Selecting previously unselected package bluez.
	(Reading database ... 253342 files and directories currently installed.)
	Unpacking bluez (from .../bluez_4.101-0ubuntu6_amd64.deb) ...
	Processing triggers for man-db ...
	Processing triggers for ureadahead ...
	Setting up bluez (4.101-0ubuntu6) ...
	reload: Unknown instance: 
	invoke-rc.d: initscript dbus, action "force-reload" failed.
	start: Job failed to start
	invoke-rc.d: initscript bluetooth, action "start" failed.
	dpkg: error processing bluez (--configure):
	 subprocess installed post-installation script returned error exit status 1
	Processing triggers for ureadahead ...
	Errors were encountered while processing:
	 bluez
	E: Sub-process /usr/bin/dpkg returned an error code (1)

Google 了一下，毫无头绪，好不容易找到一个帖子，试了一下，果然就行了：

	$ sudo mv /usr/sbin/bluetoothd /usr/sbin/bluetoothd-backup
	$ sudo ln -s /bin/true /usr/sbin/bluetoothd

之后再重新安装 `bluez` 就可以了，因为 `/usr/sbin/bluetoothd` 已经是 `/bin/true` 了。

之前都没有遇到这个问题，不知道这次是为什么，可能是 12.10 的缘故吧。先记在这里，万一有人遇到同样的问题也能快点解决。

