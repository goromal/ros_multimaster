ROS Multimaster
===============

This package is for setting up a multimaster ROS framework, where each ROS master corresponds to only one computer. The multimaster_fkie package is utilized.

Installation
===============
To install, do the following **on each machine in your multimaster network**:

1. Clone this package into the `src` directory of your catkin workspace.

2. Make sure that the ROS package multimaster_fkie is installed:
```bash
sudo apt-get install ros-kinetic-multimaster-fkie
```

3. Ensure that you are exporting the ROS_MASTER_URI variable in your environment:
```bash
export ROS_MASTER_URI=http://<hostname or IP address>:11311
```

4. Enable network multicasting (disabled on Ubuntu by default)

First check if the multicast feature is enabled using the following command:
```bash
cat /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
```
If this command returns 0, then the multicast feature is enabled and the rest of step 4 can be skipped.

To temporarily enable the multicast feature until reboot, execute the following command:
```bash
sudo sh -c "echo 0 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts"
```

To permanently enable the multicast feature, append or uncomment the following line in /etc/sysctl.conf:
```
net.ipv4.icmp_echo_ignore_broadcasts=0
```
Then, execute the following command:
```bash
sudo service procps restart
```

To test the multicast feature, execute the following command:
```bash
ping 224.0.0.1
```
If everything is configured properly, you should get a reply from each computer in the network at each iteration.

5. 



(have a launch file that takes care of everything, with a param file of ip addresses (needed? actually maybe not) and a param file with topics that you wanna pass over the network, explaining the whole bandwith thing behind this mentality)
- modify parameter files
- either roslaunch directly or add the following line to whatever launch file your project is using
- conclusion/results
