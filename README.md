# Webarchitects Debian alternatives Ansible Role

An Ansible role to manage [Debian alternatives](https://wiki.debian.org/DebianAlternatives), see the [update-alternatives man page](https://manpages.debian.org/update-alternatives).

This role requires [jc](https://git.coop/webarch/jq) version 1.18.8 or greater and [yc](https://git.coop/webarch/yq) can be used to convert JSON to YAML for the generation of the configuration, for example this command:

```bash
jc -p update-alternatives --query editor | yq -P
```

Will generate a block of YAML that can be edited as necessary and used with this role as a item in the `alternatives_update` array.

If the results of `jc -p update-alternatives --query editor` match the supplied configuration then all the update tasks will be skipped.

If a `state` variable is added into the settings array then this can be set to `absent` to remove alternatives, see the [defaults/main.yml](defaults/main.yml) for an example.

