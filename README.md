oracle_java
===========

Ansible role which installs a particulat version of Oracle Java. It only works
for RedHat at the moment and it requires you to configure YUM repo from which the
Oracle Java RPM is intalled (see
[`yumrepo`](https://github.com/picotrading/ansible-yumrepo) and
[`pulp`](https://github.com/picotrading/ansible-yumrepo)). You can use this role
to install multiple version of Oracle Java and choose which one is the default
one for which the `/usr/bin/` links will be created. All Java packages not
managed by this role will be automatically uninstalled.


Example
-------

```
---

# Example of how to install default version (jdk-1.7.0_71)
- hosts: myhost1
  roles:
    - role: oracle_java
      oracle_java_finish: yes

# Example of how to install a particular version (jre-1.8.0_25)
- hosts: myhost2
  roles:
    - role: oracle_java
      oracle_java_distribution: jre
      oracle_java_version_minor: 8
      oracle_java_version_update: 25
      oracle_java_finish: yes

# Example of installation of multiple versions (version jdk-1.8.0_25 will be
# set as default):
- hosts: myhost3
  roles:
    - role: oracle_java
      oracle_java_distribution: jre
      oracle_java_version_minor: 8
      oracle_java_version_update: 25
    - role: oracle_java
      oracle_java_distribution: jdk
      oracle_java_version_minor: 7
      oracle_java_version_update: 71
      oracle_java_default: no
      oracle_java_finish: yes

# Example of how to uninstall all Java packages
- hosts: myhost4
  roles:
    - role: common/oracle_java
      oracle_java_distribution: none
      oracle_java_finish: yes
```


Role variables
--------------

List of variables used by the role:

```
# Default Java distribution [jdk|jre|none]
oracle_java_distribution: jdk

# Default major version
oracle_java_version_major: 1

# Default minor version
oracle_java_version_minor: 7

# Default patch version
oracle_java_version_patch: 0

# Default update version
oracle_java_version_update: 71

# Indicates whether this Java versin should be set as default alternative
oracle_java_default: false

# Flag which triggers the package cleaning
oracle_java_finish: false
```


License
-------

MIT


Author
------

Jiri Tyr
