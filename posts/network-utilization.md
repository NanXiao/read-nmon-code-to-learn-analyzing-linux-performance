# Network utilization  

Inputting '`n`' can get network utilization:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/network_utilization.jpg)  

The statistics are read from `/proc/net/dev` file (processed by `proc_net` function):  

	$ cat /proc/net/dev
	Inter-|   Receive                                                |  Transmit
	 face |bytes    packets errs drop fifo frame compressed multicast|bytes    packets errs drop fifo colls carrier compressed
	  eno2:       0       0    0    0    0     0          0         0        0       0    0    0    0     0       0          0
	    lo: 61231535   54975    0    0    0     0          0         0 61231535   54975    0    0    0     0       0          0
	  eno1: 6123992486 37999646    0 92998    0     0          0    769601 54887394843 48055902    0    0    0     0       0          0

It is not difficult to comprehend meanings of every field (You can refer this [discussion](https://stackoverflow.com/questions/3521678/what-are-meanings-of-fields-in-proc-net-dev)).