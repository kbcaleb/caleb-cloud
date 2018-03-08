---
title: GNU plot your SAR data
date: 2010-01-14 11:30:34.000000000 -07:00
categories:
  - gnu plot
  - sar
tags:
  - gnu plot
  - sar
header:
  teaser: "/assets/images/plot.png"
  show_overlay_excerpt: false
---
So recently I had to assemble some sar data into some nice  graphs that the higher ups could understand. So I decided to write out a  small script to graph out all the CPU and Memory stuff I wanted. Here  is how you can graph your data easily with gnuplot.
First we will build the sar data we want to work with. For this one I will do CPU
```shell
sar -u > /tmp/cpu_util.dat
```
Now we will use GNUplot to graph out the data from the file
```shell
gnuplot
```
Now simply enter the following information
```shell
set terminal png
set output 'cpu_util_$i.png'
set xdata time
set timefmt '%H:%M:%S'
set xrange ['00:00:00':'23:59:59']
set yrange [0:100]
set xlabel 'Hour'
set ylabel 'Percentage'
set xtics '00:00:00', 3600, '23:59:59'
set format x '%H'
set nomxtics
set grid
set size 2,1
set key right outside
set timestamp bottom
set title 'CPU Usage'
plot '/tmp/cpu_util.dat' using 1:3 title '%user' with lines, '/tmp/cpu_util.dat' using 1:5 title '%system' with lines, '/tmp/cpu_util.dat' using 1:6 title '%iowait' with lines
```
To edit the graph size simple change “set size” to your desired size.  The first number is the height and the second is the width. In addition  you can change what is reported by altering the 1:3, 1:4, or 1:5 lines  to be what ever column you want from the output of your sar command.
If you want to get more fancy you can do something like this in your script to echo in the GNUplot settings.
```shell
#!/bin/bash

cpu=/tmp/cpu_util.dat
mem=/tmp/mem_util.dat
gp=/tmp/gp

for i in ls -tr /var/log/sysstat | grep sa[0-99]
do
    sar -u -f /var/log/sysstat/$i > $cpu
    fdate=ls -latr /var/log/sysstat/"$i" | awk '{ print $6 $7}'
    echo "
    set terminal png
    set output 'cpu_util_$i.png'
    set xdata time
    set timefmt '%H:%M:%S'
    set xrange ['00:00:00':'23:59:59']
    set yrange [0:100]
    set xlabel 'Hour'
    set ylabel 'Percentage'
    set xtics '00:00:00', 3600, '23:59:59'
    set format x '%H'
    set nomxtics
    set grid
    set size 2,1
    set key right outside
    set timestamp bottom
    set title 'CPU $fdate'
    plot '$cpu' using 1:3 title '%user' with lines, '$cpu' using 1:5 title '%system' with lines, '$cpu' using 1:6 title '%iowait' with lines" > $gp gnuplot $gp rm -f $cpu $mem $gp
done
```
