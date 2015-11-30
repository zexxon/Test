Getting Messages In
--------------------

Linux, Unix and OS X
********************


The easiest way to get logs into Graylog without deploying anything is to configure your syslog server to send logs to Graylog directly. 

**Note**: If you aren't running the appliance, you may want to check that your syslog_ input is configured. 

.. _Linux:

Update (R)Syslog configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Simple Config**

Run the following commands::

$sudo sh -c "echo '*.* @127.0.0.1:5140' >> /etc/rsyslog.conf"
$sudo service rsyslog restart

For Unix and OS X Log Sources::

$sudo sh -c "echo '*.* @127.0.0.1:5140' >> /etc/syslog.conf"
Restart your syslog service (will vary depending on OS)

For other log sources, such as syslog-ng please check out our marketplace(link)

**Custom Config**

Go to the /etc directory, and use vi, vim (`CheatSheet <http://www.fprintf.net/vimCheatSheet.html>`_), or the editor of your choice to modify the ``/etc/rsyslog.conf`` file.  There are excellent resources on the web for `rsyslog configuration <http://www.rsyslog.com/doc/v8-stable/tutorials/reliable_forwarding.html>`_.

At the bottom of the file, add the following so messages will forward to the local Graylog server::

$:*.* @127.0.0.1:5140

In case you wanted to know, @ means UDP, 127.0.0.1 is localhost, and 5140 is the port (514 is the default port for syslog but if you don't have root access, you will need to use a port >1024).

.. image:: /images/gs_7-rsyslogadd.png

**Restart rsyslog**

Type::

  $sudo service rsyslog status
  $sudo service rsyslog restart

Quick Collector Deployment
**************************

**Note**:Requires the GELF_ input plugin to be enabled 

#. Download the latest collector release. (find download links in the `collector repository README <https://github.com/Graylog2/collector#binary-download>`_)
#. Unzip collector tgz file to target location
#. cp ``config/collector.conf.example`` to ``config/collector.conf``
#. Update server-url in collector.conf to correct Graylog server address (required for registration)
#. Update file input configuration with the correct log files
#. Update outputs->gelf-tcp with the correct Graylog server address (required for sending GELF messages)

**Note**:The collector will not start properly if you do not set the URL or the correct input log files and GELF output configuration

.. _Windows:

Windows
*******

Note:: Requires the GELF_ input plugin to be enabled
 
You need to have Java >= 7 installed to run the collector.

Download a release zip file from the `collector repository README <https://github.com/Graylog2/collector#binary-download>`_. Unzip the collector zip file to target location.

.. image:: /images/collector_win_install_1.png

Change into the extracted collector directory and create a collector configuration file in ``config\collector.conf``.

.. image:: /images/collector_win_install_2.png

The following configuration file shows a good starting point for Windows systems. It collects the *Application*, *Security*, and *System* event logs.
Replace the ``<your-graylog-server-ip>`` with the IP address of your Graylog server.

Example::

  server-url = "http://<your-graylog-server-ip>:12900/"

  inputs {
    win-eventlog-application {
      type = "windows-eventlog"
      source-name = "Application"
      poll-interval = "1s"
    }
    win-eventlog-system {
      type = "windows-eventlog"
      source-name = "System"
      poll-interval = "1s"
    }
    win-eventlog-security {
      type = "windows-eventlog"
      source-name = "Security"
      poll-interval = "1s"
    }
  }

  outputs {
    gelf-tcp {
      type = "gelf"
      host = "<your-graylog-server-ip>"
      port = 12201
    }
  }

Start a ``cmd.exe``, change to the collector installation path and execute the following commands to install the collector as Windows service.

Commands::

  C:\> cd graylog-collector-0.2.2
  C:\graylog-collector-0.2.2> bin\graylog-collector-service.bat install GraylogCollector
  C:\graylog-collector-0.2.2> bin\graylog-collector-service.bat start GraylogCollector

.. _syslog: config_input.html
.. _GELF: config_input.html
