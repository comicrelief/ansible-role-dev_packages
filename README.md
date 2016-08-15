# Ansible role: Developer Packages

An Ansible role that installs Composer, NodeJs and manages their packages.

## Requirements

* Any php cli >= 5.5

## Role Variables

Available Variables are listed below, along with default values (see `default/main.yml`) and internal role values (see `vars/main.yml`):

### Defaults

```
packages_owner: user
packages_group: group
```

The owner and the group that Composer and NodeJs will be part of.

```
packages_composer: true
packages_composer_version: ''
packages_composer_home_path: ~/.composer
```

**packages_composer**: If this variable is true, the role will first check if Composer is installed and then it will install the packages defined.

**packages_composer_version**: The Composer version to be installed on the host.

**packages_composer_home_path**: The `COMPOSER_HOME` variable.

```
packages_composer_packages: {}
```

The Composer package(s) to be installed. The default variable is empty therefore the role won't install any package. If you want to define some packages, the dictionary accepts two values:

* name - name of the package to install (eg `phing/phing`)
* release - version of the package to install (eg `@latest`)

```
packages_nodejs: true
packages_nodejs_version: v4.4.7
packages_nodejs_arc: x64
```

**packages_nodejs**: If this variable is true, the role will first check if NodeJs is installed and then it will install the packages defined.

**packages_nodejs_version**: The NodeJs version to be installed on the host.

**packages_nodejs_arc**: The host processor Architecture used to assemble NodeJs download url.

```
packages_nodejs_npm_packages: {}
packages_nodejs_npm_config_dir: /usr/local/lib/npm
```

**packages_nodejs_npm_packages**: The Npm package(s) to be installed. The default variable is empty therefore the role won't install any package. If you want to define some packages, the dictionary accepts two values:

* name - name of the package to install (eg `grunt-cli`)
* release - version of the package to install (eg `latest`)

**packages_nodejs_npm_config_dir**: The directory where npm will install the given packages to.

```
packages_env_path: ''
```

The path to add to the PATH environment variable. If empty, it'll skip the task that writes it into `/etc/environment` file

### Internal Role Variables

These variables won't be changed very often.

```
packages_composer_path: /var/lib/composer
packages_composer_bin: composer
packages_composer_url: https://getcomposer.org/installer
```

**packages_composer_path**: The directory where Composer will be installed to.

**packages_composer_bin**: The name of the Composer binary.

**package_composer_url**: The url where the role will download Composer from.

```
packages_nodejs_path: /var/lib/nodejs
packages_nodejs_bin: node
packages_nodejs_npm_bin: npm
packages_nodejs_url: https://nodejs.org/dist/{{ package_nodejs_version }}/node-{{ package_nodejs_version }}-linux-{{ package_nodejs_arc }}.tar.xz
packages_nodejs_untar_dir: node-{{ package_nodejs_version }}-linux-{{ package_nodejs_arc }}
```

**packages_nodejs_path**: The directory where NodeJs will be installed to.

**packages_nodejs_bin**: The name of the NodeJs binary.

**packages_nodejs_npm_bin**: The name of the npm binary.

**packages_nodejs_url**: The url where the role will download NodeJs from.

**packages_nodejs_untar_dir**: The name of the uncompressed nodejs directory.

## Dependencies

None

## Kitchen

### Local Variables

Test kitchen reads the variables from a directory called `local` and they will be interpreted as Group Vars (see [Ansible Documentation](http://docs.ansible.com/ansible/intro_inventory.html#group-variables) for more info). Modify them if you want to do some test with your role.

### Create

To create the vm type:

```
$ kitchen create
```

### Provision

To provision the role type:

```
$ kitchen converge
```

### Login

To log in to the vm just type:

```
$ kitchen login
```

### Destroy

When you're done with your tests, you can destroy the vm by typing:

```
$ kitchen destroy
```

## License

MIT/BSD

## Author Information

This role was created in 2016 by [Davide Di Mauro](http://github.com/davidedimauro88), for [Comic Relief](http://comicrelief.com)
