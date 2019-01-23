# Top processes

Inputting '`t`' can get top processes information:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/top_processes.jpg)

By default, the processes are sorted and displayed in CPU utilization. The `%CPU` and `min/max Faults` fields are read and calculated from `/proc/[pid]/stat`, and `Size`, `Res` ... are got `/proc/[pid]/statm`.  

There are other modes for top processes. E.g., pressing `1` can switch to "`Base`" mode:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/top_processes_base.jpg) 

For detailed information of every process, please refer [/proc/[pid]/stat](http://man7.org/linux/man-pages/man5/proc.5.html).