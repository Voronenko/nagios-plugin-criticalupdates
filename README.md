nagios-plugin-criticalupdates
=============================

Simple nagios plugin for monitoring critical updates on host

Assuming you have installed it into 

/etc/nagios-plugins/nagios-plugin-criticalupdates



#Define new command (for example by amending commands.cfg)

define command {
  command_name check_criticalupdates
  command_line /etc/nagios-plugins/nagios-plugin-criticalupdates/check_critical$
}


#Define service to check on concrete host.  Enjoy!

define service{
        use                             generic-service         ; Name of servi$
        host_name                       localhost
        service_description             Security updates pending
                check_command           check_criticalupdates
        }

