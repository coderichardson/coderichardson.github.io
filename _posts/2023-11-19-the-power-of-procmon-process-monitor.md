---
title: "The Power of Procmon (Process Monitor)"
date: 2023-11-19 21:27:00 +0000
tags:
  - "Windows"
  - "Cybersecurity"
---

![](/assets/img/posts/the-power-of-procmon-process-monitor/01.png)
Procmon (Process Monitor) is "an advanced monitoring tool for Windows that shows real-time file system, Registry and process/thread activity." This accurately describes what Procmon does, but it doesn't come close to describing the power that it provides to monitor, investigate, and troubleshoot on a Windows system.

Let explore it (download from [Microsoft](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon) to follow along).

## Activity Options

![](/assets/img/posts/the-power-of-procmon-process-monitor/02.png)
Procmon had a hard time adjusting to my display resolution, but you can see here and in the screenshot at the top the Activity display options. These will enable / disable various types of activities from being displayed. Deselecting one of these options doesn't erase any existing logs, but just narrows down the output to the types of events you want to see. These include registry, file system, network, and process/thread activity.

These are helpful for narrowing focus when troubleshooting an issue, but you can still be left with thousands of entries. This is where filters come in.   

## Filters

![](/assets/img/posts/the-power-of-procmon-process-monitor/03.png)
Filters allow you to narrow the results in Procmon down to just those entries you care about and is where Procmon really starts to shine. For example, to see all of what chrome.exe is doing, we can apply the filter "Process Name is chrome.exe".

We can also select a Process ID, User, Path, and several other options. One of the most useful when troubleshooting an issue can be the Result filter. With the Result filter you can show all activity that was not successful -- failed or otherwise. This can be helpful in cases where an application is looking for a particular file or registry entry that is missing, or if a suspicious process is attempting to access directories it shouldn't.

## Process Tree

![](/assets/img/posts/the-power-of-procmon-process-monitor/04.png)
Procmon also gives you the ability to see a live process tree and include specific processes or whole subtrees in the full Procmon view.

Alternatively, you can select **Go To Event** and the chosen process will be jumped to and highlighted in the full Procmon view.

## Event Properties - Process and Stack

![Event Process](/assets/img/posts/the-power-of-procmon-process-monitor/06.png)

*Event Process*

![Event Stack](/assets/img/posts/the-power-of-procmon-process-monitor/07.png)

*Event Stack*

Two areas I use less often but that provide interesting detail are the Event Process and Event Stack tabs. These tabs provide the associated modules and the thread stack of a process, respectively.

## Boot Logging

![](/assets/img/posts/the-power-of-procmon-process-monitor/05.png)
Finally, enabling Boot Logging allows Procmon to record Windows startup activity for events such as loaded drivers that can aid in troubleshooting (requires a restart and starting Procmon again upon entering Windows).

## Conclusion

If you're ever troubleshooting an issue with a piece of software, investigating what a particular script touches, or just curious to learn more about what processes are doing on your system, Procmon is a great tool for the job.