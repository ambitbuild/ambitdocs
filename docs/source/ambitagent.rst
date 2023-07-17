Ambit Agent
=====

.. _ambitagent:

The Ambit Agent is core to the Ambit Framework. It is the component that is installed on the endpoint itself.



Prerequisites
-------------

The prerequisites that are required by ambit-agent are :

Zero MQ

LGPL Crypto library

PCAP - System interface for user-level packet capture

.. note::

   The following are the packages for ambit-agent on Ubuntu 22.04

.. code-block:: console

   $ sudo apt-get install libzmq5 libgcrypt20 libpcap0.8
   

Installation
------------

Agent Installation:

Once you have downloaded the agent binary for the architecture and distro that you require, copy it to a directory of your choice (default is /usr/local/bin/ambit-agent).

.. code-block:: console

   $ cp ambit-agent /usr/local/bin/


Configuring the agent
----------------

.. note::

   The agent will look for a config file at /etc/ambitsentry/config.yaml by default.

The configuration of the agent is defined in a yaml file.

The yaml file sections are detailed below

.. code-block:: console

   ``crypt:
      hmackeyb64: "EtWX3tULHQViiTLDoyLBoVmmnpltdkwpJF4qH0Uo8Gw="
      aeskeyb64: "sEAhWAQGDVJoM3JJmSxgXhdEUUvlaMdTp+oqmbYMWnk="``

The crypt section defines the AES key and the HMAC key that the agent and client will have in common.

The keys on the client MUST match the keys on the agent.

To generate a set of random keys you can use the following :

.. code-block:: console

   $ ambitagent --action genkeys
   Generating random HMAC and AES keys...                                                                                                                                                                             

   HMAC - 41jcSpTGAM90nsBgbSM4DsChpc/I40D1/PQM7J8NAGU=
   AES - u5kNUwpJojp5LJKIhaiLkH1xD+NJNthDCD9Noyecg98=

   Done.

.. code-block:: console

   ``license:
      licensefilepath: "/etc/ambitsentry/company.license.pem"
      
The license section defines the license configuration.


licensefilepath: is the location of the ambit sentry license file


.. code-block:: console

   ``ambitlog:
      logfile: "/var/log/ambitagent.log"
      loglevel: "DEBUG"``

The ambitlog section defines the logging configuration.


logfile: is the file that the agent will log to. It can also be set to STDOUT. This will log to the standard out of the process.


loglevel: is the level of logging. Possible values are DEBUG,INFO,WARN,ERROR


.. code-block:: console

   ``network:
      udpauthport: 34000
      udpauthdev: "lo"``

The network section defines the network configuration.


udpauthport: is is the UDP port that the agent will listen on for incoming client packets.


udpauthdev: is the device/adaptor that the agent will listen on 


.. code-block:: console

   ``fwmodule:
      fwmodule: "iptables"
      chainname: "AMBIT"
      purgechainonstop: "true"
      awssecgroupid: "aw23as34de3"
      removerulesonstop: "false"
      ingressauthport: 34000``

The fwmodule section defines the firewall module configuration.


fwmodule: is is the firewall module that the agent will use. Possible values are iptables and awssecuritygroups.


chainname: is the iptables chain name that the agent will create for it's rules


purgechainonstop: specifies whether or not the agent should purge the rules from the chain when the agent is stopped


awssecgroupid: is the AWS Security Group ID that is to be managed


removerulesonstop: specifies whether or not the agent must remove any rules it created in the security group when the agent is stopped.


ingressauthport: is the port to allow for incoming client requests


.. code-block:: console

   ``messaging:
      zmqbindaddress: "*"
      zmqbindport: 5757
      zmqauthdomain: "*"
      zmqauthiplist: "127.0.0.1/8"``

The messaging section defines the messaging configuration for comunication between the agent and the AMC.


zmqbindaddress: is is the address the ZMQ framework will bind to.


zmqbindport: is is the port the ZMQ framework will bind to.


zmqauthdomain: is is the authentication domain for the ZMQ framework


zmqauthiplist: is is the list of ip addresses allowed to connect to the ZMQ module of the agent



An example config file is

.. code-block:: console
   
   crypt:
      hmackeyb64: "EtWX3tULHQViiTLDoyLBoVmmnpltdkwpJF4qH0Uo8Gw="
      aeskeyb64: "sEAhWAQGDVJoM3JJmSxgXhdEUUvlaMdTp+oqmbYMWnk="
   license:
      licensefilepath: "/etc/ambitsentry/company.license.pem"
   ambitlog:
      logfile: "/var/log/ambitagent.log"
      loglevel: "DEBUG"
   network:
      udpauthport: 34000
      udpauthdev: "eth0"
      fwmodule:
   fwmodule: "iptables"
      chainname: "AMBIT"
      purgechainonstop: "true"
      awssecgroupid: "aw23as34de3"
      removerulesonstop: "false"
      ingressauthport: 34000
   insights:
      capdev: "eth0"
   messaging:
      zmqbindaddress: "*"
      zmqbindport: 5757
      zmqauthdomain: "*"
      zmqauthiplist: "127.0.0.1/8"


Starting the agent
----------------

.. note::

   The user that starts the agent requires sufficient permissions. Particularly permissions to capture packets and modify the netfilter module via iptables.


The agent can be started with no args if the config file is in the default location. 

Alternatively the location of the config file may be specified as an argument.


.. code-block:: console

   $ sudo ./ambitagent -config ./agent.example.yaml


The logs will indicate if the agent started successfully.
