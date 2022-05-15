# Webarchitects Debian alternatives Ansible Role

An Ansible role to manage [Debian alternatives](https://wiki.debian.org/DebianAlternatives), see the [update-alternatives man page](https://manpages.debian.org/update-alternatives).

This role requires [jc](https://git.coop/webarch/jq) version 1.18.8 or greater to generate JSON from the output of `update-alternatives --query`.

[yc](https://git.coop/webarch/yq) can be used to convert JSON to YAML for the generation of the configuration, for example this command:

```bash
jc -p update-alternatives --query editor | yq -P
```

Will generate a block of YAML that can be edited as necessary and used with this role as a item in the `alternatives_update` array.

The Ansible managed alternatives are listed in the `/etc/ansible/alternatives` file, one per line, and the `/etc/ansible/facts.d/update_alternatives.fact` script generates JSON facts for each listed alternative.

If the supplied configuration matches and facts then all the update tasks will be skipped.

If a `state` variable is added into the settings array then this can be set to `absent` to remove alternatives, it defaults to `present`, see the [defaults/main.yml](defaults/main.yml) for an example.

