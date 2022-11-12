# Systrace

> The article is from this [link](https://android-doc.github.io/tools/help/systrace.html).

The Systrace tool helps analyze the performance of your application by capturing and displaying execution times of your applications processes and other Android system processes. The tool combines data from the Android kernel such as the CPU scheduler, disk activity, and application threads to generate an HTML report that shows an overall picture of an Android device’s system processes for a given period of time.

The Systrace tool is particularly useful in diagnosing display problems where an application is slow to draw or stutters while displaying motion or animation. For more information on how to use Systrace, see [Analyzing UI Performance with Systrace](https://android-doc.github.io/tools/debugging/systrace.html).

## Requirements

In order to run Systrace, you must have Android SDK Tools 20 or later installed. You must also have [Python](http://www.python.org/) installed and included in your development computer's execution path. In order to generate a trace, you must connect a device running Android 4.1 (API Level 16) or higher to your development system using a [USB debugging connection](https://android-doc.github.io/tools/device.html#setting-up).

The Systrace tool can be run either from one of the Android SDK's graphical user interface tools, or from the command line. The following sections describe how to run the tool using either of these methods.

## Command Line Usage

The Systrace tool has different command line options for devices running Android 4.3 (API level 18) and higher versus devices running Android 4.2 (API level 17) and lower. The following sections describe the different command line options for each version.

The general syntax for running Systrace from the command line is as follows.

```shell
$ python systrace.py [options] [category1] [category2] ... [categoryN]
```

See the sections below for example Systrace sessions.

### Android 4.3 and higher options

When you use Systrace on devices running Android 4.3 and higher, you can omit trace category tags to get the defaults, or you may manually specify tags for inclusion. Here is an example execution run that sets trace tags and generates a trace from a connected device.

```shell
$ cd android-sdk/platform-tools/systrace
$ python systrace.py --time=10 -o mynewtrace.html sched gfx view wm
```

> **Tip:** If you want to see the names of tasks in the trace output, you *must* include the `sched` category in your command parameters.

The table below lists the Systrace command line options for devices running Android 4.3 (API level 18) and higher.

| Option                                           | Description                                                  |
| :----------------------------------------------- | :----------------------------------------------------------- |
| `-h, --help`                                     | Show the help message.                                       |
| `-o <*FILE*>`                                    | Write the HTML trace report to the specified file.           |
| `-t N, --time=N`                                 | Trace activity for *N* seconds. The default value is 5 seconds. |
| `-b N, --buf-size=N`                             | Use a trace buffer size of *N* kilobytes. This option lets you limit the total size of the data collected during a trace. |
| `-k <*KFUNCS*>--ktrace=<*KFUNCS*>`               | Trace the activity of specific kernel functions, specified in a comma-separated list. |
| `-l, --list-categories`                          | List the available tracing category tags. The available tags are:<br /><ul><br/>        <li><code>gfx</code> - Graphics</li><br/>        <li><code>input</code> - Input</li><br/>        <li><code>view</code> - View</li><br/>        <li><code>webview</code> - WebView</li><br/>        <li><code>wm</code> - Window Manager</li><br/>        <li><code>am</code> - Activity Manager</li><br/>        <li><code>audio</code> - Audio</li><br/>        <li><code>video</code> - Video</li><br/>        <li><code>camera</code> - Camera</li><br/>        <li><code>hal</code> - Hardware Modules</li><br/>        <li><code>res</code> - Resource Loading</li><br/>        <li><code>dalvik</code> - Dalvik VM</li><br/>        <li><code>rs</code> - RenderScript</li><br/>        <li><code>sched</code> - CPU Scheduling</li><br/>        <li><code>freq</code> - CPU Frequency</li><br/>        <li><code>membus</code> - Memory Bus Utilization</li><br/>        <li><code>idle</code> - CPU Idle</li><br/>        <li><code>disk</code> - Disk input and output</li><br/>        <li><code>load</code> - CPU Load</li><br/>        <li><code>sync</code> - Synchronization Manager</li><br/>        <li><code>workq</code> - Kernel Workqueues</li><br/>      </ul><br />**Note:** Some trace categories are not supported on all devices.<br />**Tip:** If you want to see the names of tasks in the trace output, you *must* include the `sched` category in your command parameters. |
| `-a <*APP_NAME*>--app=<*APP_NAME*>`              | Enable tracing for applications, specified as a comma-separated list of [package names](https://android-doc.github.io/guide/topics/manifest/manifest-element.html#package). The apps must contain tracing instrumentation calls from the `Trace` class. For more information, see [Analyzing UI Performance with Systrace](https://android-doc.github.io/tools/debugging/systrace.html#app-trace). |
| `--from-file=<*FROM_FILE*>`                      | Create the interactive Systrace report from a file, instead of running a live trace. |
| `-e <*DEVICE_SERIAL*>--serial=<*DEVICE_SERIAL*>` | Conduct the trace on a specific connected device, identified by its [device serial number](https://android-doc.github.io/tools/help/adb.html#devicestatus). |

## Trace Viewing Shortcuts

The table below lists the keyboard shortcuts that are available while viewing a Systrace trace HTML report.

| Key             | Description                                                  |
| :-------------- | :----------------------------------------------------------- |
| **w**           | Zoom into the trace timeline.                                |
| **s**           | Zoom out of the trace timeline.                              |
| **a**           | Pan left on the trace timeline.                              |
| **d**           | Pan right on the trace timeline.                             |
| **e**           | Center the trace timeline on the current mouse location.     |
| **g**           | Show grid at the start of the currently selected task.       |
| **Shift+g**     | Show grid at the end of the currently selected task.         |
| **Right Arrow** | Select the next event on the currently selected timeline.    |
| **Left Arrow**  | Select the previous event on the currently selected timeline. |

# Command Examples

```shell
# Example 1
python systrace.py -t 5 -o trace.html am wm view res ss database freq power sched gfx input idle binder_driver binder_lock dalvik pagecache -b 30720

# Example 2
python systrace.py -t 10 -o trace.html am wm view  res ss gfx  view hal bionic pm sched irq freq idle sync binder_driver binder_lock disk mmc pagecache memreclaim dalvik input  -b 20480
```
