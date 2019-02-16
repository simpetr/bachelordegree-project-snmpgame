# bachelordegree-project-snmpgame

I developed this game as my bachelor degree thesis project. The game uses some data gathered by the SNMP protocol to create and to update some elements of the game itself. 

The is available on:
-Windows

The game it's like a "3D Task Manager". Game goal is to find as many monsters as possible around the map and "scan" them.The game is time limited, to stop the countdown is necessary to scan at least 70% of monsters. Each monster is a real process executing on the machine we connected previously. A monster will move only if the related process is running, and its size will change based on the RAM usage. Monsters can "see" or "hear" the player, in that case they will start to follow the player trying to hit it. The player can run and escape from them or killing them with the laser gun losing the chance to get the information about their related processes.

Scanning a monster allows to view the information related to its process in real-time (name, PID, RAMusage, CPUusage, status). Also it's possible to mark that process and view the related monster on the mini-map.

Because the game gathers the data in real-time from another machine, the number of processes (and so monsters) can drastically change in any moment.

The player gets one point for each second it's not seen from monsters. With these points it can buy some bonus like the batteries for the torch.

## Installation instructions

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

## CONTROLS

-WASD movement
- 1 turn on/off torch
- 2 laser gun
- E scan
- B scanned processes information view

While the scanned processes information view is open
- up/down arrows to move between the scanned processes
- L to mark the selected scanned process

- T turn on beacon
- Y heal
- U extra battery
- I laser gun extra energy
- O speed boost






