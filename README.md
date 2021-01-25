# Reference
<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

**Classes**

* [`wireguard`](#wireguard): Wireguard class manages wireguard - an open-source software application
and protocol that implements virtual private network techniques to create
secure point-to-point connections in routed or bridged configurations.
* [`wireguard::config`](#wireguardconfig): Class configures files and directories for wireguard
* [`wireguard::install`](#wireguardinstall): Class installs wireguard packages and sets yum repository
* [`wireguard::params`](#wireguardparams): Class that contains OS specific parameters for other classes

**Defined types**

* [`wireguard::interface`](#wireguardinterface): Defines wireguard tunnel interfaces

**Functions**

* [`wireguard::genkey`](#wireguardgenkey): Returns an array containing the wireguard private and public (in this order) key for a certain interface.
* [`wireguard::genprivatekey`](#wireguardgenprivatekey): Returns the private key. Will be generated and saved to disk if it doesn't already exist.
* [`wireguard::genpsk`](#wireguardgenpsk): Returns string containing the wireguard psk for a certain interface.
* [`wireguard::genpublickey`](#wireguardgenpublickey): Returns a public key derived from a private key. Will be generated and saved to disk if it doesn't already exist.

## Classes

### wireguard

Wireguard class manages wireguard - an open-source software application
and protocol that implements virtual private network techniques to create
secure point-to-point connections in routed or bridged configurations.

* **See also**
https://www.wireguard.com/

#### Parameters

The following parameters are available in the `wireguard` class.

##### `package_name`

Data type: `Variant[Array, String]`

Name the package(s) that installs wireguard

Default value: $wireguard::params::package_name

##### `repo_url`

Data type: `String`

URL of wireguard repo

Default value: $wireguard::params::repo_url

##### `manage_repo`

Data type: `Boolean`

Should class manage yum repo

Default value: $wireguard::params::manage_repo

##### `manage_package`

Data type: `Boolean`

Should class install package(s)

Default value: $wireguard::params::manage_package

##### `package_ensure`

Data type: `Variant[Boolean, Enum['installed','latest','present']]`

Set state of the package

Default value: 'installed'

##### `config_dir`

Data type: `Stdlib::Absolutepath`

Path to wireguard configuration files

Default value: $wireguard::params::config_dir

##### `config_dir_mode`

Data type: `String`

The config_dir access mode bits

Default value: $wireguard::params::config_dir_mode

##### `interfaces`

Data type: `Optional[Hash]`

Define wireguard interfaces

Default value: {}

##### `config_dir_purge`

Data type: `Boolean`



Default value: $wireguard::params::config_dir_purge

### wireguard::config

Class configures files and directories for wireguard

#### Parameters

The following parameters are available in the `wireguard::config` class.

##### `config_dir`

Data type: `Stdlib::Absolutepath`

Path to wireguard configuration files

##### `config_dir_mode`

Data type: `String`

The config_dir access mode bits

##### `config_dir_purge`

Data type: `Boolean`



### wireguard::install

Class installs wireguard packages and sets yum repository

#### Parameters

The following parameters are available in the `wireguard::install` class.

##### `package_name`

Data type: `Variant[Array, String]`

Name the package(s) that installs wireguard

##### `repo_url`

Data type: `String`

URL of wireguard repo

##### `manage_repo`

Data type: `Boolean`

Should class manage yum repo

##### `manage_package`

Data type: `Boolean`

Should class install package(s)

##### `package_ensure`

Data type: `Variant[Boolean, Enum['installed','latest','present']]`

Set state of the package

### wireguard::params

Class that contains OS specific parameters for other classes

## Defined types

### wireguard::interface

Defines wireguard tunnel interfaces

#### Parameters

The following parameters are available in the `wireguard::interface` defined type.

##### `private_key`

Data type: `Any`

Private key for data encryption

##### `listen_port`

Data type: `Integer[1,65535]`

The port to listen

##### `ensure`

Data type: `Enum['present','absent']`

State of the interface

Default value: 'present'

##### `address`

Data type: `Optional[Variant[Array,String]]`

List of IP (v4 or v6) addresses (optionally with CIDR masks) to
be assigned to the interface.
Data type isn't 100% correct but needs to be 'Any' to allow 'Deferred'
on Puppet 6 systems. epp will enforce Optional[Variant[Array,String]].

Default value: `undef`

##### `mtu`

Data type: `Optional[Integer[1,9202]]`

Set MTU for the wireguard interface

Default value: `undef`

##### `preup`

Data type: `Optional[Variant[Array,String]]`

List of commands to run before the interface is brought up

Default value: `undef`

##### `postup`

Data type: `Optional[Variant[Array,String]]`

List of commands to run after the interface is brought up

Default value: `undef`

##### `predown`

Data type: `Optional[Variant[Array,String]]`

List of commands to run before the interface is taken down

Default value: `undef`

##### `postup`

List of commands to run after the interface is taken down

Default value: `undef`

##### `peers`

Data type: `Optional[Array[Struct[
    {
      'PublicKey'           => String,
      'AllowedIPs'          => Optional[String],
      'Endpoint'            => Optional[String],
      'PersistentKeepalive' => Optional[Integer],
      'PresharedKey'        => Optional[String],
      'Comment'             => Optional[String],
    }
  ]]]`

List of peers for wireguard interface

Default value: []

##### `dns`

Data type: `Optional[String]`

List of IP (v4 or v6) addresses of DNS servers to use

Default value: `undef`

##### `saveconfig`

Data type: `Boolean`

save current state of the interface upon shutdown

Default value: `true`

##### `config_dir`

Data type: `Stdlib::Absolutepath`

Path to wireguard configuration files

Default value: '/etc/wireguard'

##### `postdown`

Data type: `Optional[Variant[Array,String]]`



Default value: `undef`

## Functions

### wireguard::genkey

Type: Ruby 4.x API

Returns an array containing the wireguard private and public (in this order) key for a certain interface.

#### Examples

##### Creating private and public key for the interface wg0.

```puppet
wireguard::genkey('wg0', '/etc/wireguard') => [
  '2N0YBID3tnptapO/V5x3GG78KloA8xkLz1QtX6OVRW8=',
  'Pz4sRKhRMSet7IYVXXeZrAguBSs+q8oAVMfAAXHJ7S8=',
]
```

#### `wireguard::genkey(String $name, Optional[String] $path)`

Returns an array containing the wireguard private and public (in this order) key for a certain interface.

Returns: `Array` Returns [$private_key, $public_key].

##### Examples

###### Creating private and public key for the interface wg0.

```puppet
wireguard::genkey('wg0', '/etc/wireguard') => [
  '2N0YBID3tnptapO/V5x3GG78KloA8xkLz1QtX6OVRW8=',
  'Pz4sRKhRMSet7IYVXXeZrAguBSs+q8oAVMfAAXHJ7S8=',
]
```

##### `name`

Data type: `String`

The interface name.

##### `path`

Data type: `Optional[String]`

Absolut path to the wireguard key files (default '/etc/wireguard').

### wireguard::genprivatekey

Type: Ruby 4.x API

Returns the private key. Will be generated and saved to disk if it doesn't already exist.

#### Examples

##### Creating private key for the interface wg0.

```puppet
wireguard::genprivatekey('/etc/wireguard/wg0.key') => '2N0YBID3tnptapO/V5x3GG78KloA8xkLz1QtX6OVRW8='
```

##### Using it as a Deferred function

```puppet
include wireguard
wireguard::interface { 'wg0':
  private_key => Deferred('wireguard::genprivatekey', ['/etc/wireguard/wg0.key']),
  listen_port => 53098,
}
```

#### `wireguard::genprivatekey(String $path)`

Returns the private key. Will be generated and saved to disk if it doesn't already exist.

Returns: `String` Returns the private key.

##### Examples

###### Creating private key for the interface wg0.

```puppet
wireguard::genprivatekey('/etc/wireguard/wg0.key') => '2N0YBID3tnptapO/V5x3GG78KloA8xkLz1QtX6OVRW8='
```

###### Using it as a Deferred function

```puppet
include wireguard
wireguard::interface { 'wg0':
  private_key => Deferred('wireguard::genprivatekey', ['/etc/wireguard/wg0.key']),
  listen_port => 53098,
}
```

##### `path`

Data type: `String`

Absolut path to the private key

### wireguard::genpsk

Type: Ruby 4.x API

Returns string containing the wireguard psk for a certain interface.

#### Examples

##### Creating psk for the interface wg0.

```puppet
wireguard::genpsk('wg0') => 'FIVuvMyHvzujQweYa+oJdLDRvrpbHBithvMmNjN5rK4='
```

#### `wireguard::genpsk(String $name, Optional[String] $path)`

Returns string containing the wireguard psk for a certain interface.

Returns: `String` Returns psk.

##### Examples

###### Creating psk for the interface wg0.

```puppet
wireguard::genpsk('wg0') => 'FIVuvMyHvzujQweYa+oJdLDRvrpbHBithvMmNjN5rK4='
```

##### `name`

Data type: `String`

The interface name.

##### `path`

Data type: `Optional[String]`

Absolut path to the wireguard key files (default '/etc/wireguard').

### wireguard::genpublickey

Type: Ruby 4.x API

Returns a public key derived from a private key.
Will be generated and saved to disk if it doesn't already exist.

#### Examples

##### Creating public key for the interface wg0.

```puppet
wireguard::genpublickey('/etc/wireguard/wg0.key',
                         '/etc/wireguard/wg0.pub'
                        ) => 'gNaMjIpR7LKg019iktKJC74GX/MD3Y35Wo+WRNRQZxA='
```

#### `wireguard::genpublickey(String $private_key_path, String $public_key_path)`

Returns a public key derived from a private key.
Will be generated and saved to disk if it doesn't already exist.

Returns: `String` Returns the public key.

##### Examples

###### Creating public key for the interface wg0.

```puppet
wireguard::genpublickey('/etc/wireguard/wg0.key',
                         '/etc/wireguard/wg0.pub'
                        ) => 'gNaMjIpR7LKg019iktKJC74GX/MD3Y35Wo+WRNRQZxA='
```

##### `private_key_path`

Data type: `String`

Absolut path to the private key

##### `public_key_path`

Data type: `String`

Absolut path to the public key

