# Android Debug Bridge (adb)

## System Properties

| Information           | Command                                      |
| --------------------- | -------------------------------------------- |
| Build Version Release | `adb shell getprop ro.build.version.release` |
| Build Version SDK     | `adb shell getprop ro.build.version.sdk`     |
| Product Model         | `adb shell getprop ro.product.model`         |
| Product Brand         | `adb shell getprop ro.product.brand`         |
| Serial Number         | `adb shell getprop ro.serialno`              |
| IMEI                  | `adb shell dumpsys iphonesubinfo`            |

## Cat something

| Information         | Command                                      |
| ------------------- | -------------------------------------------- |
| MAC Address         | `adb shell cat /sys/class/net/wlan0/address` |
| Memory Information  | `adb shell cat /proc/meminfo`                |
| SD Card             | `adb shell df /sdcard`                       |
| Internal Storage    | `adb shell df /data`                         |
| Storage Information | `adb shell df`                               |

## Display

| Information    | Command                |
| -------------- | ---------------------- |
| Screen Size    | `adb shell wm size`    |
| Screen Density | `adb shell wm density` |

## CPU

1. the number of CPU cores

   ```shell
   cat /sys/devices/system/cpu/present
   ```

2. the number of CPU online

   ```shell
   cat /sys/devices/system/cpu/online
   ```

3. Setting CPUs online

   ```shell
   echo 1 > /sys/devices/system/cpu/cpu1/online
   echo 1 > /sys/devices/system/cpu/cpu2/online
   echo 1 > /sys/devices/system/cpu/cpu3/online
   ```

4. Setting CPUs offline

   ```shell
   echo 0 > /sys/devices/system/cpu/cpu1/online
   echo 0 > /sys/devices/system/cpu/cpu2/online
   echo 0 > /sys/devices/system/cpu/cpu3/online
   ```

5. Current Frequency

   ```shell
   cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq
   ```

6. Maximum Frequency

   ```shell
   cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_max_freq
   ```

7. Minimum Frequency

   ```shell
   cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_min_freq
   ```

8. Available Frequency

   ```shell
   cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies
   ```

9. Transition Latency

   ```shell
   cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_transition_latency
   ```

10. Brand

    ```shell
    cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_driver
    ```

11. An example to set CPU 0 max frequency

    ```shell
    //1. Available frequency.
    cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies
    768000 884000 1000000 1100000 1200000
    
    //2. Set max and min frequency.
    echo 416000  > /sys/devices/system/cpu/cpu0/cpufreq/scaling_min_freq
    echo 416000  > /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq
    
    //3. Check the result.
    cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
    ```

12. Available Governor

    ```shell
    cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors
    ```

13. Supported Governor

    ```shell
    cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
    ```

14. Set a governor

    ```shell
    echo "userspace" > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
    ```

## DDR

First you should enter the shell environment and then:

1. Current Frequency 

   ```shell
   cat sys/class/devfreq/scene-frequency/xxx-governor/ddrinfo_cur_freq
   ```

2. Supported Frequency

   ```shell
   cat sys/class/devfreq/scene-frequency/xxx-governor/ddrinfo_freq_table
   ```

3. Fixed DDR to a certain frequency

   ```shell
   echo 0 > /sys/class/devfreq/scene-frequency/xxx_governor/auto_dfs_on_off
   echo xxx > /sys/class/devfreq/scene-frequency/xxx_governor/scaling_force_ddr_freq
   ```

4. Governor of DDR

   ```
   cat /sys/class/devfreq/scene-frequency/xxx-governor
   ```

## GPU

First you should enter the shell environment and then:

1. GPU Frequency

   ```shell
   cat  sys/class/devfreq/60000000.gpu/available_frequencies
   ```

2. Current Frequency

   ```shell
   cat /sys/class/devfreq/60000000.gpu/cur_fre
   ```

## Skip wizard

If you want to skip the wizard when the device is active first time, you can:

```shell
adb shell settings put secure user_setup_complete 1
adb shell settings put global device_provisioned 1
adb reboot
```

## Find a APK file

If you want to find a `.apk` file on a device, you can issue this command:

```shell
adb shell pm path <PACKAGE_NAME>
```

## Compile Way

You can dump an app to find this app compile way.

```shell
adb shell dumpsys package <PACKAGE_NAME>
```

Then, scroll to `Dexopt state`. 

```shell
Dexopt state:
  [<PACKAGE_NAME>]
    path: /product/app/<NAME>/<NAME>.apk
      arm64: [status=verify] [reason=prebuilt]
```

If you want to modify compile way, you can issue this command:

```shell
adb shell cmd package compile -m <compile> <PACKAGE_NAME>
```

For example:

```shell
adb shell cmd package compile -m quicken com.google.android.calculator
```

Reference Docs:

1. https://zhuanlan.zhihu.com/p/418965915

2. https://blog.csdn.net/wenwen091100304/article/details/49704139
3. https://blog.csdn.net/weixin_35203997/article/details/117764764