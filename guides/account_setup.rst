Controls Account Setup Guide
============================

Introduction
------------

NSLS-II controls accounts allow access to all computers at CSX. Once a new
account has been created, the following is suggested to get the account working
correctly. 

Fixing Permissions
------------------

Firstly, all accounts are created with global read permissions. If this is OK
by you then skip the next step. However, if you want to restict access to files
in your home directory then do the following: ::

    [swilkins@xf23id1-srv2 ~ ]$ chmod o-rwx,g-w+rx,u+rwx /home/<uid>

Setting up an SSH Key
---------------------

Create the RSA Key Pair
^^^^^^^^^^^^^^^^^^^^^^^

The first step is to create an SSH key pair in your home directory: ::

    ssh-keygen -t rsa

the ``ssh-keygen`` command will ask you a few questions: ::

    Enter file in which to save the key (/home/demo/.ssh/id_rsa):

You can press enter here, saving the file to the user home (in this case, the
user is called demo). ::

    Enter passphrase (empty for no passphrase):

You should enter a passphrase. The security of a key, no matter how encrypted,
still depends on the fact that it is not visible to anyone else. Should a
passphrase-protected private key fall into an unauthorized users possession,
they will be unable to log in to its associated accounts until they figure out
the passphrase.

The entire key generation process looks like this: ::

    ssh-keygen -t rsa
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/demo/.ssh/id_rsa): 
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /home/demo/.ssh/id_rsa.
    Your public key has been saved in /home/demo/.ssh/id_rsa.pub.
    The key fingerprint is:
    4a:dd:0a:c6:35:4e:3f:ed:27:38:8c:74:44:4d:93:67 demo@a
    The key's randomart image is:
    +--[ RSA 2048]----+
    |          .oo.   |
    |         .  o.E  |
    |        + .  o   |
    |     . = = .     |
    |      = S = .    |
    |     o + = +     |
    |      . o + o .  |
    |           . o   |
    |                 |
    +-----------------+
    The public key is now located in /home/demo/.ssh/id_rsa.pub The private key (identification) is now located in /home/demo/.ssh/id_rsa

Copy the Public Key
^^^^^^^^^^^^^^^^^^^

Once the key pair is generated, you can now install it on the controls system
to allow access. This can be done with the ``ssh-copy-id`` command: ::

    ssh-copy-id user@box64-2

where ``user`` is your username. If sucsessful, You should see something like: ::

    [swilkins@xf23id1-srv2 ~/Scratch ]$ ssh-copy-id swilkins@box64-2
    ********************************************************************************
    *                                                                              *
    *                                NOTICE TO USERS                               *
    *                                                                              *
    *     This is a Federal computer system (and/or it is directly connected       *
    *      to a BNL local network system) and is the property of the United        *
    *    States Government. It is for authorized use only. Users (authorized or    *
    *      unauthorized) have no explicit or implicit expectation of privacy.      *
    *                                                                              *
    *      Any or all uses of this system and all files on this system may be      *
    *      intercepted, monitored, recorded, copied, audited, inspected, and       *
    *         disclosed to authorized site, Department of Energy, and law          *
    *       enforcement personnel, as well as authorized officials of other        *
    *       agencies, both domestic and foreign. By using this system, the         *
    *     user consents to such interception, monitoring, recording, copying,      *
    *          auditing, inspection, and disclosure at the discretion of           *
    *              authorized site or Department of Energy personnel.              *
    *                                                                              *
    *   Unauthorized or improper use of this system may result in administrative   *
    *    disciplinary action and civil and criminal penalties. By continuing to    *
    *      use this system you indicate your awareness of and consent to these     *
    *     terms and conditions of use. LOG OFF IMMEDIATELY if you do not agree     *
    *                  to the conditions stated in this warning.                   *
    *                                                                              *
    ********************************************************************************
    Now try logging into the machine, with "ssh 'swilkins@box64-2'", and check in:

      ~/.ssh/authorized_keys

    to make sure we haven't added extra keys that you weren't expecting.

Now you are done ... you should be able to login using SSH kets now.

