Installing Linxbrew
===================

Introduction
------------

`Linuxbrew <http://brew.sh/linuxbrew/>`_ is a package manager for linux which
can be used to have a local installation of such utilities such as ``git``,
``gist`` and ``tmux``. It is especially useful to get around systems which have
relatively out of date core utilities (not looking at you debian). As it
doesn't need superuser privilages it can be installed in a home directory for
example.  

Installing
----------

To install at CSX, it is prefertable to install in the GPFS system in your
userspace. To do this: ::

    [swilkins@xf23id1-srv2 ~]$ git clone https://github.com/NSLS-II-CSX/linuxbrew.git \
        /GPFS/xf23id/users/<uid>/linuxbrew

where ``<id>`` should be substituted for your username. Now edit your
``.bashrc`` file and add the following:

.. code-block:: bash
    
    if [ -e "/GPFS/xf23id/users/<id>/linuxbrew" ]; then
        export PATH="/GPFS/xf23id/users/<id>/linuxbrew/bin:$PATH"
        export MANPATH="/GPFS/xf23id/users/<id>/linuxbrew/share/man:$MANPATH"
        export INFOPATH="/GPFS/xf23id/users/<id>/linuxbrew/share/info:$INFOPATH"
    fi

where as before ``<id>`` should be replaced with your username. You are now
ready to install some useful programs. As a suggestion, the following are useful: ::

    [swilkins@xf23id1-srv2 ~]$ brew install openssl
    [swilkins@xf23id1-srv2 ~]$ brew install git
    [swilkins@xf23id1-srv2 ~]$ brew install gist
    [swilkins@xf23id1-srv2 ~]$ brew install tmux


