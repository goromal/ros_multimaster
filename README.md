ROS Multimaster
===============

This package is for setting up a multimaster ROS framework, where each ROS master corresponds to only one computer. The multimaster_fkie package is utilized.

Installation
===============
To install, do the following **on each machine in your multimaster network**:

1. Clone this package into the `src` directory of your catkin workspace.

2. Update submodules to obtain the multimaster_fkie package, then build:
```bash
cd ros_multimaster
git submodule update --init --recursive
cd ../..
catkin_make
```

3. Ensure that you are exporting the ROS_MASTER_URI and ROS_HOSTNAME variables in your environment:
```bash
export ROS_MASTER_URI=http://<IP address of machine>:11311
export ROS_HOSTNAME=<IP address of machine>
```
**Note:** it is important to use the IP address for at least all but one of the machines in the multimaster network, since there is no handling case for more than one ros master named 'localhost'.

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

5. Launch relevant multimaster nodes (if part of a larger project, you can just include the launch file in your main project launch file):
```bash
source devel/setup.bash
roslaunch multimaster multimaster.launch
```

Once this is done on each machine, each ros master should be able to see all of the nodes and published topics of the other ros master. Ignore functionality pending.
