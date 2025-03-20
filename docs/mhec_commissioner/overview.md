## MHEC Commissioner Module Overview

The `mhec_commissioner` module is a custom Drupal module designed to manage and display information related to commissioners within the MHEC (Maryland Higher Education Commission) system. This module provides functionality to store, organize, and present commissioner data in a structured and user-friendly manner. It integrates seamlessly with the Drupal CMS, leveraging custom content types, views, and templates to ensure flexibility and scalability.

Key features of the module include the ability to create and manage commissioner profiles, display commissioner details on public-facing pages, and support administrative workflows for updating commissioner information. The module is built with extensibility in mind, allowing for future enhancements such as advanced filtering, search capabilities, or integration with external data sources. It is tailored to meet the specific needs of the MHEC organization while adhering to Drupal best practices.

```
name: 'MHEC Commissioner'
type: module
description: 'MHEC Commissioner alterations and enhancements.'
core_version_requirement: ^8.8 || ^9
package: 'MHEC'
```

### Menu 

```
mhec_commissioner.login:
  title: 'Commissioner Login'
  weight: 0
  route_name: user.login
  menu_name: top

mhec_commissioner.landing:
  title: 'Commissioner Portal'
  weight: 0
  menu_name: top
  url: internal:/node/1340
```

### Services

```
services:
  mhec_commissioner.redirect:
    class: Drupal\mhec_commissioner\EventSubscriber\RedirectSubscriber
    tags:
      - { name: event_subscriber }
```