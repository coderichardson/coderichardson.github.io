---
title: "On Time - NTP, ISO 8601, UTC, Atomic Clocks, and Time Zones"
date: 2025-06-23 00:32:00 +0000
tags:
  - "NTP"
  - "Time"
---

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/01.png)
I enjoy learning about time. It's fascinating to me how we've globally agreed that time will be different for various parts of the world, how we are going to represent that time difference, and making sure that we know the most accurate time possible. This isn't just important to make sure you're on time for an appointment, but it is surprisingly important in the technology we use every day.

Here's everything I find interesting about time.

## Time Zones and UTC

As of this writing, there are [38 time zones](https://www.timeanddate.com/time/current-number-time-zones.html#zones) in use globally. Most are an hour offset from their neighbor, but some are only 30 or 45 minutes different. Some countries encompass multiple time zones (United States, Russia) while others use only one despite being large enough to have previously used five (China)!

Time zones get complicated very quickly, but have a rather simple origin -- Greenwich Mean Time (GMT) and the goal of aiding sailors in determining longitude at sea. This is where the term "prime meridian" comes from as it was chosen as the referential meridian at the time. This grew to establishing a standard time for people and countries to observe, followed by other countries establishing their own time zones offset from GMT. There is quite a bit of interesting history around this and I encourage you to read some of it -- [here](https://en.wikipedia.org/wiki/Time_zone#History), [here](http://en.wikipedia.org/wiki/Greenwich_Mean_Time), and [here](https://avi-8.com/blogs/the-aviation-journal/the-history-of-greenwich-mean-time-gmt?srsltid=AfmBOor631zcOzLMPPuMYwm5ikVXjvIGBn4UNErBA2mnQN3TDCq_3lBo). I won't repeat it here, but will fast-forward to today and share some of my favorite information about time zones and UTC.

Time zones split the world into "western" time zones and "eastern" time zones referenced from the prime meridian, as mentioned earlier. These span from the westernmost (−12:00) to the easternmost (+14:00) with various special offsets mixed in. This is why you will often see these offsets shown in  maps as they will coincide with the referenced time zone (for example at the top of this blog post).

As previously mentioned, most countries observe [hour offsets](https://en.wikipedia.org/wiki/List_of_UTC_offsets#) denoted as, for example, UTC-05:00.  For some countries, there may multiple offsets if you observe Daylight Savings Time (DST). This is when, typically in spring and summer, countries advance their clocks by one hour so daylight ends later in the day.

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/02.png)
*Countries that observe Daylight Savings Time*

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/03.png)
*Showing how Daylight Savings Time impacts the UTC offset between EST and DST.*

Whether Daylight Savings Time should still be in practice, is useful in modern times, and its true origin are all...subjects for another time. But as it is the reality we live in, I always ensure when emailing or otherwise referencing time for professional matters that I include "EST" or "DST" and it is accurate. This is especially important if you're working with someone in Arizona or in a country that doesn't observe DST. On more than one occasion I've seen people miss meetings because they failed to account for observation of daylight savings time and correct offsets. Coordinating global resources is fun.

What is the answer to these problems? UTC.

UTC is based on International Atomic Time (TAI) and does not adjust for daylight savings time. This means that no matter where you are in the world at any given moment UTC is the same globally. Humanity worked for hundreds of years to arrive at this achievement and we hardly think about it day-to-day.

Most people in tech are familiar with Coordinated Universal Time (UTC). This is the primary standard for time used by computers, your phone, aviation, weather forecasts, and even the International Space Station. It is what the vast majority of the world references for time, aside from very specialized applications in research, navigation, and timekeeping. (It is also "local time" for Iceland and Ghana).

As mentioned, this is why industries such as aviation and tech often use it when communicating time. Tracking an incident that spans multiple time zones? Or troubleshooting an issue between different regions in AWS? Reference UTC. Looking at Wireshark traces in different time zones, accounting for the offsets, and the presence or lack of DST, gets tiring. (Not to mention if you're used to 12-hour clocks and you have to "convert" from 24-hours clocks). I don't work in aviation, but I imagine they have similar experiences I could relate to (flight plans, air traffic control directions, etc). You may also see UTC referenced as "Zulu time" or written as, for example, 10:30Z instead of 10:30 UTC. This is due Z being the designation for the "0" offset for UTC. All the [other offsets](https://en.wikipedia.org/wiki/List_of_UTC_offsets#) have designators as well, but this is by far the most frequently referenced and well-known.

## ISO 8601

Since we are talking about displaying time (and dates), I want to introduce [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601). This section will be brief but will highlight one of my favorite things -- a standard.

The International Organization for Standardization (ISO) is responsible for establishing standards for multiple industries in technical and non-technical fields. To date, they have published over 25,000 standards. In IT/Infosec/GRC, [ISO 27001](https://www.iso.org/standard/27001) is a well-known ISO standard followed by many security programs globally.

In 1988, ISO solved the problem of how to properly format dates and times such that they are unambiguous, or at the very least, so everyone knows what they are looking at -- ISO 8601. The opportunity was created so that there would be no confusion as to whether 6/13/2025 meant June 12, 2025 or December 6, 2025. ISO 8601 provides the following standards for dates and times:

**Date**:   
2025-06-13 (YYYY-MM-DD)

**Time**:   
00:04:37Z

T000437Z

**Date and time**:   
2025-06-13T00:04:37Z

20250613T000437Z

**Date and time with the offset**:   
2025-06-12T12:04:37−12:00 UTC−12:00

2025-06-13T00:04:37+00:00 UTC+00:00

2025-06-13T12:04:37+12:00 UTC+12:00

**Week**:   
2025-W24

**Week with weekday**:   
2025-W24-5

**Ordinal date**:   
2025‐164

The regular date being the most useful of the bunch in my opinion. An infrequently mentioned benefit of formatting dates this way is that if you save files on a computer with the date in the beginning of the file, all files will automatically be sorted by date. No need to sort by "date modified", etc. This is something I've found useful on occasion depending on the project.

A close second favorite, and one I use frequently in writing, is to fully write out the date (e.g. July 4, 1776). This also clears up any confusion as to what date is being referenced.

## Atomic Clocks

Atomic clocks are a special kind of clock that keep the most precise time on Earth. They measure properties of certain atoms which allow for an accurate keeping of time. Specifically, the precise length of a second. These clocks are primarily used by governments, universities, and other large organizations as they require in-depth scientific knowledge and funding to operate. UTC (as well as International Atomic Time - a subject for another day) is based on the result of atomic clocks worldwide and is another reason why UTC is so accurate.

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/04.jpg)
*By National Institute of Standards and Technology - Physics Laboratory: Time and Frequency Division*

  
NIST in the United States operates the standard atomic clock for the United States with its NIST-F2 cesium fountain atomic clock. This and other cesium fountain atomic clocks work by measuring the resonant frequency of cesium. From the official definition of a "second":

“*The second is the duration of 9,192,631,770 periods of the radiation corresponding to the transition between the two hyperfine levels of the ground state of the caesium-133 atom. This definition refers to a caesium atom at rest at a temperature of 0 Kelvin.*”  

There are several thorough explanations of the full process behind this on YouTube as well as other blogs/articles online. I understand some of the physics, but believe you'll be better served looking at some of the original content as I am far from an expert.

In addition to the cesium fountain atomic clocks, other types of atomic clocks exist. For example, rubidium atomic clocks and hydrogen maser clocks. These both have pros and cons, with the pros being that they are typically simpler and cheaper to build than cesium fountain atomic clocks. However, they are not as reliable long-term. There are rubidium atomic clocks found in many satellites currently orbiting Earth.

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/05.jpg)
*WWVB radio transmission from Fort Collins, Colorado*

  
The accurate time measured by these atomic clocks is broadcast for consumer and commercial applications. In the United States, [this is in Fort Collins, Colorado](https://www.nist.gov/pml/time-and-frequency-division/time-distribution/radio-station-wwvb). Germany and the United Kingdom have similar broadcasts in Europe, as do other locations globally. Many clocks, watches, and other appliances are preconfigured to receive this signal and automatically update the time on that appliance.  

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/06.jpg)
*Signal strength of WWVB at 0600 UTC*

## Network Time Protocol (NTP)

Network Time Protocol (NTP), like most of the other subjects in this post, could use its own article. But I'll do my best to provide a high-level overview and highlight what I like about it.

NTP is used by most computers globally to sync their system clock to within a few milliseconds of UTC. This likely includes the computer or phone you're reading this on. It is currently defined in [RFC 5905](https://www.rfc-editor.org/rfc/rfc5905) which specifically defines NTPv4.

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/07.png)
*NTP hierarchical design, credit Wikipedia.*

Typically, a client, such as your phone, is configured to poll (query) a specified NTP server. This NTP server is usually configured to poll another NTP server, either a peer or a NTP server in another *stratum*. The usual data flow is such that devices in stratum 3 query devices in stratum 2, which query devices in stratum 1, which query devices in stratum 0. NTP uses UDP port 123.

  

Technically, devices in stratum 0 cannot advertise themselves. These are the cesium fountain atomic clocks and other similar timekeeping devices we discussed previously. Computers are attached or otherwise synchronized to these devices and those computers are then part of stratum 1. Practically, stratum 1 is the source of truth in NTP as a device advertising itself as stratum 0 in NTP means that its stratum is undefined. The maximum number of strata in a given NTP system is 15. 16 is reserved to indicate that a device in unsynchronized.

![](/assets/img/posts/on-time-ntp-iso-8601-utc-atomic-clocks/08.png)
Above is an example output from my system showing that it synchronizes to **time.windows.com** for its NTP server. Plenty of other options exist and advertise on different stratum depending on the server. My personal recommendations in addition to time.windows.com are:

- time.nist.gov
- pool.ntp.org

Both have benefits and drawbacks, but I will say that if you need highly-accurate time (within 1ms) use time.nist.gov.

On a separate note, I like <https://www.time.gov/> for finding what the current time is and seeing how far off my current device is from UTC. Setting the oven and microwave clocks after a power outage means getting them as close to this time as possible.

## Conclusion

I hope you found some of this information interesting and realize that accurate time is really important!

Something we didn't get into, but as an example, Windows Server Domain Controllers (DC) often won't allow clients to connect if their system time is off by 5 minutes or more due to risk of replay attacks. Sync your DCs against reliable NTP servers and ensure all clients are connected frequently to your DCs!

See you next *time*!