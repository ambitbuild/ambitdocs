Ambit Agent
=====

.. _agent:

The Ambit Agent is core to the Ambit Framework. It is the component that is installed on the endpoint itself.

.. toctree::
   agent-ubuntu


Prerequisites
-------------

The following are dependencies that need to be installed for ambit-agent

.. code-block:: console

   $ sudo apt-get install libzmq5 libgcrypt20 libpcap0.8
   

Installation
------------

Agent Installation:

Once you have downloaded the agent binary for the architecture that you require, copy it to a directory of your choice (default is /usr/local/share/ambit-agent).

.. code-block:: console

   $ cp ambit-agent /usr/local/share/


Configuring the agent
----------------

.. note::

   The agent will look for a config file at /etc/ambitsentry/config.yaml by default.

An example config file is

.. code-block:: console
   
   crypt:
      hmackeyb64: "EtWX3tULHQViiTLDoyLBoVmmnpltdkwpJF4qH0Uo8Gw="
      aeskeyb64: "sEAhWAQGDVJoM3JJmSxgXhdEUUvlaMdTp+oqmbYMWnk="
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
   apiservice:
      apiservicecertpath: "/etc/ambitsentry/cert.pem"
      apiservicekeypath: "/etc/ambitsentry/key.pem"
      apiserviceclientcertspath: "/etc/ambitsentry/tarcapcert.pem"
      apiservicebindip: "10.131.0.2"
      apiservicebindport: 8000
   insights:
      capdev: "eth0"
   messaging:
      zmqbindaddress: "*"
      zmqbindport: 5757
      zmqauthdomain: "*"
      zmqauthiplist: "127.0.0.1/8"

