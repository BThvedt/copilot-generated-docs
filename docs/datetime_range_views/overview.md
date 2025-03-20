# Overview of the `datetime_range_views` Module

The `datetime_range_views` module is a custom Drupal module that extends the functionality of the `datetime_range` field type by integrating it with the Views module. It provides enhanced support for filtering, sorting, and using arguments based on `datetime_range` fields in Views, making it easier to build dynamic and flexible displays of date-based content.

This module adds custom Views handlers for `datetime_range` fields, allowing users to filter by start and end dates, sort by these values, and create arguments for specific date components such as year, month, day, week, and more. By doing so, it ensures that `datetime_range` fields can be fully utilized in Views, enabling developers and site builders to create more powerful and intuitive date-based queries and displays.

```
name: 'Datetime Range Views'
type: module
description: 'Add support for relative filter and sorting to datetime range fields.'
core_version_requirement: ^8.8 || ^9
package: 'Views'
```