---
layout:     post
title:      Visualizing ZeroAccess Botnet Traffic with D3
date:       2015-08-13 00:53:29
summary:    Visualizing data.
categories: viz code data
---

### ZeroAccess Botnet Traffic
#####UPDATE: So we got some colors on the map and played around with the data so we can visualize it. The initial data file was 2.4 GB in size and contained duplicate records for several communications between my infection and other infections. We removed the duplicates and added some color.

To give a little background about this post, I ran a virtual machine for about 3 weeks with ZeroAccess botnet infection and captured all the communication between my machine and the world. I have been meaning to get this data visualized on a map, but I haven't had the time to do so. 

We took pairs of IPs (Time, IP_a, IP_b), did a lookup for each using Maxmind DB. Then we transformed the file to (time, country_a, country_b). We used D3JS and ThreeJS to animate and visualize the data. We also shamelessly stole the base template from here (http://d3.artzub.com/wbca/). Thanks bro!


![Image](/images/zaccess.gif)


I was recently approached by a CMUQ student to work with me. So, I assigned him this task, and he has done a beautiful job! We are still tweaking things here and there, but we will have a more colorful animation soon.
