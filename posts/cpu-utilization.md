# CPU utilization

During the home screen, you can press '`c`' to get CPU utilization chart:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/cpu_utilization.jpg)

CPU utilization metrics are read from `/proc/stat` file:  

	$ cat /proc/stat
	cpu  69329351 1546 2133140 1777137470 701736 266457 200025 0 0 0
	cpu0 1381282 4 75089 16197830 12424 6417 107331 0 0 0
	cpu1 1368760 13 67306 16310343 9995 6896 19434 0 0 0
	......

After `Linux 2.6`, every CPU row has `10` items: `user`, `nice`, `system`, `idle`, `iowait`, `irq`, `softirq`, `steal`, `guest` and `guest_nice` (For the meaning of every metric, please refer [/proc](http://man7.org/linux/man-pages/man5/proc.5.html) document), and the value is measured in units of `USER_HZ`. The first row is the total statistics of the system, and followings are the information of every CPU. In the screen, `User%` consists of `user` and `nice`, `Sys%` is composed of `system`, `irq` and `softirq`, etc. Please refer `nomon` code:  

			......
			cpu_user = RAW(user) + RAW(nice);
			cpu_sys =
			RAW(sys) + RAW(irq) + RAW(softirq); 
			/* + RAW(guest) + RAW(guest_nice); these are in addition to the 100% */
			cpu_wait = RAW(wait);
			cpu_idle = RAW(idle);
			cpu_steal = RAW(steal);

			cpu_sum =
			cpu_idle + cpu_user + cpu_sys + cpu_wait +
			cpu_steal; 
			......

BTW, press '`l`' can display CPU utilization in `long-term` format, which can help you get the overview of  system better in real time:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/cpu_utilization_long_term.jpg)

 
