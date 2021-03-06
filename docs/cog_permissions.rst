.. Permissions Cog Reference

=========================
Permissions Cog Reference
=========================

------------
How it works
------------

When loaded, the permissions cog will allow you
to define extra custom rules for who can use a command

If no applicable rules are found, the command will behave as if
the cog was not loaded.

-------------
Rule priority
-------------

Rules set will be checked in the following order


    1. Owner level command specific settings
    2. Owner level cog specific settings
    3. Server level command specific settings
    4. Server level cog specific settings

For each of those, settings have varying priorities (listed below, highest to lowest priority)

    1. User whitelist
    2. User blacklist
    3. Voice Channel whitelist
    4. Voice Channel blacklist
    5. Text Channel whitelist
    6. Text Channel blacklist
    7. Role settings (see below)
    8. Server whitelist
    9. Server blacklist
    10. Default settings

For the role whitelist and blacklist settings,
roles will be checked individually in order from highest to lowest role the user has
Each role will be checked for whitelist, then blacklist. The first role with a setting
found will be the one used.

-------------------------
Setting Rules from a file
-------------------------

The permissions cog can set rules from a yaml file:
All entries are based on ID. 
An example of the expected format is shown below.

.. code-block:: yaml

    cogs:
      Admin:
        allow:
          - 78631113035100160
        deny:
          - 96733288462286848
      Audio:
        allow: 
          - 133049272517001216
        default: deny
    commands:
      cleanup bot:
        allow:
          - 78631113035100160
        default: deny
      ping:
        deny:
          - 96733288462286848
        default: allow

----------------------
Example configurations
----------------------

Locking Audio cog to approved server(s) as a bot owner

.. code-block:: none

    [p]permissions setglobaldefault Audio deny
    [p]permissions addglobalrule allow Audio [server ID or name]

Locking Audio to specific voice channel(s) as a serverowner or admin:

.. code-block:: none

    [p]permissions setguilddefault deny play
    [p]permissions setguilddefault deny "playlist start"
    [p]permissions addguildrule allow play [voice channel ID or name]
    [p]permissions addguildrule allow "playlist start" [voice channel ID or name]

Allowing extra roles to use cleanup

.. code-block:: none

    [p]permissions addguildrule allow Cleanup [role ID]

Preventing cleanup from being used in channels where message history is important:

.. code-block:: none

    [p]permissions addguildrule deny Cleanup [channel ID or mention]
