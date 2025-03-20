## Overview of the MHEC Search Module

The `mhec_search` module is a custom Drupal module designed to enhance search functionality within the MHEC (Midwestern Higher Education Compact) platform. This module provides tailored search capabilities, enabling users to efficiently locate relevant content, resources, or data within the system. It integrates seamlessly with the Drupal framework, leveraging its APIs and extending core search features to meet specific organizational needs.

Key features of the `mhec_search` module may include advanced filtering options, keyword-based search, and support for custom content types. It is built with scalability and performance in mind, ensuring that search results are delivered quickly and accurately, even as the volume of content grows. This module is a critical component for improving user experience and accessibility across the platform.

```
name: 'MHEC Search'
type: module
description: 'Search functionality and alterations.'
core_version_requirement: ^8.8 || ^9
package: 'MHEC'
```

### Libraries 

```
search:
  version: VERSION
  js:
    js/mhec.search.js: {}
  dependencies:
    - core/jquery
    - core/jquery.once
    - core/drupal
```

### Links

```
site.search:
  title: 'Search'
  weight: 0
  route_name: view.search_list.page_1
  menu_name: top
  options:
    attributes:
      data-icon: fa-search
      data-icon-position: after
      class:
        - 'search-list'
```