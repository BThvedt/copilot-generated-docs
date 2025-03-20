# Site Settings Module Overview

The `site_settings` module is a custom Drupal module designed to provide site-specific configuration and functionality through reusable blocks. It simplifies the management of common elements such as footer information, social media links, address details, and notifications, making it easier for administrators to customize and maintain their website.

This module includes a variety of pre-built blocks, such as the "AAI Footer," "Social Links," "Address Info," and "Global Notification" blocks. These blocks are highly configurable and can be placed in different regions of the site to display dynamic content. The `site_settings` module is ideal for websites that require tailored content management solutions while maintaining flexibility and ease of use.

```
name: Site Settings
type: module
description: Settings specific to this site.
core_version_requirement: ^8.8 || ^9
package: Custom
```

### Libraries 
```
dashboard_notice:
  version: VERSION
  js:
    js/dashboard-notice.js: {}
  dependencies:
    - core/jquery
    - core/jquery.once
global_notification:
  version: VERSION
  js:
    js/global-notification.js: {}
  dependencies:
    - core/jquery
    - core/jquery.once
```

### Menus 
```
site_settings.site_settings:
  title: 'Site Settings'
  route_name: site_settings.site_settings
  description: 'Manage site settings.'
  parent: system.admin_config_system
  weight: 99
```

### Tasks 
```
site_settings.site_settings_tab:
  route_name: site_settings.site_settings
  title: Site Settings
  base_route: site_settings.site_settings
```

### Permissions 
```
administer site settings:
  title: 'Administer Site Settings'
```

### Routings
```
site_settings.site_settings:
  path: '/admin/config/settings'
  defaults:
    _form: '\Drupal\site_settings\Form\SiteSettings'
    _title: 'Site Settings'
  requirements:
    _permission: 'administer site settings'
  options:
    _admin_route: TRUE
```

### Services 
```
services:
  site_settings.settings:
    class: Drupal\site_settings\SiteSettings
    arguments: ['@config.factory']
```