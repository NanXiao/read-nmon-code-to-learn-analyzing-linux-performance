# File systems

Inputting '`j`' can get file systems information:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/file_systems.jpg)  

File systems information is stored in `/etc/mtab` file (Please refer [Wikipedia](https://en.wikipedia.org/wiki/Mtab)):  

	# cat /etc/mtab
	proc /proc proc rw,nosuid,nodev,noexec,relatime 0 0
	sys /sys sysfs rw,nosuid,nodev,noexec,relatime 0 0
	dev /dev devtmpfs rw,nosuid,relatime,size=1989392k,nr_inodes=497348,mode=755 0 0
	run /run tmpfs rw,nosuid,nodev,relatime,mode=755 0 0
	/dev/sda / ext4 rw,relatime 0 0
	securityfs /sys/kernel/security securityfs rw,nosuid,nodev,noexec,relatime 0 0
	tmpfs /dev/shm tmpfs rw,nosuid,nodev 0 0
	devpts /dev/pts devpts rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000 0 0
	......

This file is processed by `jfs_load()` function:  

	void jfs_load(int load)
	{
	    ......
	    mfp = setmntent("/etc/mtab", "r");
	    for (i = 0; i < JFSMAX && (mp = getmntent(mfp)) != NULL; i++) {
	        strncpy(jfs[i].device, mp->mnt_fsname, JFSNAMELEN);
	        strncpy(jfs[i].name, mp->mnt_dir, JFSNAMELEN);
	        strncpy(jfs[i].type, mp->mnt_type, JFSTYPELEN);
	        mp->mnt_fsname[JFSNAMELEN - 1] = 0;
	        mp->mnt_dir[JFSNAMELEN - 1] = 0;
	        mp->mnt_type[JFSTYPELEN - 1] = 0;
	    }
	    endmntent(mfp);
	    ......
	}

We should use dedicated functions: `setmntent()`, `getmntent()` and `endmntent()` to parse `/etc/mtab` file.