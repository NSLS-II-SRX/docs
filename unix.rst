UNIX Account Setup
==================

File Permissions
----------------

In a unix system every file (and directory) has an owner, an associated
group, and a set of permission flags that specify separate read, write,
and execute permissions for the *user* (owner), *group*, and *other*.
*Other* is also sometimes known as *world* permissions, and applies to
all users who can login to the system. 

The permission flags can be seen by the ``ls -l`` command::

    [swilkins@xf23id1-srv1 ~/Presentations]$ ls -l
    total 24M
    -rw-rw---- 1 swilkins csx  22M Mar  5  2014 csx.pdf
    -rw-rw---- 1 swilkins csx 1.2M Mar  3  2014 csx.ppt
    drwxrwx--- 2 swilkins csx    6 Nov 24 06:15 other

The first field is a set of 10 permission flags. The first flag is the *file
type*. For regular files it is not set (-). Directories are indicated by *d*
and links by *l*. The remaining 9 flags are 3 groups of 3 for read (r) / write
(w) / execute (x) for the user, group and other. In the example above the files
are read/write permitted for both the user (swilkins) and any members of the
csx group. Any other users cannot read or write the files. Note that the
directory *other* has the execute bit set for only the user and group to
restrict listing to only the user and members of the csx group.

To set file permissions, UNIX uses the *octal* representation of file
permissions, with 4 digits representing the special, user, group and other.

.. table:: Octal file permissions for ``chmod`` and ``umask``

    =========== ==================================== ==================================================== 
    Octal digit ``chmod`` Permissions                ``umask`` Permissions
    =========== ==================================== ==================================================== 
    0           No permissions                       Any permission may be set
    1           Execute permission only              Setting of execute permission is prohibited
    2           Write permission only                Setting of write permission is prohibited
    3           Write and execute permissions        Setting of write and execute permission is prohibited 
    4           Read permission only                 Setting of read permission is prohibited
    5           Read and execute permissions         Setting of read and execute permission is prohibited
    6           Read and write permissions           Setting of read and write permission is prohibited
    7           Read, write and execute permissions  All permissions are prohibited from being set
    =========== ==================================== ==================================================== 

The file permissions can be changed using the ``chmod`` command with the
permissions specified in an octal format and can be applied *recursively* using
the ``-R`` option. For example: ::

    [swilkins@xf23id1-srv1 ~/Presentations]$ ls -l
    total 24M
    -rw-rw---- 1 swilkins csx  22M Mar  5  2014 csx.pdf
    -rw-rw---- 1 swilkins csx 1.2M Mar  3  2014 csx.ppt
    drwxrwx--- 2 swilkins csx    6 Nov 24 06:15 other
    [swilkins@xf23id1-srv1 ~/Presentations]$ chmod 700 other
    [swilkins@xf23id1-srv1 ~/Presentations]$ ls -l
    total 24M
    -rw-rw---- 1 swilkins csx  22M Mar  5  2014 csx.pdf
    -rw-rw---- 1 swilkins csx 1.2M Mar  3  2014 csx.ppt
    drwx------ 2 swilkins csx    6 Nov 24 06:15 other
    [swilkins@xf23id1-srv1 ~/Presentations]$

UNIX uses the **umask** to define how (new or default) files permissions are
set. This can be set on a per-user basis using the ``umask`` command to set the
default (allowed) permissions. The ``umask`` command uses the `octal
representation`_ the same as ``chmod`` to define permissions and should have
the *restricted* permissions set - i.e. the inverse of what you want the files
to be. 

.. code-block:: bash

    $ umask 0227      # allow user rwx group r-x and other r-x      (-rwxr-xr-x)
    $ umask 0027      # allow user rwx group r-x and restrict other (-rwxr-x---)
    $ umask 0007      # allow group and user rwx and restrict other (-rwxrwx---)
    $ umask 0077      # allow only user rwx                         (-rwx------)

The following example illustrates the use of the ``umask`` command: ::

    [swilkins@xf23id1-srv1 ~/Example]$ umask
    0007
    [swilkins@xf23id1-srv1 ~/Example]$ touch hello_world
    [swilkins@xf23id1-srv1 ~/Example]$ ls -l
    total 0
    -rw-rw---- 1 swilkins csx 0 Nov 24 06:55 hello_world
    [swilkins@xf23id1-srv1 ~/Example]$ umask 0027
    [swilkins@xf23id1-srv1 ~/Example]$ touch goodbye_world
    [swilkins@xf23id1-srv1 ~/Example]$ ls -l
    total 0
    -rw-r----- 1 swilkins csx 0 Nov 24 06:55 goodbye_world
    -rw-rw---- 1 swilkins csx 0 Nov 24 06:55 hello_world
    [swilkins@xf23id1-srv1 ~/Example]$ umask 0023
    [swilkins@xf23id1-srv1 ~/Example]$ touch hello_world_again
    [swilkins@xf23id1-srv1 ~/Example]$ ls -l
    total 0
    -rw-r----- 1 swilkins csx 0 Nov 24 06:55 goodbye_world
    -rw-rw---- 1 swilkins csx 0 Nov 24 06:55 hello_world
    -rw-r--r-- 1 swilkins csx 0 Nov 24 06:58 hello_world_again

To set the umask for every session the command should be added to your
``.bashrc`` file. CSX Team members should add the following to their ``.bashrc``:

.. code-block:: bash

    umask 0027

Bash Shell Setup
----------------

The BASH shell is initialized by two main files ``.bashrc`` and ``.bash_profile``.
These are executed by the shell differently depending on how the shell is
executed. This is often a source of confusion. These files are summarized below:

* ``.bashrc`` : This is run by *interactive* shells. These are shells that are
  connected to a terminal (or pseudo-terminal) such as a `xterm` running under
  a windowing system.  
  
* ``.bash_profile`` : This is run by *login* shells. These are shells
  that are started when you login from another host or you login from the text
  terminal on a local machine. 

BASH is also different from other shells in that ``.bashrc`` and ``.bash_profile``
are *mutually exclusive* (i.e. only one is run on the shell startup). To get
round this problem, most people place teh following in the ``.bash_profile`` so
that the shell is initialized the same way for both *interactive* and *login*
shells:

.. code-block:: bash

    if [ -f ~/.bashrc ]; then
        source ~/.bashrc
    fi


.. _`octal representation`: https://en.wikipedia.org/wiki/Chmod
