Network configuration
=========================

.. sectionauthor:: Emile Giot <emile.giot@student.uclouvain.be>
.. sectionauthor:: François Duchêne <francois.duchene@student.uclouvain.be>

--------------------------------
FRRouting
--------------------------------

FRRouting is a free and open-source Internet routing protocol suite for Linux and Unix platforms,
it implements many protocoles such as BGP or OSPF. 

We will assume that an implementation using FRRouting is already installed on your machine.

The BGP commands to use RPKI are already implemented in FRRouting. They are available in full on the official documentation site [#frrouting_rpki]_ .
The implementation of RPKI by FRRouting is based on the definition given in RFC 6810 and the validation scheme on RFC 6811 :cite:p:`RFC6810,RFC6811`.

You need to install the additional package "frr-rpki-rtrlib" to enable support for RPKI, otherwise the "bgpd" daemon will simply not start.

^^^^^^^^^^^^^^^^^^
Configure a router
^^^^^^^^^^^^^^^^^^

To activate the RPKI configuration mode on a router on which you have previously logged in, simply activate the "rpki" command.
Be careful, activating this command does not activate the validation of IP prefixes in itself. In order to work, at least one cache server must be available.



--------------------------------
RPKI validator
--------------------------------

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
OctoRPKI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AUTRE TODO
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-------------------------------------
Virtual network tools
-------------------------------------

^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Mininet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

^^^^^^^^^^^^^^^^^^^^^^^^^^^^
IPMininet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. rubric:: Footnotes

.. [#frrouting_rpki] http://docs.frrouting.org/en/latest/bgp.html#prefix-origin-validation-using-rpki