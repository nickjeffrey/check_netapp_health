# check_netapp_health
nagios check for NetApp ONTAP storage system health

# Requirements
perl, snmpget, snmpwalk on nagios server, SNMP enabled on NetApp storage

# Configuration
You will need a section in the services.cfg file on the nagios server that looks similar to the following.
```
    define service{
       #syntax is check_netapp_health!SNMP_community_name
       use                             generic-service
       host_name                       netappfiler01
       service_description             Netapp health check
       check_command                   check_netapp_health!public
       }
```
You will also need a command definition similar to the following in commands.cfg on the nagios server
```
    # 'check_netappe_health' command definition
    define command{
       command_name    check_netapp_health
       command_line    $USER1$/check_netapp_health -H $HOSTADDRESS$ -C $ARG1$
       }
```

Enable SNMP on the NetApp storage from the CLI with:
```
    options snmp.enable on|off
    system snmp community show
    system snmp community add -type ro -community-name public
```

# Output
You will see output similar to the following
<img src=images/netapp.png>
