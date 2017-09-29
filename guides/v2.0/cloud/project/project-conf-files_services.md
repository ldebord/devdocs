---
layout: default
group: cloud
subgroup: 090_configure
title: services.yaml
menu_title: services.yaml
menu_order: 55
menu_node:
level3_menu_node: level3child
level3_subgroup: services
version: 2.0
github_link: cloud/project/project-conf-files_services.md
---

We provide a `services.yaml` file to configure all of your services supported and used by {{site.data.var.ece}}. These services include MySQL, PHP, Redis, Solr, and so on. You don't need to subscribe to external service providers.

This file is located at `.magento/services.yaml` in your project.

<div class="bs-callout bs-callout-info" id="info">
  <p>When you push your local environment to the remote server, our deploy script uses the values defined by configuration files in the <code>.magento</code> directory, then the script deletes the directory and its contents. Your local development environment isn't affected.</p>
</div>

[Sample `services.yaml` file](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml){:target="_blank"}

<div class="bs-callout bs-callout-info" id="info">
  <p>Changes you make using <code>.yaml</code> files affect your <a href="{{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-int">integration environment</a> only. For technical reasons, neither <a href="{{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-stage">staging</a> nor <a href="{{ page.baseurl }}cloud/reference/discover-arch.html#cloud-arch-prod">production</a> environments use <code>.yaml</code> files. To make these changes in a staging or production environment, you must create a <a href="{{ page.baseurl }}cloud/bk-cloud.html#gethelp">Support issue</a>.</p>
</div>


The following sections discuss properties in `services.yaml`.

## Defaults {#cloud-yaml-services-default}
If you do not provide a `services.yaml` file, the following defaults are used:

	mysql:
	   type: mysql:10.0
	   disk: 2048

	redis:
	   type: redis:3.0

	solr:
	   type: solr:4.10
	   disk: 1024

## `name` {#cloud-yaml-services-name}
`name` identifies the service in the project. `name` can consist only of lower case alphanumeric characters; that is, `a`&ndash;`z` and `0`&ndash;`9`.

Usually you will see in our examples that we simply call the mysql: `mysql`. Note that you can have multiple instances of each service.

<div class="bs-callout bs-callout-warning">
    <p>Because we support multiple services of the same type (for example, multiple databases), changing the name of a service in <code>services.yaml</code> causes the existing service to be <em>permanently removed</em> before creating a new service with the new name you specify. <em>Renaming a service results in the loss of all of that service's data</em>. We strongly recommend you <a href="{{page.baseurl}}cloud/admin/admin-snap.html">snapshot your environment</a> before you change the name of an existing service.</p>
</div>

### `type` {#cloud-yaml-services-type}
The `type` of your service in the format `type:version`

We support and deploy the following services for you:

*	`mysql` version `10.0`
*	`redis` versions `2.8` and `3.0`
*	`solr` version `4.0`
*	`elasticsearch` version `1.7`
*	`rabbitmq` version `3.5`

### `disk` {#cloud-yaml-services-disk}

`disk` specifies the size of the persistent disk storage (in MB) allocated to the service.

For example, the current default storage amount per project is 5GB (meaning 5120MB), which you can distribute between your application and each of its services. See [`.magento.app.yaml`]({{page.baseurl}}cloud/project/project-conf-files_magento-app.html).

## Using the services
For services to be available to an application in your project, you must specify [*relationships*]({{page.baseurl}}cloud/project/project-conf-files_magento-app.html#cloud-yaml-platform-rel) between applications and services in `.magento.app.yaml`.

#### Related topics
*	[Get started with a project]({{page.baseurl}}cloud/project/project-start.html)
*	[`.magento.app.yaml`]({{page.baseurl}}cloud/project/project-conf-files_magento-app.html)
*	[Set up MySQL service]({{page.baseurl}}cloud/project/project-conf-files_services-mysql.html)
*	[Set up Redis service]({{page.baseurl}}cloud/project/project-conf-files_services-redis.html)
*	[Set up Solr service](http://devdocs.magento.com/guides/v2.0/cloud/project/project-conf-files_services-solr.html)
*	[Set up Elasticsearch service]({{page.baseurl}}cloud/project/project-conf-files_services-elastic.html)
*	[Set up RabbitMQ service]({{page.baseurl}}cloud/project/project-conf-files_services-rabbit.html)
*	[`routes.yaml`]({{page.baseurl}}cloud/project/project-conf-files_routes.html)