# Memory utilization

Inputting '`m`' can show memory utilization:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/mem_utilization.jpg)

Memory utilization metrics are parsed from `/proc/meminfo` file (For the meaning of every metric, please refer [/proc](http://man7.org/linux/man-pages/man5/proc.5.html) document):  

	$ cat /proc/meminfo
	MemTotal:       196664796 kB
	MemFree:        160337264 kB
	MemAvailable:   177147604 kB
	Buffers:         1098864 kB
	Cached:         16097336 kB
	SwapCached:            0 kB
	Active:         19958356 kB
	Inactive:       13062956 kB
	......

Please beware that in `proc_mem()` function, some metrics are only valid if `LARGEMEM` macro is defined (Refer this [document](https://wiki.debian.org/Hugepages) to know what is "Huge pages".):  

	void proc_mem()
	{
	    ......
	#ifdef LARGEMEM
	    ......
	    p->mem.hugetotal = proc_mem_search("HugePages_Total");
	    p->mem.hugefree = proc_mem_search("HugePages_Free");
	    p->mem.hugesize = proc_mem_search("Hugepagesize");
	#else
	    p->mem.bigfree = proc_mem_search("BigFree");
	#endif /*LARGEMEM*/
	}

You can also press '`V`' to get "virtual memory" statistics:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/virtual_memory.jpg)  

The information is read from `/proc/vmstat`:  

	$ cat /proc/vmstat
	nr_free_pages 34583276
	nr_zone_inactive_anon 77718
	nr_zone_active_anon 8755682
	nr_zone_inactive_file 2972621
	nr_zone_active_file 1707733
	nr_zone_unevictable 56
	nr_zone_write_pending 19037
	nr_mlock 56
	......

and processed by `read_vmstat()` function.