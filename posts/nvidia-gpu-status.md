# NVIDIA GPU status  

`nmon` can also be used to monitor `NVIDIA` GPU status. You need to compile code with `NVIDIA_GPU` macro enabled and linked with `nvidia-ml` library. E.g.:  

	$ cc -o nmon_x86_debian3 lmon.c -g -Wall -D JFS -D GETUSER -D LARGEMEM -D NVIDIA_GPU -lncurses -lm -g -D X86 -lnvidia-ml

Press '`a`' or '`E`' can show GPU status screen:  

![image](https://raw.githubusercontent.com/NanXiao/read-nmon-code-to-learn-analyzing-linux-performance/master/images/nvidia_gpu_status.jpg)

`gpu_init()` function is used to get GPU information:  

	void gpu_init()
	{
	    int i;
	    nvmlReturn_t nvres;
	    if ((nvres = nvmlInit()) != NVML_SUCCESS) {
	        printf("nvmlInit failed %d\n", nvres);
	        return;
	    }
	    ......
	    if ((nvres = nvmlDeviceGetCount(&gpu_devices)) != NVML_SUCCESS) {
	        printf("nvmlDeviceGetCount failed %d\n", nvres);
	        return;
	    }
	    if (gpu_devices > 4)
	        gpu_devices = 4;
	    ......
	}  
You can see `gpu_init()` just utilizes [NVML](https://developer.nvidia.com/nvidia-management-library-nvml) APIs to get GPU's knowledge. But there are also limitations: such as `nmon` can only support `4` GPUs, the metrics are not abundant, etc. Since source code is here, you can customize it if you want. 


