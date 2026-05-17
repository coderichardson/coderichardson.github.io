---
title: "The Power of Procmon (Process Monitor)"
date: 2023-11-19 21:27:00 +0000
tags:
  - "Windows"
  - "Cybersecurity"
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgOO5WXqmHW2tPLvxxuVaibf6WZlXs6sDJvK6kVbVMNFwItCwe3GaZBlIoux4GjFSyNJkUedaTezIjcgW3TSnr4kJOmpsSNApKZOp49iC3pdgsZkv6jl0nBJLDBu6ciG1d7J7-8yeIIPMSM0lxgclTc6-6r4_T1om29ZDcpy6xo4Hia_yZYTC37DKmpuH7S/w640-h478/procmon-main.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgOO5WXqmHW2tPLvxxuVaibf6WZlXs6sDJvK6kVbVMNFwItCwe3GaZBlIoux4GjFSyNJkUedaTezIjcgW3TSnr4kJOmpsSNApKZOp49iC3pdgsZkv6jl0nBJLDBu6ciG1d7J7-8yeIIPMSM0lxgclTc6-6r4_T1om29ZDcpy6xo4Hia_yZYTC37DKmpuH7S/s1024/procmon-main.png)

Procmon (Process Monitor) is "an advanced monitoring tool for Windows that shows real-time file system, Registry and process/thread activity." This accurately describes what Procmon does, but it doesn't come close to describing the power that it provides to monitor, investigate, and troubleshoot on a Windows system.

Let explore it (download from [Microsoft](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon) to follow along).

## Activity Options

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEFbZg0E5lTFTgDKzcaoXnrhrOqHDXKcZR1f2K61V9XZRMUBJU4ZIWgFFqNHJe5gyDGQMkvArvsIKe_e-1WDGmqG_TtPZW64fuTve3315QnPhfRBAsRfv8_xiKyNi1dht_vgjY1stG5SIfyiaMYTvmoNjvDS_mOraNxH8KR5CiYYg_nVqSoNDHpaXQtYSn/w640-h336/sysinternals-activity-types.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEFbZg0E5lTFTgDKzcaoXnrhrOqHDXKcZR1f2K61V9XZRMUBJU4ZIWgFFqNHJe5gyDGQMkvArvsIKe_e-1WDGmqG_TtPZW64fuTve3315QnPhfRBAsRfv8_xiKyNi1dht_vgjY1stG5SIfyiaMYTvmoNjvDS_mOraNxH8KR5CiYYg_nVqSoNDHpaXQtYSn/s2858/sysinternals-activity-types.png)

Procmon had a hard time adjusting to my display resolution, but you can see here and in the screenshot at the top the Activity display options. These will enable / disable various types of activities from being displayed. Deselecting one of these options doesn't erase any existing logs, but just narrows down the output to the types of events you want to see. These include registry, file system, network, and process/thread activity.

These are helpful for narrowing focus when troubleshooting an issue, but you can still be left with thousands of entries. This is where filters come in.   

## Filters

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjI9HgzQPzFAQfw1SYsu5FlwKhvLqkCPVRP10eEV3RVUUSK0xjidWhjlv13Pfqd3jQJukG8ArdxV76DnhhGlUJn2JMHTND19duSUtHPpfVtyhYlq5bCjsTPtuV0oVFxIpVCG9CQ8goEY-V7azOI9DbZQ6kwFD-opXWJvQuLFh0pUW8T3vFwYK13IUJM6amF/w640-h278/procmon-filters.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjI9HgzQPzFAQfw1SYsu5FlwKhvLqkCPVRP10eEV3RVUUSK0xjidWhjlv13Pfqd3jQJukG8ArdxV76DnhhGlUJn2JMHTND19duSUtHPpfVtyhYlq5bCjsTPtuV0oVFxIpVCG9CQ8goEY-V7azOI9DbZQ6kwFD-opXWJvQuLFh0pUW8T3vFwYK13IUJM6amF/s2370/procmon-filters.png)

Filters allow you to narrow the results in Procmon down to just those entries you care about and is where Procmon really starts to shine. For example, to see all of what chrome.exe is doing, we can apply the filter "Process Name is chrome.exe".

We can also select a Process ID, User, Path, and several other options. One of the most useful when troubleshooting an issue can be the Result filter. With the Result filter you can show all activity that was not successful -- failed or otherwise. This can be helpful in cases where an application is looking for a particular file or registry entry that is missing, or if a suspicious process is attempting to access directories it shouldn't.

## Process Tree

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLbPBVmPZkuNFFBzjretPD2MaINaqmA8xfF4_yzpx-RpuSZrVkoMrBZjhBjxBarM9hr3yV31lAmN_LF7bl8KD27yZGkT-_EUGDraypBQ1LfSceGM11v_KqtCYQyFsqZwJn90TtiYyr8SETHr2O1_CYUsW3LpcR3pGC-HTN06LA_a8h1fhsk_S4Zvdz76T9/w640-h608/procmon-process-tree.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLbPBVmPZkuNFFBzjretPD2MaINaqmA8xfF4_yzpx-RpuSZrVkoMrBZjhBjxBarM9hr3yV31lAmN_LF7bl8KD27yZGkT-_EUGDraypBQ1LfSceGM11v_KqtCYQyFsqZwJn90TtiYyr8SETHr2O1_CYUsW3LpcR3pGC-HTN06LA_a8h1fhsk_S4Zvdz76T9/s1414/procmon-process-tree.png)

Procmon also gives you the ability to see a live process tree and include specific processes or whole subtrees in the full Procmon view.

Alternatively, you can select **Go To Event** and the chosen process will be jumped to and highlighted in the full Procmon view.

## Event Properties - Process and Stack

|  |
| --- |
|  |
| Event Process |

  

|  |
| --- |
|  |
| Event Stack |

Two areas I use less often but that provide interesting detail are the Event Process and Event Stack tabs. These tabs provide the associated modules and the thread stack of a process, respectively.

## Boot Logging

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUTOwP7nkoTqJZ6E1EV1kEERTdzNDjd8MTwlwQGKzzNcxwfFCKKoKq2bQ8fB48t7LYkEI-q7ogFVVmMAYCmuGN0QcZFZv46Z9s6A6_ZyQQ5bqbcMjkTMTbjOhV7W33anPgZnpmweC-u4hMQnWFQzK_L6GmEDv6DA6FVghyy0HwQx4xzToy98-jWqSv6tLB/w640-h440/2023-11-19%2016_17_46-Enable%20Boot%20Logging.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUTOwP7nkoTqJZ6E1EV1kEERTdzNDjd8MTwlwQGKzzNcxwfFCKKoKq2bQ8fB48t7LYkEI-q7ogFVVmMAYCmuGN0QcZFZv46Z9s6A6_ZyQQ5bqbcMjkTMTbjOhV7W33anPgZnpmweC-u4hMQnWFQzK_L6GmEDv6DA6FVghyy0HwQx4xzToy98-jWqSv6tLB/s1017/2023-11-19%2016_17_46-Enable%20Boot%20Logging.png)

Finally, enabling Boot Logging allows Procmon to record Windows startup activity for events such as loaded drivers that can aid in troubleshooting (requires a restart and starting Procmon again upon entering Windows).

## Conclusion

If you're ever troubleshooting an issue with a piece of software, investigating what a particular script touches, or just curious to learn more about what processes are doing on your system, Procmon is a great tool for the job.