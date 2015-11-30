Configure Graylog Inputs
************************

In order for Graylog to receive log messages, you will need to configure one or more inputs.  

We use GELF for our collector and it is an open log format with many native integrations. 

Syslog
^^^^^^

1. Click on System->Inputs
2. Select Syslog UDP
3. Select *Launch* new input.  
4. Follow the example configuration below

**Note**: If you are not root, you may not be able to use ports below 1024, in that case simply add a 0 to the port.  

.. image:: ../images/syslog.png

GELF
^^^^

1. Click on System->Inputs
2. Select Gelf UDP
3. Select *Launch* new input.  
4. Follow the example configuration below

.. image:: ../images/gelf.png

