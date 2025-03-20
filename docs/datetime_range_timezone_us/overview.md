# Summary of the `datetime_range_timezone_us` Module

The `datetime_range_timezone_us` module is a custom Drupal module designed to extend the functionality of date range fields by incorporating timezone-specific formatting tailored for US-based use cases. It provides a custom field formatter plugin, `DateRangeTimezoneUs`, which builds upon the existing `DateRangeTimezone` formatter. This formatter allows for flexible and user-friendly display of date ranges, including handling cases where the start and end dates fall on the same day, with customizable formatting options.

```
name: 'Datetime Range Timezone US'
type: module
description: 'Provides utilities for storing and displaying date ranges with US timezones.'
core_version_requirement: ^8.8 || ^9
package: 'Date'
dependencies:
  - datetime_range_timezone
```