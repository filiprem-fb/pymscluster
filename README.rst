Python module for Windows Server Failover Clustering
=====

This module manage the Windows Server Failover Clustering using the Windows API.

Features
--------
* List cluster nodes, resources and group
* Get node, resource and group status
* Move group between nodes
* Start and stop resources and group

Install
--------
::

    pip install pymscluster`

Example
--------
.. code-block:: python

    import mscluster

    C = mscluster.Cluster()  # localhost by default

    Cname = C.name
    
    for Gname in C.groups:
        G = C.openGroup(Gname)
        Gnode = G.node
        Gstate = G.state
        print('Cluster [%s] ResourceGroup[%s] state[%s] ownerNode[%s]' % (Cname, Gname, Gstate.name, Gnode))

    for Nname in C.nodes:
        N = C.openNode(Nname)
        Nstate = N.state
        print('Cluster [%s] Node[%s] state[%s]' % (Cname, Nname, Nstate.name))

    for Rname in C.resources:
        R = C.openResource(Rname)
        Rstate = R.state
        Rgroup = R.state.group
        Rnode = Rstate.node
        Rtype = R.type
        print('Cluster [%s] Resource[%s] Type[%s] State[%s] OwnedBy[%s] Group[%s]'
              % (Cname, Rname, Rtype, Rstate.state.name, Rnode, Rgroup))


    r = C.openResource("IP Address 192.168.12.236")
    r.takeOffline()
    t.takeOnline()
