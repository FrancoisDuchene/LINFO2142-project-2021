Validation of Route Origination
===============================

.. sectionauthor:: Emile Giot <emile.giot@student.uclouvain.be>
.. sectionauthor:: François Duchêne <francois.duchene@student.uclouvain.be>

As mentionned before, the interest of RPKI is to ensure that a route to a prefix was annouced over BGP by an AS that
was allowed to announce such prefix. Therefore, a validation process has to take place for each route received
over a BGP session in order to check the IP prefix - AS number pair. It is performed using the ROA information and 
can have 3 different outcomes: valid, unknown or invalid. The validation process is the following:

1. Firstly, a set of ROAs matching the IP prefix or being a covering aggregate of the IP prefix of the route is selected. This set forms "the candidate ROAs".
2. If the set of candidate ROAs is empty, the validation procedure stops and the outcome is "unknown".
3. If any of the candidate ROA contains an asID field matching the route's origin AS and the route IP prefix matches an IP prefix in the ROA, the outcome of the procedure is "valid".
4. If this step is reached, the outcome of the procedure is "invalid".

The table below summurizes the procedure:


+---------------+-----------+--------------+
| Route  AS->   | matching  | non-matching |
| Prefix        | AS        |   AS         |
+===============+===========+==============+
| Non-          | unknown   | unknown      |
| Intersecting  |           |              |
+---------------+-----------+--------------+
| Covering      | unknown   | unknown      |
| Aggregate     |           |              |
+---------------+-----------+--------------+
| match ROA     | valid     | invalid      |
| prefix        |           |              |
+---------------+-----------+--------------+
| More Specific | invalid   | invalid      |
| than ROA      |           |              |
+---------------+-----------+--------------+

Once the validation is done, it can be applyed to the route selection process. The preference order should be
the following: "valid" is to be preferred over "unknown", which is to be preferred over "invalid". However,
the action to be taken for an "unknown" or "invalid" route's validity state is a matter of local routing 
policy.
As mentionned in RFC6483 :cite:p:`RFC6483`, it is recommended to not consider "unknown" validity state as sufficient ground 
to reject a route from futher consideration due to the partial use of ROAs.