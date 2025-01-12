# Cisco Router/Switch NTP Setup

Setting up NTP and generally anything with config requires privilege elevation into User Exec to global conf mode. 
These methods will work on both Routers and Switches based on what I've read.


// If time shows user configuration, it was setup manually
~~~
R1# show clock detail
20:55:10.207 UTC Fri Nov 15 2019
Time source is user configuration 
~~~
~~~
R1 > enable
R1# conf t
R1(config)# ntp server ip-address
R1(config)#end
R1# show clock detail
21:01:34.563 UTC Fri Nov 15 2019
Time source is NTP
~~~

# NTP Authentication?

# Verification:
There are two methods of verification. Here are the methods along with their output: 
~~~
R1# show ntp associations
Clock is synchronized, stratum 2, reference is 209.165.200.225
nominal freq is 250.0000 Hz, actual freq is 249.9995 Hz, precision is 2**19
ntp uptime is 589900 (1/100 of seconds), resolution is 4016
reference time is DA088DD3.C4E659D3 (13:21:23.769 PST Fri Nov 15 2019)
clock offset is 7.0883 msec, root delay is 99.77 msec
root dispersion is 13.43 msec, peer dispersion is 2.48 msec
loopfilter state is 'CTRL' (Normal Controlled Loop), drift is 0.000001803 s/s
system poll interval is 64, last update was 169 sec ago.
~~~
~~~
R1# show ntp status
Clock is synchronized, stratum 3, reference is 192.168.1.1
nominal freq is 119.2092 Hz, actual freq is 119.2088 Hz, precision is 2**17
reference time is DA08904B.3269C655 (13:31:55.196 PST Tue Nov 15 2019)
clock offset is 18.7764 msec, root delay is 102.42 msec
root dispersion is 38.03 msec, peer dispersion is 3.74 msec
loopfilter state is 'CTRL' (Normal Controlled Loop), drift is 0.000003925 s/s
system poll interval is 128, last update was 178 sec ago.
~~~
