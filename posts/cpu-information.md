# CPU information

When you launch `nmon` in the terminal, it will display following home screen:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/homescreen.jpg)  

Besides usage tip, the screen mainly show the CPU information of current system. The CPU information is obtained from `/proc/cpuinfo` file:  

	# cat /proc/cpuinfo
	processor       : 0
	vendor_id       : GenuineIntel
	cpu family      : 6
	model           : 23
	model name      : Intel(R) Core(TM)2 Duo CPU     P8700  @ 2.53GHz
	stepping        : 10
	microcode       : 0xa07
	cpu MHz         : 1596.311
	cache size      : 3072 KB
	physical id     : 0
	......

and `lscpu` command output:  
	
	void lscpu_init()
	{
		......
	
		if (lscpu_available == 1)
		return;
		pop = popen("/usr/bin/lscpu 2>/dev/null", "r");
		if (pop != NULL) {
			......
		}
	}

But in fact, `lscpu` command also gets value from `/proc/cpuinfo` (please refer [code](https://github.com/karelzak/util-linux/blob/200769b6c0dff6863089ea2a9ff4ea9ccbd15d0f/sys-utils/lscpu.c#L405)).  

The `ProcessorChips` is equivalent to `lscpu` output's `Sockets`, which identifies the number of "physical CPUs"; `PhyscalCores` is equivalent to `lscpu` output's `Cores`; `Hyperthreads` to `Thrds` and `VirtualCPUs` to `CPU`.`VirtualCPUs` is also named as "logical CPUs", which is equal to "`Sockets` * `Cores` * `Thrds`" (`2` * `26` * `2` = `104`).

