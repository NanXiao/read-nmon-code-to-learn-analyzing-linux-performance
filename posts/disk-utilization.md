# Disk utilization

Inputting '`d`' can get disk utilization:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/disk_utilization.jpg)  

The `proc_disk()` function is like this:  

	void proc_disk(double elapsed)
	{
	    struct stat buf;
	    int ret;
	    if (disk_mode == 0) {
	        ret = stat("/proc/diskstats", &buf);
	        if (ret == 0) {
	            disk_mode = DISK_MODE_DISKSTATS;
	        } else {
	            ret = stat("/proc/partitions", &buf);
	            ......
	        }
	        ......
	}

After `Linux 2.6`, `/proc/diskstats` replaced `/proc/partitions`. My `Linux` kernel's version is `4.19.4`, and the `/proc/diskstats` is like following:  

	$ cat /proc/diskstats
	   8       0 sda 24517099 658117 3634832978 137524335 5161201 1899656 2471640416 126499269 0 15834950 222007107 0 0 0 0
	   8       1 sda1 24517060 658117 3634830626 137524328 5147969 1899656 2471640416 126443415 0 15730970 221884500 0 0 0 0
	......

While `/proc/partitions` is very slim:  

	$ cat /proc/partitions
	major minor  #blocks  name
	
	   8        0 1000204632 sda
	   8        1 1000203608 sda1
	......

For every field's meaning of `/proc/diskstats`, you can refer [I/O statistics fields](https://www.kernel.org/doc/Documentation/iostats.txt). BTW, the "`Transfers`" in above image refers the sum of read and write operations:  

    void proc_diskstats(double elapsed)
    {
        ......
        p->dk[i].dk_xfers = p->dk[i].dk_reads + p->dk[i].dk_writes;
        ......
    }



