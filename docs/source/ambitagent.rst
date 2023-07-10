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

The key value pairs are as follows :

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
   insights:
      capdev: "eth0"
   messaging:
      zmqbindaddress: "*"
      zmqbindport: 5757
      zmqauthdomain: "*"
      zmqauthiplist: "127.0.0.1/8"

