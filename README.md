nagios-plugin-criticalupdates
=============================

Simple nagios plugin for monitoring critical updates on host

Assuming you have installed it into 

/etc/nagios-plugins/nagios-plugin-criticalupdates



#Define new command (for example by amending commands.cfg)

define command {

  command_name check_criticalupdates
  
  command_line /etc/nagios-plugins/nagios-plugin-criticalupdates/check_critical
  
}


#Define service to check on concrete host.  Enjoy!


define service {

        use                             generic-service         ; Name of service
        
        host_name                       localhost
        
        service_description             Security updates pending
        
        check_command           check_criticalupdates
                
        }



#Installation on remote host:


On remote host:

1.  Install npre server

sudo apt-get install nagios-nrpe-server

sudo gedit /etc/nagios/nrpe.cfg

modify allowed_hosts to include main nagios address

allowed_hosts = 192.168.0.8,127.0.0.1

2.	Install security updates checker from https://github.com/Voronenko/nagios-plugin-criticalupdates

Next steps assume, that you don’t want git installed:

cd /usr/lib/nagios

sudo mkdir nagios-plugin-criticalupdates

cd nagios-plugin-criticalupdates/

sudo touch  check_criticalupdates.sh

sudo gedit check_criticalupdates.sh

copy contents of the file https://raw.github.com/Voronenko/nagios-plugin-criticalupdates/master/check_criticalupdates.sh and save

sudo chmod +x check_criticalupdates.sh

3.	Register security update checker command in /etc/nagios/nrpe.cfg

command[check_criticalupdates]=/usr/lib/nagios/nagios-plugin-criticalupdates/check_criticalupdates.sh

4.	Restart nagios nrpe server

sudo service nagios-nrpe-server restart

