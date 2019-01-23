# The end

It is time to wrap up this journey now. After going through the code, I summarize the steps of implementing a home-brew performance monitor tool:  

a) Get the performance raw data: `/proc` is a treasure for the whole system while `/proc/[pid]` for a specified process. If you want to observer proprietary devices (e.g., `NVIDIA` GPU), please refer vendor APIs;  

b) Understand and parse data;  

c) Display them. You can choose primitive `ncurses` or more fancy modern `GUI` libraries.  

If you are learning a new programming language, reinventing a monitor wheel may be a good exercise, isn't it?   

P.S., if this small project gives you little help, please consider give it a star in [github](https://github.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance). :-)