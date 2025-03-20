# MHEC Person Importer Module Overview

The `mhec_person_importer` module is a custom Drupal module designed to facilitate the automated import and synchronization of person-related data into a Drupal site. This module streamlines the process of integrating external data sources, such as CSV files or APIs, to populate and update user or entity records within the system. It ensures data consistency and reduces manual effort by providing a reliable mechanism for bulk data handling.

Key features of the module include configurable import settings, mapping of external data fields to Drupal entities, and robust error handling to manage invalid or incomplete data. The module is designed to be extensible, allowing developers to customize its behavior to meet specific project requirements. By leveraging this module, organizations can efficiently manage large datasets and maintain up-to-date records with minimal manual intervention.


```
name: MHEC Person Import
type: module
description: Import person handler.
core_version_requirement: ^8.8 || ^9
package: MHEC
```

### Permissions 

```
perform person import:
  title: 'Can perform person import'
```

### Routing 

```
mhec_person_import.form:
  path: '/admin/structure/person-import'
  defaults:
    _form: '\Drupal\mhec_person_import\Form\MhecPersonImportForm'
    _title: 'Import People'
  requirements:
    _permission: 'perform person import'
```

### Services

```
services:
  mhec_person_import.importer:
    class: Drupal\mhec_person_import\MhecPersonImporter
    arguments: ['@entity_type.manager']
```