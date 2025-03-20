## Overview of the MHEC States Module

The `mhec_states` module is a custom Drupal module developed to manage and display state-specific data and resources within the MHEC (Midwestern Higher Education Compact) platform. This module is designed to provide users with easy access to information and tools tailored to individual states, enhancing the platform's usability and relevance for diverse audiences.

Key features of the `mhec_states` module may include the ability to organize content by state, display state-specific statistics or reports, and integrate with other modules to deliver localized functionality. By streamlining access to state-related data, this module plays a vital role in supporting the MHEC's mission of improving higher education through collaboration and resource sharing across its member states.

```
name: 'MHEC States'
type: module
description: 'Provide a state navigation form.'
core_version_requirement: ^8.8 || ^9
package: 'MHEC'
```

### Libraries
```
select:
  version: VERSION
  js:
    js/mhec-states.select.js: {}
  dependencies:
    - core/jquery
    - core/jquery.once
    - core/drupal
```