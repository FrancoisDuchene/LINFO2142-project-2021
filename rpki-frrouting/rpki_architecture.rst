.. _rpki_architecture:

RPKI Architecture
==================

.. sectionauthor:: Emile Giot <emile.giot@student.uclouvain.be>
.. sectionauthor:: François Duchêne <francois.duchene@student.uclouvain.be>

The deployment structure of RPKI is composed of 3 main elements.
1. Trust anchors
2. Local caches / Validator
3. Routers

-------------
Trust anchors
-------------

The trust anchors are a set of servers on which the authorative data of the RPKI are published.
For a relying party to use RPKI, it has to choose a set of trust anchors from which it will retreive the
RPKI data. According to RFC6480, an obvious choice would be the five RIRs (regional internet registries)
which are AFRINIC, ARIN, APNIC, LACNIC and RIPE NCC.

The trust anchors are contacted via rsync [#]_ 1 [#]_ using information contained in a TAL. A TAL or trust
anchor locator is composed of a rsync URI and a public key corresponding to a particular trust anchor as
described in RFC6490. Here is an example:

rsync://rpki.example.org/rpki/hedgehog/root.cer
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAovWQL2lh6knDx
GUG5hbtCXvvh4AOzjhDkSHlj22gn/1oiM9IeDATIwP44vhQ6L/xvuk7W6
Kfa5ygmqQ+xOZOwTWPcrUbqaQyPNxokuivzyvqVZVDecOEqs78q58mSp9
nbtxmLRW7B67SJCBSzfa5XpVyXYEgYAjkk3fpmefU+AcxtxvvHB5OVPIa
BfPcs80ICMgHQX+fphvute9XLxjfJKJWkhZqZ0v7pZm2uhkcPx1PMGcrG
ee0WSDC3fr3erLueagpiLsFjwwpX6F+Ms8vqz45H+DKmYKvPSstZjCCq9
aJ0qANT9OtnfSDOS+aLRPjZryCNyvvBHxZXqj5YCGKtwIDAQAB

-------------------------
Local caches / Validator
-------------------------
The role of the validator will firstly be to contact to choosen set of trust anchors in order to retrieve 
the RPKI data that will be needed to create a local ROA cache. And secondly, the validator will be used
by the routers to access ROAs information. The validator has to periodically refresh the RPKI data.

--------
Routers
--------
RPKI enabled routers can contact the validator in order to verify that a route to a given IP prefix was 
originated by an AS that was allowed by the prefix holder. Depending on the validation result, the router
can handle the received route accordingly.
The communication bewteen a router and the validator is done via the RTR protocol.



.. rubric:: Footnotes

.. [#] https://rsync.samba.org/