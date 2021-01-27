# Vopster: Project Manager

:warning: **Warning** :warning:

```diff
--
- This project is under continuous development, and it is NOT production-ready yet.
- The installer is not published, yet.
- Stay tuned by following.
--
```

**Table of contents**

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Vopster: Project Manager](#vopster-project-manager)
  - [Introduction](#introduction)
  - [Goals & Roadmap](#goals-roadmap)
    - [2021](#2021)
    - [2022](#2022)
  - [System Requirements](#system-requirements)
        - [OS Support](#os-support)
        - [Dependencies](#dependencies)
  - [Installation](#installation)
        - [Linux](#linux)
  - [Modules](#modules)
    - [Module: System](#module-system)
      - [Commands](#commands)
        - [system:start](#systemstart)
        - [system:stop](#systemstop)
        - [system:restart](#systemrestart)
        - [system:update](#systemupdate)
        - [system:config:set](#systemconfigset)
        - [system:config:get](#systemconfigget)
    - [Module: Project](#module-project)
      - [Project file structure](#project-file-structure)
      - [Commands](#commands-1)
        - [project:create](#projectcreate)
        - [project:delete](#projectdelete)
        - [project:build](#projectbuild)
        - [project:deploy](#projectdeploy)
        - [project:start](#projectstart)
        - [project:stop](#projectstop)
        - [project:restart](#projectrestart)
        - [project:backup:list](#projectbackuplist)
        - [project:backup:create](#projectbackupcreate)
        - [project:backup:restore](#projectbackuprestore)
        - [project:backup:delete](#projectbackupdelete)
        - [project:sync](#projectsync)
        - [project:config:set](#projectconfigset)
        - [project:config:get](#projectconfigget)
        - [project:cli](#projectcli)
    - [Module: Router](#module-router)
      - [Plugins](#plugins)
        - [Traefik](#traefik)
        - [HAProxy `[NYI]`](#haproxy-nyi)
        - [Nginx reverse-proxy `[NYI]`](#nginx-reverse-proxy-nyi)
        - [Zookeeper `[NYI]`](#zookeeper-nyi)
      - [Commands](#commands-2)
        - [router:list](#routerlist)
        - [router:create](#routercreate)
        - [router:delete](#routerdelete)
        - [router:update](#routerupdate)
        - [router:alias:list](#routeraliaslist)
        - [router:alias:create](#routeraliascreate)
        - [router:alias:update](#routeraliasupdate)
        - [router:alias:delete](#routeraliasdelete)
        - [router:config:set](#routerconfigset)
        - [router:config:get](#routerconfigget)
    - [Module: Docker](#module-docker)
      - [Services](#services)
        - [Nginx](#nginx)
        - [Apache2](#apache2)
        - [PHP](#php)
        - [Node](#node)
        - [MariaDB](#mariadb)
        - [PostgreSQL](#postgresql)
        - [MongoDB](#mongodb)
        - [ApacheSolr](#apachesolr)
        - [ElasticSearch](#elasticsearch)
        - [Redis](#redis)
        - [Memcached](#memcached)
        - [Varnish](#varnish)
        - [phpMyAdmin](#phpmyadmin)
      - [Commands](#commands-3)
        - [docker:service:add](#dockerserviceadd)
        - [docker:service:remove](#dockerserviceremove)
        - [docker:service:upgrade](#dockerserviceupgrade)
    - [Module: Framework](#module-framework)
      - [Plugins](#plugins-1)
        - [Drupal](#drupal)
        - [WordPress](#wordpress)
        - [PrestaShop](#prestashop)
        - [What's next?](#whats-next)
      - [Commands](#commands-4)
        - [framework:add](#frameworkadd)
        - [framework:remove](#frameworkremove)
        - [framework:upgrade (experimental) `[NYI]`](#frameworkupgrade-experimental-nyi)
        - [framework:migrate (experimental) `[NYI]`](#frameworkmigrate-experimental-nyi)
    - [Module: Cloud](#module-cloud)
      - [Plugins](#plugins-2)
        - [Hetzner](#hetzner)
        - [DigitalOcean `[NYI]`](#digitalocean-nyi)
        - [AWS `[NYI]`](#aws-nyi)
      - [Commands](#commands-5)
        - [cloud:provider:register](#cloudproviderregister)
        - [cloud:provider:unregister](#cloudproviderunregister)
        - [cloud:server:list](#cloudserverlist)
        - [cloud:server:create](#cloudservercreate)
    - [Module: VSC](#module-vsc)
    - [Module: DNS](#module-dns)
      - [Plugins](#plugins-3)
        - [Mail-in-a-box (self-hosted)](#mail-in-a-box-self-hosted)
        - [Cloudflare `[NYI]`](#cloudflare-nyi)
        - [DNSimple `[NYI]`](#dnsimple-nyi)
  - [CI/CD guidelines](#cicd-guidelines)
  - [Module and plugin development guidelines](#module-and-plugin-development-guidelines)
  - [Workflow examples](#workflow-examples)
  - [F.A.Q.](#faq)
    - [Can I use `pm` for local-only development?](#can-i-use-pm-for-local-only-development)
    - [What's an environment in `pm`?](#whats-an-environment-in-pm)
    - [Can I use the same remote server for stage and prod environments?](#can-i-use-the-same-remote-server-for-stage-and-prod-environments)
    - [Can I build the dev environment?](#can-i-build-the-dev-environment)
    - [What is the use of environment versions?](#what-is-the-use-of-environment-versions)
    - [What frameworks are supported in the current version?](#what-frameworks-are-supported-in-the-current-version)
    - [What other frameworks will be supported?](#what-other-frameworks-will-be-supported)
    - [Is it possible to create a project without a pre-installed framework?](#is-it-possible-to-create-a-project-without-a-pre-installed-framework)
    - [Can I host multiple projects on the same server using `pm`?](#can-i-host-multiple-projects-on-the-same-server-using-pm)
    - [Can I use multiple cloud providers for the same project using `pm`?](#can-i-use-multiple-cloud-providers-for-the-same-project-using-pm)
    - [What are the premium alternatives to `pm`?](#what-are-the-premium-alternatives-to-pm)
    - [How can I contribute?](#how-can-i-contribute)
    - [Can I support the development in any other way?](#can-i-support-the-development-in-any-other-way)
  - [Credits](#credits)

<!-- /code_chunk_output -->

## Introduction

**Vopster's ProjectManager `pm`**, aims to integrate all the Dev-Ops tasks a full-stack web developer would ever need.

Yet, there are many premium solutions to handle such tasks, we built a tool what is completely **open-source** and all it needs is some "bare-metal".

## Goals & Roadmap

### 2021

- [ ] Make server orchestration easy. `[Q1]`
- [ ] Support all major web development frameworks. `[Q2]`
- [ ] Support all major cloud hosting providers. `[Q3]`
- [ ] Interactive project configuration through CLI. `[Q4]`
- [ ] Generalize web development workflow. `[Q4]`

### 2022

- [ ] Support all major domain name providers. `[Q1]`
- [ ] Support all major dns service providers. `[Q1]`
- [ ] Integrate tools for security management. `[Q2]`
- [ ] Framework upgrade and migration tasks. `[Q3]`
- [ ] Unified interface for server log management. `[Q3]`
- [ ] Provide a WebUI to simplify and generalize the management of web projects. `[Q4]`

## System Requirements

##### OS Support

- `Ubuntu / Debian`
- `Fedora / CentOS / RedHat`
- `MacOS`

##### Dependencies

- `git`
- `python3+`
- `docker`
- `docker-compose`

## Installation

##### Linux

```shell
# Not yet available.
# wget -qO pm-setup pm.vopster.com/releases/1.0.0/installer && sudo bash pm-setup
```

## Modules

Pluggable extensions to the main application.

### Module: System

**About**

This is the main module of `pm`. It handles system related tasks, such as updates and maintenance.

#### Commands

##### system:start

Starts all services.

```shell
pm system:start
```

##### system:stop

Stops all services.

```shell
pm system:stop
```

##### system:restart

Restarts all services.

```shell
pm system:restart
```

##### system:update

Updates `pm` to the latest version.

```shell
pm system:update
```

##### system:config:set

Sets a system configration value by its key.

```shell
pm system:config:set
```

| Argument    | Description |
| --------- | ----------- |
| `--key`   | Configuration key            |
| `--value` | Configuration value            |

##### system:config:get

Gets a system configration value by its key.

```shell
pm system:config:get
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--key`     | Configuration key           |

### Module: Project

**About**

Project module manages all project related operations.

#### Project file structure

```bash
$APP_PROJECTS_ROOT # The project storage directory defined in project-manager/.env
┣ <project_id> # The unique identifier of the project.
┃ ┣ app # The application.
┃ ┃ ┣ config
┃ ┃ ┣ build # Only used by staging and production environments.
┃ ┃ ┃ ┣ <env>-<version>
┃ ┃ ┃ ┃ ┣ .env # Environment specific configuration.
┃ ┃ ┃ ┗ ┗ ... # Built project source.
┃ ┃ ┣ src # The source code of the app.
┃ ┃ ┣ var # Variable files.
┃ ┃ ┃ ┣ data # Persistent storage for services.
┃ ┃ ┃ ┃ ┣ _shared # Shared data between environments and versions.
┃ ┃ ┃ ┃ ┃ ┣ ... # Other shared files
┃ ┃ ┃ ┃ ┃ ┣ files # Environment specific persistent files.
┃ ┃ ┃ ┃ ┃ ┃ ┣ public
┃ ┃ ┃ ┃ ┃ ┃ ┣ private
┃ ┃ ┃ ┃ ┃ ┗ ┗ tmp
┃ ┃ ┃ ┃ ┣ <env>-<version> # Environment specific persistent storage.
┃ ┃ ┃ ┃ ┃ ┣ db # The database storage.
┃ ┃ ┃ ┃ ┃ ┃ ┣ mysql
┃ ┃ ┃ ┃ ┃ ┃ ┣ postgresql
┃ ┃ ┃ ┃ ┃ ┃ ┣ mongodb
┃ ┃ ┃ ┃ ┃ ┃ ┗ ... # Other database storage.
┃ ┃ ┃ ┃ ┃ ┣ files # Media and other files.
┃ ┃ ┃ ┃ ┃ ┃ ┣ public
┃ ┃ ┃ ┃ ┃ ┃ ┣ private
┃ ┃ ┃ ┃ ┃ ┃ ┗ tmp
┃ ┃ ┃ ┃ ┃ ┣ search # Search service persistent files.
┃ ┃ ┗ ┗ ┗ ┗ cache # Cache service persistent files.
┃ ┣ docker # Docker service definitions.
┃ ┃ ┗ <env>-<version>
┗ ┗ project.yml # Project definition.
```

#### Commands

##### project:create

Creates the file structure, including the project definition file: `project.yml`.

```shell
pm project:create
```
Available arguments:

<table>
<thead>
  <tr>
    <th>
      Argument
    </th>
    <th>
      Description
    </th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>--id</code></td>
    <td>The unique identifier of the project.</td>
  </tr>
  <tr>
    <td><code>--build</code></td>
    <td>Builds the project from the generated <code>project.yml</code></td>
  </tr>
  <tr>
    <td><code>--start</code></td>
    <td>Starts all services after build.</td>
  </tr>
  <tr>
    <td colspan="2" align="center"><strong>Framework</strong></td>
  </tr>
  <tr>
    <td width="250"><code>--framework</code></td>
    <td>
    <p>The framework to install / use with the project.</p>
    <p>
      Available options: <code>drupal:7</code> <code>drupal:8</code> <code>drupal:9</code> <code>wordpress:4</code> <code>wordpress:5</code> <code>prestashop:1.6</code> <code>prestashop:1.7</code>
    </p>
    <p>Default: <code>None</code></p>
    </td>
  </tr>
  <tr>
    <td width="250"><code>--framework:addon:add</code></td>
    <td>
    <p>Adds an extension for the framework.</p>
    <p>
      <strong>Global</strong> framework addons:
      <ul>
        <li><code>php:composer</code> - default</li>
        <li><code>php:grunt</code></li>
        <li><code>php:gulp</code></li>
        <li><code>php:platformsh</code></li>
        <li><code>db:mysqltuner</code></li>
      </ul>
      <strong>Drupal</strong> framework addons:
      <ul>
        <li><code>php:drush</code> - default</li>
        <li><code>php:drupalconsole</code> - default</li>
      </ul>
      <strong>WordPress</strong> framework addons:
      <ul>
        <li><code>php:wp-cli</code> - default</li>
      </ul>
    </p>
    </td>
  </tr>
  <tr>
    <td width="250"><code>--framework:addon:remove</code></td>
    <td>
    <p>Removes any default extension from the framework.</p>
    </td>
  </tr>
  <tr>
    <td colspan="2" align="center"><strong>Docker services</strong></td>
  </tr>
  <tr>
    <td><code>--docker:service:add</code></td>
    <td>
      <p>Adds a services to the <code>project.yml</code></p>
      <p>
        Available options: <code>solr</code> <code>elastic</code> <code>redis</code> <code>memcached</code> <code>rsyslog</code>
      </p>
    </td>
  </tr>
  <tr>
    <td><code>--docker:service:remove</code></td>
    <td>Removes any default services recommended for a framework.</td>
  </tr>
  <tr>
    <td colspan="2" align="center"><strong>Cloud</strong></td>
  </tr>
  <tr>
    <td><code>--cloud:provider:register</code></td>
    <td>
      <p>Registers a cloud provider to manage server instances from the CLI.</p>
      <p>
        Available options: <code>hetzner</code> <code>digitalocean</code> <code>aws</code>
      </p>
    </td>
  <tr>
    <td><code>--cloud:server:ip</code></td>
    <td>
      <p>If a server was already created, it can be attached to the project with its IP address. For remote management, the <code>pm</code> client must be able to connect to the server through <code>ssh</code>. </p>
    </td>
  </tr>
  <tr>
    <td><code>--cloud:server:ssh-user</code></td>
    <td>
      <p>The ssh user used for the connection.</p>
    </td>
  </tr>
  <tr>
    <td><code>--cloud:server:ssh-key</code></td>
    <td>
      <p>The ssh private key used for the connection.</p>
      <p>Default: <code>~/.ssh/id_rsa</code></p>
    </td>
  </tr>
  <tr>
    <td colspan="2" align="center"><strong>Version Control</strong></td>
  </tr>
  <tr>
    <td><code>--vsc:type</code></td>
    <td>
      <p>The type of the VSC platform.</p>
      <p>Available options: <code>github</code> <code>gitlab</code> <code>bitbucket</code></p>
      <p>Default: <code>github</code></p>
    </td>
  </tr>
  <tr>
    <td><code>--vsc:repository</code></td>
    <td>Sets the repository URL for the project.</td>
  </tr>
  <tr>
    <td><code>--vsc:name</code></td>
    <td>Sets the username used for version control.</td>
  </tr>
  <tr>
    <td><code>--vsc:email</code></td>
    <td>Sets the email used for version control.</td>
  </tr>
  <tr>
    <td colspan="2" align="center"><strong>Router</strong></td>
  </tr>
  <tr>
    <td><code>--router:domain</code></td>
    <td>
      <p>The public domain of the project.</p>
      <p>Example: <code>example.com</code></p>
    </td>
  </tr>
  <tr>
    <td><code>--router:domain:alias</code></td>
    <td>
      <p>Adds one or multiple domain aliases to the project.</p>
      <p>Value format: <code>alias-id:alias-value</code></p>
      <p>Example value: <code>gb:example.co.uk</code></p>
    </td>
  </tr>
  <tr>
    <td><code>--router:domain:https</code></td>
    <td>
      <p>Enables https for <code>stage</code> and <code>prod</code> environments using <code>letsencrypt</code> as a default provider. Also creates an automatic redirect from http to https.</p>
    </td>
  </tr>
  <tr>
    <td><code>--router:domain:root</code></td>
    <td>
      <p>Sets the web-root of the project.</p>
      <p>Default: <code>/var/www/html</code></p>
    </td>
  </tr>
</tbody>
</table>


##### project:delete

Deletes a project or a project environment.

```shell
pm project:delete
```

| Argument               | Description                                    |
| -------------------- | ---------------------------------------------- |
| `--id`               | The unique identifier of the project. |
| `--env`              | The environment. |

##### project:build

Builds a specific environment from _project.yml_.

```shell
pm project:build
```

Available arguments:

| Argument                | Description |
| --------------------- | ----------- |
| `--id`                |   The unique identifier of the project.          |
| `--env`               |   The environment.          |
| `--version`           |   A version tag of format `major-minor`.          |

##### project:deploy

Deploys a specific environment / version to the server used by the project.

```shell
pm project:deploy
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project.          |
| `--env`     | The environment.            |
| `--version` | A built version tag.            |

##### project:start

Starts all services of the project environment.

```shell
pm project:start
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project. |
| `--env`     | The environment. |

##### project:stop

Stops all services of the project environment.

```shell
pm project:stop
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project.            |
| `--env`     | The environment.            |


##### project:restart

Restarts all services of the project environment.

```shell
pm project:restart
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project.            |
| `--env`     | The environment.            |

##### project:backup:list

Lists the current backups of the project.

```shell
pm project:backup:list
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project.            |
| `--env`     | The environment.            |

##### project:backup:create

Creates a full backup of the project environment, including files and databases.

```shell
pm project:backup:create
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project.            |
| `--env`     |             |
| `--backup`  |             |

##### project:backup:restore

Restores a backup by its ID.

```shell
pm project:backup:restore
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project.            |
| `--env`     |             |
| `--backup`  |             |

##### project:backup:delete

Deletes a backup by its ID.

```shell
pm project:backup:create
```

Available arguments:

| Argument      | Description |
| ----------- | ----------- |
| `--id`      | The unique identifier of the project.            |
| `--env`     |             |
| `--backup`  |             |

##### project:sync

Synchronizes a project environment to local.

```shell
pm project:sync
```

Available arguments:

| Argument   | Description                                    |
| --------- | ---------------------------------------------- |
| `--source`| The environment to sync the data from. |
| `--all`   | Default option if no other flag was specified. |
| `--files` | Sync media files.                              |
| `--db`    | Sync database(s).                              |

##### project:config:set

Sets a project configuration value by key.

```shell
pm project:config:set
```

Available arguments:

| Argument    | Description                                    |
| --------- | ---------------------------------------------- |
| `--id`    | The unique identifier of the project. |
| `--env`   | |
| `--key`   | |
| `--value` | |

##### project:config:get

Returns a project configuration value by key.

```shell
pm project:config:get
```

Available arguments:

| Argument  | Description |
| ------- | ----------- |
| `--id`  | The unique identifier of the project. |
| `--env` |             |
| `--key` | |

##### project:cli

Opens a terminal connection to the service. If **--stage** or **--prod** flag is provided, a remote connection will be opened to the server / environment.

```shell
pm project:cli
```

Available arguments:

| Argument | Description                           |
| -------- | ------------------------------------- |
| `--id`   | The unique identifier of the project. |
| `--env`  |                                       |
| `--service` | |

### Module: Router

**About**
This module is responsible for the network traffic distribution. It allows attaching domains and domain aliases / subdomains to a project / environment using various rules.

Routers are also installed as services. This module provides an abstract connector between the projects and the router.

#### Plugins

##### Traefik

The default router used by `pm`. It handles the private and public network traffic.

##### HAProxy `[NYI]`

A basic HAProxy to route the network traffic.

##### Nginx reverse-proxy `[NYI]`

A basic nginx reverse proxy implementation to route network traffic.

##### Zookeeper `[NYI]`

#### Commands

##### router:list

```shell
pm router:list
```

Available arguments:

| Argument | Description                           |
| -------- | ------------------------------------- |
| `--project`   | The unique identifier of the project. |
| `--env`  |                                       |

##### router:create

```shell
pm router:create
```

Available arguments:

| Argument    | Description                                    |
| --------- | ---------------------------------------------- |
| `--project`    | The unique identifier of the project. |
| `--env`   | |

##### router:delete

Completely removes the router definition, including aliases.

```shell
pm router:delete
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--env`     |                                       |

##### router:update

```shell
pm router:update
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--env`     |                                       |

##### router:alias:list

```shell
pm router:alias:list
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--env`     |                                       |

##### router:alias:create

```shell
pm router:alias:create
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--env`     |                                       |

##### router:alias:update

```shell
pm router:alias:update
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--env`     |                                       |

##### router:alias:delete

```shell
pm router:alias:delete
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--env`     |                                       |

##### router:config:set

```shell
pm router:config:set
```

Available arguments:

| Argument  | Description |
| --------- | ----------- |
| `--key`   |             |
| `--value` |             |

##### router:config:get

```shell
pm router:config:get --key=config-key
```

| Argument | Description |
| -------- | ----------- |
| `--key`  |             |

### Module: Docker

**About**

This module is responsible to handle docker and service related tasks. It creates the required dockerfile definitions and docker-compose files for the project.

#### Services

##### Nginx

| Key                | Value                                            |
| ------------------ | ------------------------------------------------ |
| Supported versions | `1.13` `1.14` `1.15` `1.16` `1.17` `1.18` `1.19` |
| Default version    | `1.19`                                           |
| Supported images   | - [wodby/nginx](https://github.com/wodby/nginx)  |
| Default image      | `wodby/nginx`                                    |

##### Apache2

| Key                | Value                                             |
| ------------------ | ------------------------------------------------- |
| Supported versions | `2.4`                                             |
| Default version    | `2.4`                                             |
| Supported images   | - [wodby/apache](https://github.com/wodby/apache) |
| Default image      | `wodby/apache`                                    |

##### PHP

| Key                | Value                                       |
| ------------------ | ------------------------------------------- |
| Supported versions | `7.3` `7.4` `8.0`                           |
| Default version    | `7.4`                                       |
| Supported images   | - [wodby/php](https://github.com/wodby/php) |
| Default image      | `wodby/php`                                 |

##### Node

| Key                | Value                                         |
| ------------------ | --------------------------------------------- |
| Supported versions | `8.17` `10.23` `12.20` `14.15`                |
| Default version    | `12.20`                                       |
| Supported images   | - [wodby/node](https://github.com/wodby/node) |
| Default image      | `wodby/node`                                  |

##### MariaDB

| Key                | Value                                               |
| ------------------ | --------------------------------------------------- |
| Supported versions | `10.3` `10.4` `10.5`                                |
| Default version    | `10.5`                                              |
| Supported images   | - [wodby/mariadb](https://github.com/wodby/mariadb) |
| Default image      | `wodby/mariadb`                                     |

##### PostgreSQL

| Key                | Value                                                 |
| ------------------ | ----------------------------------------------------- |
| Supported versions | `10` `11` `12` `13`                                   |
| Default version    | `13`                                                  |
| Supported images   | - [wodby/postgres](https://github.com/wodby/postgres) |
| Default image      | `wodby/postgres`                                      |

##### MongoDB

| Key                | Value                                              |
| ------------------ | -------------------------------------------------- |
| Supported versions | `3.6` `4.0` `4.2` `4.4`                            |
| Default version    | `4.4`                                              |
| Supported images   | - [mongo](https://github.com/docker-library/mongo) |
| Default image      | `mongo`                                            |

##### ApacheSolr

| Key                | Value                                         |
| ------------------ | --------------------------------------------- |
| Supported versions | `5.5` `6.6` `7.5` `7.6` `7.7` `8.7`           |
| Default version    | `8.7`                                         |
| Supported images   | - [wodby/solr](https://github.com/wodby/solr) |
| Default image      | `wodby/solr`                                  |

##### ElasticSearch

| Key                | Value                                                           |
| ------------------ | --------------------------------------------------------------- |
| Supported versions | `5.8` `7.10`                                                    |
| Default version    | `7.10`                                                          |
| Supported images   | - [wodby/elasticsearch](https://github.com/wodby/elasticsearch) |
| Default image      | `wodby/elasticsearch`                                           |

##### Redis

| Key                | Value                                           |
| ------------------ | ----------------------------------------------- |
| Supported versions | `5.0` `6.0`                                     |
| Default version    | `6.0`                                           |
| Supported images   | - [wodby/redis](https://github.com/wodby/redis) |
| Default image      | `wodby/redis`                                   |

##### Memcached

| Key                | Value                                                   |
| ------------------ | ------------------------------------------------------- |
| Supported versions | `1.6`                                                   |
| Default version    | `1.6`                                                   |
| Supported images   | - [wodby/memcached](https://github.com/wodby/memcached) |
| Default image      | `wodby/memecahed`                                       |

##### Varnish

| Key                | Value                                               |
| ------------------ | --------------------------------------------------- |
| Supported versions | `4.1` `6.0`                                         |
| Default version    | `6.0`                                               |
| Supported images   | - [wodby/varnish](https://github.com/wodby/varnish) |
| Default image      | `wodby/varnish`                                     |

##### phpMyAdmin

| Key                | Value                                                           |
| ------------------ | --------------------------------------------------------------- |
| Supported versions | `5.0`                                                           |
| Default version    | `5.0`                                                           |
| Supported images   | - [phpmyadmin/phpmyadmin](https://github.com/phpmyadmin/docker) |
| Default image      | `phpmyadmin/phpmyadmin`                                         |

#### Commands

> **Note:** Docker commands mostly work in the dev environment. Changes applied through these commands are usually deployed to other environments.

##### docker:service:add

Adds a service to a project.

```shell
pm docker:service:add
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--service` |                                       |

##### docker:service:remove

Removes a service from a project.

```shell
pm docker:service:remove
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--service` |                                       |

##### docker:service:upgrade

Upgrades a service of the project.

```shell
pm docker:service:upgrade
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |
| `--service` |                                       |

### Module: Framework

**About**

This module handles the framework management tasks, such as installation, upgrade or removal of pre-defined / available frameworks.

#### Plugins

##### Drupal

| Key                 | Value                                 |
| ------------------- | ------------------------------------- |
| Supported versions  | `7.x` `8.x` `9.x`                     |
| Default services    | `nginx:1.19` `php:7.4` `mariadb:10.5` |
| Compatible services | `solr` `elastic` `redis` `memcached`  |

Available add-ons:

- **php:** `drush` `drupalconsole` `composer` `grunt` `gulp` `node`
- **mariadb:** `mysqltuner`

##### WordPress

| Key                 | Value                                 |
| ------------------- | ------------------------------------- |
| Supported versions  | `4.x` `5.x`                           |
| Default services    | `nginx:1.19` `php:7.4` `mariadb:10.5` |
| Compatible services | `solr` `elastic` `redis` `memcached`  |

Available add-ons:

- **php:** `wp-cli` `composer` `grunt` `gulp`
- **mariadb:** `mysqltuner`

##### PrestaShop

| Key                 | Value                                 |
| ------------------- | ------------------------------------- |
| Supported versions  | `1.6.x` `1.7.x`                       |
| Default services    | `nginx:1.19` `php:7.4` `mariadb:10.5` |
| Compatible services | `solr` `elastic` `redis` `memcached`  |

Available add-ons:

- **php:** `composer` `grunt` `gulp`
- **mariadb:** `mysqltuner`

##### What's next?

**PHP**

- `Laravel`
- `Magento`
- `CodeIgniter`
- `Symfony`
- `Zend`
- `PHalcon`

**Python**

- `Django`
- `CherryPy`

**Node**

- `AdonisJS`
- `ExpressJS`
- `MeteorJS`
- `Sails.js`

#### Commands

##### framework:add

Adds a framework definition to the `project.yml`. A project can only have one framework.

```shell
pm framework:add
```
Available arguments:

| Argument      | Description                           |
| ------------- | ------------------------------------- |
| `--project`   | The unique identifier of the project. |
| `--framework` |                                       |

##### framework:remove

Removes the current framework definition from the `project.yml`.

```shell
pm framework:remove
```

Available arguments:

| Argument      | Description                           |
| ------------- | ------------------------------------- |
| `--project`   | The unique identifier of the project. |

##### framework:upgrade (experimental) `[NYI]`

Runs compatibility checks over the codebase and upgrades the framework to the target version, keeping all custom code as it is.

```shell
pm framework:upgrade
```

Available arguments:

| Argument      | Description                           |
| ------------- | ------------------------------------- |
| `--project`   | The unique identifier of the project. |
| `--framework:version` |                                       |

##### framework:migrate (experimental) `[NYI]`

Migrates the project from a framework to another into a new dev environment.

```shell
pm framework:migrate
```

Available arguments:

| Argument      | Description                           |
| ------------- | ------------------------------------- |
| `--project`   | The unique identifier of the project. |
| `--target-framework` |                                       |

### Module: Cloud

**About**

This module integrates cloud management APIs. It creates / removes servers and provides management tasks for other modules.

#### Plugins

##### Hetzner

##### DigitalOcean `[NYI]`

##### AWS `[NYI]`

#### Commands

##### cloud:provider:register

Registers a cloud provider to the project.

```shell
pm cloud:provider:register
```

Available arguments:

| Argument                    | Description                           |
| --------------------------- | ------------------------------------- |
| `--project`                 | The unique identifier of the project. |
| `--provider` |                                       |
| `--token`                   |                                       |

##### cloud:provider:unregister

Unregisters a cloud provider from the project.

```shell
pm cloud:provider:register
```

Available arguments:

| Argument                    | Description                           |
| --------------------------- | ------------------------------------- |
| `--project`                 | The unique identifier of the project. |
| `--provider` |                                       |


##### cloud:server:list

Lists all servers of the project.

```shell
pm cloud:server:list
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |

##### cloud:server:create

Creates and adds a cloud server to the project.

```shell
pm cloud:server:create
```

Available arguments:

| Argument    | Description                           |
| ----------- | ------------------------------------- |
| `--project` | The unique identifier of the project. |

### Module: VSC

**About**

This is a bridge module to handle version control related tasks.

### Module: DNS

**About**

#### Plugins

##### Mail-in-a-box (self-hosted)

##### Cloudflare `[NYI]`

##### DNSimple `[NYI]`

## CI/CD guidelines

> .. soon ..

## Module and plugin development guidelines

> .. soon ..

## Workflow examples

> .. soon ..

## F.A.Q.

### Can I use `pm` for local-only development?

> Yes. In this case building your application is not mandatory, since you will be only working on your `dev` environment.

### What's an environment in `pm`?

> Environments are isolated copies of the application. There are 3 pre-defined environments: _dev_, _stage_ and _prod_:
>
> **dev:** Used for development, served from the src/ directory of the application. This is a local environment.
>
> **stage:** Used for testing. This environment holds the latest version of the app which will be published into the production environment. This environment runs on a remote server.
>
> **prod:** This environment is the released application. This environment runs on a remote server.

### Can I use the same remote server for stage and prod environments?

> Yes, since environments are isolated, stage and prod can be deployed on the same, or different servers.

### Can I build the dev environment?

> No. The local dev environment uses the raw _src/_ directory to serve the project, and the build command only accepts the **--stage** and **--prod** flags.

### What is the use of environment versions?

> They help in quick reverts (if something goes wrong during the deploy). Built environments have a version like **prod-0.0.1**, **prod-0.0.2**, and so on. Assuming that prod-0.0.2 was deployed and "something isn't right with it", we can revert with one command to prod-0.0.1, which was the latest stable release.

### What frameworks are supported in the current version?

> The current version supports the following frameworks:
>
> **PHP:**
>
> - Drupal: `7.x`, `8.x`, `9x`
> - WordPress: `4.x`, `5.x`
> - PrestaShop `1.6.x`, `1.7.x`

### What other frameworks will be supported?

> The current version supports the following frameworks:
>
> **PHP:**
>
> - Laravel
> - Magento
> - CodeIgniter
> - Symfony
> - Zend
> - PHalcon
>
> **Python:**
>
> - Django
> - CherryPy
>
> **Node:**
>
> - AdonisJS
> - ExpressJS
> - MeteorJS
> - Sails.js

### Is it possible to create a project without a pre-installed framework?

> Yes. The framework flag is only optional.

### Can I host multiple projects on the same server using `pm`?

> Yes. It is possible to host multiple projects on the same server.

### Can I use multiple cloud providers for the same project using `pm`?

> Yes. It is possible to connect multiple providers to the same project.

### What are the premium alternatives to `pm`?

> _..soon.._

### How can I contribute?

> Contributors are always welcome. Just check the issues and create your PR (respecting our guidelines) to contribute to the core development.
> It is also possible to write **modules** to integrate things, what we didn't think of (yet).

### Can I support the development in any other way?

> Yes. Since this is an open-source project, any donations are welcome to support the development costs.
> We're taking this project seriously, but are resources are limited. It would be great if we could allocate more time and interns to speed up things.

## Credits

Supporting organizations:

- [Vopster](vopster.com) (Romania, Oradea): [@vopster](https://github.com/vopster)

Contributors:

- [@vzsigmond](https://github.com/vzsigmond)
