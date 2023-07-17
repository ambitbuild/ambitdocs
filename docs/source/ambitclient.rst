Ambit Client
=====

.. _ambitclient:

Prerequisites
-------------

There are no prerequisites for the client on Ubuntu 22.04

Installation
------------

Client Installation:

Once you have downloaded the client binary for the architecture that you require, copy it to a directory of your choice (default is /usr/local/bin/ambit-client).

.. code-block:: console

   $ cp ambit-client /usr/local/bin/


Configuring the client
----------------

.. note::

   The client will look for a config file at /etc/ambitsentry/config.yaml by default.

The configuration of the client is defined in a yaml file.

The yaml file sections are detailed below

.. code-block:: console

   ``crypt:
      hmackeyb64: "EtWX3tULHQViiTLDoyLBoVmmnpltdkwpJF4qH0Uo8Gw="
      aeskeyb64: "sEAhWAQGDVJoM3JJmSxgXhdEUUvlaMdTp+oqmbYMWnk="``

The crypt section defines the AES key and the HMAC key that the agent and client will have in common.

The keys on the client MUST match the keys on the agent.

To generate a set of random keys you can use the following :

.. code-block:: console

   $ ambitclient --action genkeys
   Generating random HMAC and AES keys...                                                                                                                                                                             

   HMAC - 41jcSpTGAM90nsBgbSM4DsChpc/I40D1/PQM7J8NAGU=
   AES - u5kNUwpJojp5LJKIhaiLkH1xD+NJNthDCD9Noyecg98=

   Done.


The client can send different requests to the ambit agent.

For a list of supported requests use the following :

.. code-block:: console

   $ ./ambitclient -h
   Ambit Client BuildID - c1af038
   Usage of ./ambitclient:
   -action string
         The action for the client to perform. eg : ./ambitclient  --action genkeys
   -config string
         YAML configuration file. (default "/etc/ambitsentry/config.yaml")
   -host string
         The target host. eg : ./ambitclient  --action sendrequest --port 36000 --host service.example.com
   -message string
         The message for the action. eg : ./ambitclient  --action printpacket --message thisisatestmessage
   -port string
         The target port. eg : ./ambitclient  --action sendrequest --port 36000 --host service.example.com
   -rport string
         The requested port to open. eg : ./ambitclient  --action sendrequest --port 80 --host service.example.com --rport 80
   -rrule string
         The requested agent side rule. eg : ./ambitclient  --action sendrequest --rrule 1 --host service.example.com --rport 80
   -rtime string
         The duration (in mins) that the rule is valid for. eg : ./ambitclient  --action sendrequest --rtime 60 --host service.example.com --rport 80