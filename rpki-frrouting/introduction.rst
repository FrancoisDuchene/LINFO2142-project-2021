.. _introduction: 

Introduction
=============
.. sectionauthor:: Emile Giot <emile.giot@student.uclouvain.be>
.. sectionauthor:: François Duchêne <francois.duchene@student.uclouvain.be>
		   
.. describe here your project

In this document, we will discuss how to implement RPKI for an existing or non-existing network.

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

RPKI are used to improve security of BGP messages by verifying the authenticity of announced prefixes.
The AS(es) through which the prefixes were announced and through which they passed, are authenticated.
Les AS par lesquels les prefixes ont été annoncés, et par lesquels ils sont passés, sont authentifiés.

De cette manière, on peut s'assurer qu'un préfix annoncé provient d'une source fiable, et qu'il n'a pas été changé par un routeur d'un AS malicieux.


For more information about RPKIs, you can consult the dedicated page :doc:`rpki_architecture`.