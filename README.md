# Webarchitects Debian alternatives Ansible Role

An Ansible role to manage [Debian alternatives](https://wiki.debian.org/DebianAlternatives), see the [update-alternatives man page](https://manpages.debian.org/update-alternatives).

## Plan

The plan for this role is to have a `defaults/main.yml` containing a list of Debian alternatives we are interested in:

```yml
alternatives: true
alternatives_names:
  - php
  - phar
  - phar.phar
  - php-fpm.sock
```

And for this list to be used by a `/etc/ansible/facts.d/alternatives.fact` script which runs:

```bash
update-alternatives --get-selections
```

Then check that each `alternatives_names` is included in the first column and if it is then runs:

```bash
update-alternatives --query php
Name: php
Link: /usr/bin/php
Slaves:
 php.1.gz /usr/share/man/man1/php.1.gz
Status: auto
Best: /usr/bin/php8.1
Value: /usr/bin/php8.1

Alternative: /usr/bin/php7.4
Priority: 74
Slaves:
 php.1.gz /usr/share/man/man1/php7.4.1.gz

Alternative: /usr/bin/php8.0
Priority: 80
Slaves:
 php.1.gz /usr/share/man/man1/php8.0.1.gz

Alternative: /usr/bin/php8.1
Priority: 81
Slaves:
 php.1.gz /usr/share/man/man1/php8.1.1.gz
```

And then this is used to generate `ansible_local` facts like this:

```yml
alternatives:
  - name: php
    state: present
    link: /usr/bin/php
    best: /usr/bin/php8.1
    value: /usr/bin/php8.1
    alternatives:
      - path: /usr/bin/php7.4
        state: present
        priority: 74
      - path: /usr/bin/php8.0
        state: present
        priority: 80
      - path: /usr/bin/php8.1
        state: present
        priority: 81
```

And to set alternatives in the [main/defaults.yml](main/defaults.yml) file:

```
alternatives:
  - name: php
    state: present
    alternatives:
      - path: /usr/bin/php7.4
        state: present
        priority: 74
      - path: /usr/bin/php8.0
        state: present
        priority: 80
      - path: /usr/bin/php8.1
        state: present
        priority: 81
```



