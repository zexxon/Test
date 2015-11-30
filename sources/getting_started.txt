.. _gettingstarted:

*****************************
Graylog Getting Started Guide
*****************************

The first thing you are going to want to do is get logs into Graylog. If you are running the appliance, then you are probably collecting logs, however you will want to know how to get other logs into Graylog. 


.. image:: ../images/windows.png
   :align: left
   :height: 100
   :width: 100
   :scale: 25 %
   :target: Windows_ 

Click here if you want to get Windows_ logs in.




.. image:: ../images/linux.jpeg
   :align: left
   :height: 100
   :width: 100
   :scale: 25 %
   :target: Linux_
   
 
Click here if you want to get Linux_/Unix/OS X logs in. 





If you want to quickly get logs into Graylog, try the following command on your favourite Linux, Unix or Mac OS X host (also possible with Windows using Cygwin or other tools)::

$:while read log; do   echo -n $log; done </var/log/syslog | nc -u -c localhost 5140

**Note**: You may need to change the path/filename (/varlog/system.log) depending on the operating system and also the hostname/port (localhost 5140) to the Graylog server host/IP and Graylog syslog UDP port. Also, if log messages wrap lines, they may not be cleanly parsed. We recommend using the Graylog collector or another robust log collector to read log files. 


.. _Windows: getting_started/getting-messages-in.html#windows
.. _Linux: getting_started/getting-messages-in.html#linux


.. toctree::
   :titlesonly:
   getting_started/config_input.rst
   getting_started/getting-messages-in.rst
   getting_started/check_messages.rst
   getting_started/create_dashboard.rst
   getting_started/stream_alerts.rst
