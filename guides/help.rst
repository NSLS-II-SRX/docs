HELP!! The %$^$#@% just crashed
===============================

Managing IOCs
-------------

Soft IOCs are managed through the ``manage-iocs`` script.  To obtain a list of
softiocs running on a NSLS-II computer use the command ``manage-iocs report``
an example is shown below for ``xf23id1-ioc3``::

    [swilkins@xf23id1-ioc3 ~]$ manage-iocs report
    nBASE            | IOC             | USER            |  PORT | EXEC
    /epics/iocs     | apcupsd         | root            |  5000 | /epics/iocs/apcupsd/st.cmd
    /epics/iocs     | cam-diag1       | softioc         |  4202 | /epics/iocs/cam-diag1/st.cmd
    /epics/iocs     | cam-diag6       | softioc         |  4300 | /epics/iocs/cam-diag6/st.cmd
    /epics/iocs     | cam-dif1        | softioc         |  4204 | /epics/iocs/cam-dif1/st.cmd
    /epics/iocs     | cam-dif2        | softioc         |  4205 | /epics/iocs/cam-dif2/st.cmd
    /epics/iocs     | cam-dif3        | softioc         |  4206 | /epics/iocs/cam-dif3/st.cmd
    /epics/iocs     | cam-dif-beam    | softioc         |  4201 | /epics/iocs/cam-dif-beam/st.cmd
    /epics/iocs     | ct-eps          | softioc         |  4002 | /epics/iocs/ct-eps/st.cmd
    /epics/iocs     | es-dg645        | softioc         |  5013 | /epics/iocs/es-dg645/st.cmd
    /epics/iocs     | es-K2611        | softioc         |  4302 | /epics/iocs/es-K2611/st.cmd
    /epics/iocs     | es-tctrl1       | softioc         |  5010 | /epics/iocs/es-tctrl1/st.cmd
    /epics/iocs     | es-vortex       | softioc         |  4301 | /epics/iocs/es-vortex/st.cmd
    /epics/iocs     | mc11            | softioc         |  5001 | /epics/iocs/mc11/st.cmd
    /epics/iocs     | mc12            | softioc         |  5002 | /epics/iocs/mc12/st.cmd
    /epics/iocs     | mc13            | softioc         |  5003 | /epics/iocs/mc13/st.cmd
    /epics/iocs     | omegaM4061      | softioc         |  5012 | /epics/iocs/omegaM4061/st.cmd
    /epics/iocs     | simdetector     | softioc         |  4203 | /epics/iocs/simdetector/st.cmd
    /epics/iocs     | simmotor        | softioc         |  8001 | /epics/iocs/simmotor/st.cmd
    /epics/iocs     | timestamp       | softioc         |  6001 | /epics/iocs/timestamp/st.cmd
    /epics/iocs     | va-bakeout-01   | softioc         |  4001 | /epics/iocs/va-bakeout-01/st.cmd
    /epics/iocs     | zebra           | softioc         |  5011 | /epics/iocs/zebra/st.cmd

To connect to the IOC console, telnet to localhost at the port that is shown in
the table. For example to connect to the ``mc12`` console issue the command::

    [swilkins@xf23id1-ioc3 ~]$ telnet localhost 5002
    Trying ::1...
    Trying 127.0.0.1...
    Connected to localhost.
    Escape character is '^]'.
    @@@ Welcome to procServ (procServ Process Server 2.6.0)
    @@@ Use ^X to kill the child, auto restart is ON, use ^T to toggle auto restart
    @@@ procServ server PID: 10584
    @@@ Server startup directory: /epics/iocs/mc12
    @@@ Child startup directory: /epics/iocs/mc12
    @@@ Child "mc12" started as: /epics/iocs/mc12/st.cmd
    @@@ Child "mc12" PID: 28044
    @@@ procServ server started at: Tue Oct 20 17:35:25 2015
    @@@ Child "mc12" started at: Fri Nov 13 12:49:49 2015
    @@@ 0 user(s) and 0 logger(s) connected (plus you)

In order to reboot the IOC, type ``[CTRL] + X``. To leave the console type
``[CTRL] + ]`` and type ``close`` at the ``telnet>`` prompt

To start all IOCs configured on the system issue the command ``sudo manage-iocs
startall`` and if needed to stop all IOCs issue the command ``sudo manage-iocs
stopall``

OLog Glassfish Server
---------------------

To reboot the glassfish server on ``xf23id-ca.cs.nsls2.local`` execute::

    swilkins@xf23id-ca:~$sudo su - glassfish
    glassfish@xf23id-ca:~$cd glassfish3/bin/
    glassfish@xf23id-ca:~/glassfish3/bin$ ./asadmin stop-domain domain1
    glassfish@xf23id-ca:~/glassfish3/bin$ ./asadmin stop-domain domain2
    glassfish@xf23id-ca:~/glassfish3/bin$ ./asadmin start-domain domain1
    glassfish@xf23id-ca:~/glassfish3/bin$ ./asadmin start-domain domain2

