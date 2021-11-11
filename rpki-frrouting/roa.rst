Route Origin Authorizations
============================

.. sectionauthor:: Emile Giot <emile.giot@student.uclouvain.be>
.. sectionauthor:: François Duchêne <francois.duchene@student.uclouvain.be>

A Route Origin Authorization (ROA) is a digitally signed object that allows to verify that an IP address block
holder has allowed an Autonomous System to annoucne one or more prefix falling in the address block.
More precisely, the content of a ROA identifies one AS that has been authorized by the addres block holder
to advertise route to IP prefix from this address block. If the block holder wants to authorize multiple ASs
to advertise the same prefix, it has to issue multiple ROAs.

A ROA follows the following structure:
    RouteOriginAttestation ::= SEQUENCE {
         version [0] INTEGER DEFAULT 0,
         asID  ASID,
         ipAddrBlocks SEQUENCE (SIZE(1..MAX)) OF ROAIPAddressFamily }

It is composed of 3 fields:

1. version: the version number, must be 0.
2. asID: an integer representing the AS number receiving the Authorization.
3. ipAddrBlocks: the set of IP prefixes that the AS is allowed to announce.