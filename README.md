# bachelordegree-project-snmpgame

I developed this game as my bachelor degree thesis project. THe game uses some data gathered by the SNMP protocol to create some elements of the game itself. 



## Instruction

To play it's necessary another computer connected to Internet with a Linux distro or Windows with an Ubuntu subsystem. (It's also possible to play as localhost in the same way).

Follow this procedure on the machine you want to control:

```
apt-get update
apt-get install snmpd
apt-get install snmp

cd /etc/snmp
nano snmpd.conf
```

Now it's necessary to make some change to the configuration file:

- AGENT SECTION
```
#agentAddress udp:127.0.0.1:161
agentAddress udp:161,udp6:[::1]:161
```

-ACCESS CONTROL

To allow the access only from localhost
```
...
rwcommunity public localhost
#rocommunity public default -V systemonly
...
```
to allow access from also other address

```
...
#rocommunity public localhost
rwcommunity public default 
or
rwcommunity6 public default //for IPv6
...
```

NOTE: public it's the community string. It works like a password and can be change.

Save and close (Ctrl+O,Enter,Ctrl+X)

```
/etc/init.d/snmpd restart
```

Check if everything work properly using the instruction:
```
snmpwalk -v 2c -c public 127.0.0.1 1.3.6.1.2.1.1
```








