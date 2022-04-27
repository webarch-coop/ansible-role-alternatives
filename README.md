# Webarchitects Debian alternatives Ansible Role

An Ansible role to manage [Debian alternatives](https://wiki.debian.org/DebianAlternatives), see the [update-alternatives man page](https://manpages.debian.org/update-alternatives).

This role requires [jc](https://git.coop/webarch/jq) version 1.18.8 or greater and also haveing [yc](https://git.coop/webarch/yq) installed helps with the generation of the configuration, for example this command:

```bash
jc -p update-alternatives --query editor | yq -P
```

Will generate a block of YAML that can be edited as necessary and used with this role as a item in the `alternatives_update` array.



