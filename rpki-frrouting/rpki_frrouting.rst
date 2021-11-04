Introduction
=============
.. sectionauthor:: François Duchêne <francois.duchene@student.uclouvain.be>
.. sectionauthor:: Emile Giot <emile.giot@student.uclouvain.be>
		   
.. describe here your project

In this document, we will discuss how to implement RPKI for an existing or non-existing network.

---------------
What is RPKI ?
---------------

RPKI (*Resource Public Key Infrastructure*) is a specialized public key infrastructure (PKI) framework 
used to improve security of BGP messages. 
   
RPKI permet de vérifier qu'un préfixe partagé provient bien d'un AS identifié. 
Cette vérification s'effectue à l'aide de certificats ROA.

Cette infrastucture est composée d'autorités qui délivrent des certificats de validation, 
des serveurs de cache locaux qui récupèrent des listes de certificats de plusieurs authorités, 
et des clients qui utilisent ces serveurs locaux pour authentifier leurs messages BGP entrant et sortant.

Les serveurs de cache locaux sont eux-mêmes divisés en deux entités (cela peut varier en fonction des implémentations),
un serveur de donnée receuillant les certificats, et un autre serveur communiquant avec ce serveur de base de données.
Il communiquent entre eux à l'aide d'un protocole particulier, le protocole RTR (*RPKI to Router*).
