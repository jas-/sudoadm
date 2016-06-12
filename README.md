# sudoadm [![Build Status](https://travis-ci.org/jas-/sudoadm.png?branch=master)](https://travis-ci.org/jas-/sudoadm)

The missing API for automating sudoer changes

## Options ##
Here are the available options for `sudoadm`.

```sh
  Usage:
    ./sudoadm -vnVamrAHCD <Key> <Value>
    ./sudoadm -RiV

  Options:
    -h  Show this message
    -e  Show example usage

  Specify a mode:
    -a  Addition mode
    -r  Removal mode

  Specify an option type & value:
    -D  Defaults option
    -H  Host alias
    -A  User alias
    -C  Command alias
    -P  Permissions

  Additional actions:
    -f  Specify sudoer configuration file
    -v  Perform validation of change
    -R  Perform rollback of changes
    -i  Interactive mode (Use with -R)
    -n  Create sudoer file if it doesn't exist
    -V  Be verbose

```

## API ##
A fairly complete API for making changes is in place to help automate changes
to the sudoers or sudoers.d/ file(s).

### Manage user aliases ###
Below are some usage examples when working with the User_Alias stanza

#### Add/Edit User_Alias ####
```sh
./sudoadm -a -A foo "bar, baz, ping, pong"
```

#### Remove an existing User_Alias ####
```sh
./sudoadm -r -A foo
```

#### Remove an existing User_Alias member ####
```sh
./sudoadm -r -A foo "bar"
```

### Manage host aliases ###
Below are some usage examples when working with the Host_Alias stanza

#### Add/Edit Host_Alias ####
```sh
./sudoadm -a -H command "server01, server02, server03"
```

#### Remove an existing Host_Alias ####
```sh
./sudoadm -r -H host_alias
```

#### Remove an existing Host_Alias member ####
```sh
./sudoadm -r -H foo "bar"
```

### Manage command aliases ###

```sh
  - Add new command alias
      ./sudoadm -a -C cmd_alias "/bin/ls, /sbin/lsof, /bin/top"

  - Remove an existing command alias
      ./sudoadm -r -C cmd_alias

  - Remove an existing command alias member
      ./sudoadm -r -C foo "bar"
```

### Manage permissions ###

```sh
  - Add new permission
      ./sudoadm -a -P foo "ALL=/sbin/lsof, /bin/strace"
      ./sudoadm -a -P %foo "localhost=/sbin/lsof, /bin/strace"

  - Remove an existing command alias
      ./sudoadm -r -P foo
      ./sudoadm -r -P %foo

  - Remove an existing command alias member
      ./sudoadm -r -P foo "/bin/lsof"
      ./sudoadm -r -P %foo "/bin/lsof"
```

### Manage default options ###

```sh
  - Add new default option
      ./sudoadm -a -D default_opt "!root_sudo, timestamp_timeout"

  - Remove an existing default option
      ./sudoadm -r -D default_opt

  - Remove an existing default option member
      ./sudoadm -r -D foo "bar"
```

### Additional options ###

```sh
  - Specify path to sudoer configuration file to add a new user
    alias & members
      ./sudoadm -f /etc/sudoers.d/foo.conf -a -A foo "bar, baz"

  - Perform validation of change regarding new user alias member(s)
      ./sudoadm -v -a -A foo "bar, baz"

  - Perform automated restoration of latest saved copy of sudoers
    configuration
      ./sudoadm -R

  - Perform interactive restoration of a prior saved copy of sudoers
    configuration
      ./sudoadm -R -i

  - Optionally create the specified sudoer configuration file if it
    doesn't exist
      ./sudoadm -n -f /etc/sudoers.d/foo.conf -a -A foo "bar, baz"

```


## contributing ##

Contributions are welcome & appreciated. Refer to the [contributing document](https://github.com/jas-/node-libnmap/blob/master/CONTRIBUTING.md)
to help facilitate pull requests.

## license ##

This software is licensed under the [MIT License](https://github.com/jas-/sudoadm/blob/master/LICENSE).

Copyright Jason Gerfen, 2015-2016.