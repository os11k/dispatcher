# dispatcher
Simple config file of Kamailio as Loadblancer for calls and registrations

Hi!

This is simple config for somebody who need to use Kamailio as Loadbalancer in front of Freeswitch or Asterisk. This particular configuration will Loadbalance not only INVITEs, but registrations too.

Following configuration I took as template:
http://kamailio.org/docs/modules/4.3.x/modules/dispatcher.html

I'm not an expert in Kamailio, so this config might miss something.

I didn't put NAT traversal, for me freeswitch works without it, maybe later I will add it if I will think that this is necessary.

On freeswitch side I added following lines to sip profile config:

\<param name="all-reg-options-ping" value="true"/>

\<param name="nat-options-ping" value="true"/>

Additionnally you need to configure domain in vars.xml:

\<X-PRE-PROCESS cmd="set" data="domain=ip_or_domain_name_of_kamailio_server"/>

To make this configuration work you will need to add freeswitch servers to mysql db:

INSERT INTO dispatcher(setid, destination, flags, description) values (1, 'sip:freeswitchip:5060', 2, 'somedescription');

ToDO:

1) To add working Freeswitch configurations

2) To add working Asterisk configurations
