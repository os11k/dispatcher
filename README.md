# dispatcher
Simple config file of Kamailio as Loadblancer for calls and registrations

This is simple config for somebody who need to use Kamailio as Loadbalancer in front of Freeswitch or Asterisk. This particular configuration will Loadbalance not only INVITEs, but registrations too.

Following configuration I took as template:
http://kamailio.org/docs/modules/5.3.x/modules/dispatcher.html#dispatcher.ex.config

On freeswitch side I added following lines to sip profile config:

\<param name="all-reg-options-ping" value="true"/>

\<param name="nat-options-ping" value="true"/>

Additionnally you need to configure domain in vars.xml:

\<X-PRE-PROCESS cmd="set" data="domain=ip_or_domain_name_of_kamailio_server"/>

To make this configuration work you will need to add freeswitch/asterisk to list file(dispather.list as example) or to mysql db. 

To make DB work you will need to uncomment lines related to DB and make sure that DB url is set properly and don't forget to remove line where list file is set). 

And off cause you will need to insert related data:

`INSERT INTO dispatcher(setid, destination, flags, priority) values (1, 'sip:freeswitchip1:5060', 0, 0);`
`INSERT INTO dispatcher(setid, destination, flags, priority) values (1, 'sip:freeswitchip2:5060', 0, 0);`

Please make sure that setid is `1` for both servers.
