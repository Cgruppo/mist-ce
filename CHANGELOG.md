# Changelog


## v3.0.1 (2 Jun 2018)

Bugfix and cleanup release. Adds polling for networks. Improves KVM machine creation. Improves DB query performance.

### Upgrading from v3.0.0

1. Bring down your existing installation by running `docker-compose down` within the directory where the docker-compose.yml file resides.
2. Replace docker-compose.yaml with the one available in the assets of the current release right above.
3. Bring everything back up by running `docker-compose up -d`. Check the status by running `docker-compose ps`.
4. Once all services are running, execute the following migration steps:

```
    docker-compose exec api python api/migrations/0011-migrate-networks.py
    docker-compose exec api python api/migrations/0012-add-metering-schedules.py
```


### Changes

* Feature: Support custom sizes when creating KVM machines.
* Bugfix: Fix KVM networks upon machine creation.
* Feature: Support multiple interfaces and attaching to more than one networks when creating KVM machines.
* Feature: Poller for networks.
* Change: Sharding of polling tasks.
* Change: Deprecate collectd support.
* Change: Support metering of datapoints.
* Change: Add owner index, improves performance of DB queries.
* Bugfix: Fix internal server error when editing some rules.


## v3.0.0 (29 Apr 2018)

Major new release of the Mist Cloud Management Platform, Community Edition. 

The Community Edition now integrates with Telegraf & InfluxDB to provide a fully open source infrastructure management & monitoring stack. It also includes a revamped alerting & automation engine that will apply your rules to any group of machines. We enhanced the support of many clouds, most notably vSphere, GCE & OpenStack. It's now possible to bring together machines into a single virtual "Cloud". The usability and performance of the UI was greatly improved. At the same time we've remorselessly eliminated more than a few bugs.

A new plugin system was introduced, which is currently used by the Enterprise Edition and the Hosted Service to provide add-on functionality like i) Role Based Access Control, ii) Cost Insights, iii) VPN tunnels, iv) Orchestration of multi-tier architectures like Kubernetes clusters, as well as v) metering & billing extensions.

You can purchase the Mist Enterprise Edition and the Mist Hosted Service at https://mist.io


### Changes

* Feature: Machine monitoring, using InfluxDB & Telegraf
* Feature: Alerting and automation rules on machine metrics, apply rules on groups of machines
* Feature: Interactive API docs using OpenAPI 3.0 spec & Swagger UI
* Feature: Poller for cloud locations & sizes
* Feature: Select network & subnetwork when creating GCE machine
* Feature: Support ClearCenter SDN as cloud
* Change: Improved vSphere support
* Change: UI performance improvements
* Change: Support for plugins
* Bugfix: Too many bugfixes to count


## v2.6.0 (10 Dec 2017)

### Changes

* Feature: Export CSV on any list
* Change: Improve layout in small screens
* Bugfix: Update required fields for provisioning in OpenStack
* Change: Remove deprecated polling tasks (!510)


## v2.5.0 (18 Nov 2017)

### Changes

* Feature: Chained actions in Rules, backend only (!475)
* Feature: CSV renderer for API results
* Feature: Send multipart emails when required
* Feature: List all machines view
* Change: Dismiss notifications menu
* Change: Async session update (!503)
* Change: Vsphere opts and metadata (!487)
* Bugfix: Catch me.NotUniqueError when renaming a Cloud


## v2.4.0 (27 Oct 2017)

### Changes

* Feature: Azurearm provisioning (!457)
* Feature: Improved Windows support
* Feature: Granular Notification Overrides (!460)
* Feature: Resize machine action for EC2, DigitalOcean, OpenStack
* Bugfix: Fix lock bug https://gitlab.ops.mist.io/mistio/mist.core/issues/1221 (!454)
* Bugfix: Properly read cost from tags for generic (non-libcloud) machines
* Bugfix: Fix ping parsing
* Bugfix: Fix poller computed property
* Change: Update xterm.js & fix shell display issues
* Change: Improve display of probe data
* Change: Exclude audit log ES templates (!473)
* Change: Run tests with headless Chrome (!442)
* Change: New rules models (!472)
* Change: Sso refresh token (!461)
* Change: Update docker/nginx/nginx.conf (!459)
* Change: Move ES template for cloudify-metrics to mist.io/docker/elasticsearch-manage (!458)


## v2.3.0 (19 Sep 2017)

### Changes

* Change: Whitelisting UI improvements (!446)
* Change: Insights UI improvements
* Bugfix: Catch invalid SSL cert for OnApp
* Change: Update GCE pricing, improve list sizes behavior


## v2.2.1 (8 Sep 2017)

### Changes

* Bugfix: Use tz aware objects in changelog.py (!445)
* Bugfix: Install dateutil for ci release step (!444)


## v2.2.0 (8 Sep 2017)

### Changes

* Feature: IP whitelisting (!434)
* Change: Do not hardcore repo name in release process (!382)
* Change: Ansible script example - update ref (!432)
* Change: Refactor poller (!420)
* Change: Change submodule paths (!426)
* Change: Update ES templates with merge policy (!419)
* Bugfix: Fix async permission mappings (!401)
* Change: Fix ordering and naming of crontab fields


## v2.1.0 (21 Jul 2017)

### Changes

* Change: Display stack logs grouped by workflow operation (!406)
* Change: Notifications API & UI improvements (!390) (!409)
* Change: Update to Libcloud v2
* Change: Apply stricter checks on the dns enabled cloud field (!404)
* Bugfix: Fix error in machine weight calculation
* Change: Update DNS API (!396)
* Bugfix: Fix association with a secondary key (!394)


## v2.0.0 (21 Jun 2017)

This is a major update of the open source version Mist.io with many of the
latest features and fixes from the Enterprise SaaS version available at
https://mist.io

It comes with a brand new UI based on Polymer and web components and introduces
new functionality.

For more details on the changes also check out the
[blog post](http://blog.mist.io/post/162083041316/our-biggest-mistio-open-source-release-yet).



### Changes

* Feature: Support for more cloud providers
* Feature: DNS management
* Feature: Manage private networks
* Feature: Support for running scripts (executables as well as Ansible playbooks)
* Feature: Scheduled tasks
* Feature: Tagging of all resources
* Feature: Cost reporting
* Feature: Support for multiple Users, Teams & Organizations (full RBAC support available in the Enterprise Edition)
