.. _introduction: 

Introduction
=============
.. sectionauthor:: Emile Giot <emile.giot@student.uclouvain.be>
.. sectionauthor:: François Duchêne <francois.duchene@student.uclouvain.be>
		   
.. describe here your project

Internet connections are nowadays more and more subject to attacks as its democratization increases. 
While in the early days of the Internet, communication protocols focused almost exclusively on the technical aspect of sending data, 
nowadays the security of transmissions must also be taken into account. 
While most of the protocols used today have received a security upgrade to protect them, such as SSL/TLS for HTTP, 
or have been replaced by other secure protocols, such as Telnet by SSH, other protocols are still not completely secure.

The BGP protocol used by border routers to communicate with external and autonomous network infrastructures
is an example of a protocol that is still not completely secure everywhere. 
However, there are solutions that are increasingly implemented in the industry. 
In this tutorial, we will explain how to configure an autonomous system to secure its BGP connections with the outside world. 
In this way, the received IP prefixes can be authenticated. BGP hijacking is thus avoided.

---------------
What is RPKI ?
---------------

RPKI (*Resource Public Key Infrastructure*) is a specialized public key infrastructure (PKI) framework 
used to improve security of BGP messages. 

RPKI is used to verify that a shared prefix comes from an identified AS. 
This verification is done using ROA certificates.

This infrastructure is composed of authorities that issue validation certificates, 
local cache servers that retrieve lists of certificates from multiple authorities, 
and clients that use these local servers to authenticate their incoming and outgoing BGP messages.

The local cache servers are themselves divided into two entities (this may vary depending on the implementation)
a data server receiving the certificates, and another server communicating with this database server.
They communicate with each other using a particular protocol, the RTR (*RPKI to Router*) protocol.

----------------
Why use RPKI ?
----------------

RPKI is used to improve the security of BGP messages by verifying the authenticity of advertised IP prefixes. The ASes through which the messages containing the IP prefixes passed and were retransmitted are authenticated via the public key infrastructures.
This way, if an attacker tries to hijack BGP by sending wrong IP prefixes, the client will know from the Certificate Authority (CA) that these prefixes are not from the right AS.


IP prefix hijacking can be done in a number of ways, the two most common are:

- Regular prefix hijacking: occurs when the attacker's router hijacks a route from an existing IP prefix by advertising a new one. This prefix will then partially pollute the Internet, changing the routing tables based on the preferability of the bogus route over the valid route. This will depend on the configuration of each particular network.

- Sub-prefix hijacking: occurs when the attacker steals a subnet of a prefix already existing in the routing tables, by advertising a route for the subnet from the attacker's network. Because of the plus-grand-prefix-matching policies of network operators, most networks on the Internet become polluted. 

To further complicate matters, some stealth attackers may disguise both types of attacks with falsified AS paths without changing the original AS, 
while passing traffic through the attacker's network. :cite:p:`bgphijacking2007`
Certification of ASes and IP prefixes by Certification Authorities via RPKIs counters most attacks of this style.


For more information about RPKIs, you can consult the dedicated page :doc:`rpki_architecture`.

.. bibliography::