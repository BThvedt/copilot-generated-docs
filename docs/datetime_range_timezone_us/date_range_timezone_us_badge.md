# Explanation of `DateRangeTimezoneUsBadge.php`

The `DateRangeTimezoneUsBadge.php` file defines a custom field formatter for Drupal, extending the functionality of the `DateRangeTimezoneUs` formatter. This formatter is designed to display date ranges in a "badge" style format, with additional customization options for displaying specific parts of the date (day, month, year, timezone) and a separator between start and end dates.

## Namespace and Imports

The file is part of the `datetime_range_timezone_us` module and resides in the `Plugin\Field\FieldFormatter` namespace. It imports necessary Drupal classes for handling field items, dates, and form states.

```php
namespace Drupal\datetime_range_timezone_us\Plugin\Field\FieldFormatter;

use Drupal\Core\Field\FieldItemListInterface;
use Drupal\Core\Datetime\DrupalDateTime;
use Drupal\Core\Form\FormStateInterface;
```

## Class Definition

### Annotation

The class is annotated with `@FieldFormatter` to define it as a field formatter plugin.

```php
/**
 * Plugin implementation of the 'Default' formatter for 'datetime' fields.
 *
 * @FieldFormatter(
 *   id = "daterange_timezone_us_badge",
 *   label = @Translation("Badge US"),
 *   field_types = {
 *     "daterange_timezone"
 *   }
 * )
 */
class DateRangeTimezoneUsBadge extends DateRangeTimezoneUs {
```

### Default Settings

The `defaultSettings` method defines the default configuration for the formatter, including options to display specific parts of the date (day, month, year, timezone) and a separator for start and end dates.

```php
public static function defaultSettings() {
  return [
    'display_day' => TRUE,
    'display_month' => TRUE,
    'display_year' => TRUE,
    'display_timezone' => TRUE,
    'separator' => ' - ',
  ];
}
```

### View Elements

The `viewElements` method generates the renderable array for the field items. It formats the start and end dates into individual parts (month, day, year) and combines them using the specified separator. The output is rendered using a custom Twig theme (`datetime_range_timezone_us_badge`).

```php
public function viewElements(FieldItemListInterface $items, $langcode) {
  $elements = [];

  foreach ($items as $delta => $item) {
    if (!empty($item->start_date)) {
      if (!empty($item->start_date) && !empty($item->end_date)) {
        $timezone = $this->getTimezone($item);
        $parts = $this->formatDateParts($item->start_date, $item->timezone);
        $end_parts = $this->formatDateParts($item->end_date, $item->timezone);
        foreach ($parts as $key => &$part) {
          if ($part !== $end_parts[$key]) {
            $part .= $this->getSetting('separator') . $end_parts[$key];
          }
        }

        $elements[$delta]['date'] = [
          '#theme' => 'datetime_range_timezone_us_badge',
          '#month' => $this->getSetting('display_month') ? $parts['month'] : NULL,
          '#day' => $this->getSetting('display_day') ? $parts['day'] : NULL,
          '#year' => $this->getSetting('display_year') ? $parts['year'] : NULL,
          '#timezone' => $timezone,
        ];
      }
    }
  }

  return $elements;
}
```

### Settings Form

The `settingsForm` method defines the settings form for the formatter, allowing users to configure which parts of the date to display and the separator string.

```php
public function settingsForm(array $form, FormStateInterface $form_state) {
  $form['separator'] = [
    '#type' => 'textfield',
    '#title' => $this->t('Date separator'),
    '#description' => $this->t('The string to separate the start and end dates'),
    '#default_value' => $this->getSetting('separator'),
  ];

  foreach (['day', 'month', 'year', 'timezone'] as $type) {
    $form['display_' . $type] = [
      '#type' => 'checkbox',
      '#title' => $this->t('Display %type', ['%type' => ucfirst($type)]),
      '#description' => $this->t('Should we display the %type after the formatted date?', ['%type' => $type]),
      '#default_value' => $this->getSetting('display_' . $type),
    ];
  }

  return $form;
}
```

### Settings Summary

The `settingsSummary` method provides a summary of the formatter's settings, showing whether each part of the date (day, month, year, timezone) is displayed and the configured separator.

```php
public function settingsSummary() {
  $summary = [];

  if ($separator = $this->getSetting('separator')) {
    $summary[] = $this->t('Separator: %separator', ['%separator' => $separator]);
  }

  foreach (['day', 'month', 'year', 'timezone'] as $type) {
    $summary[] = $this->t('@action the %type', [
      '@action' => $this->getSetting('display_' . $type) ? 'Showing' : 'Hiding',
      '%type' => $type,
    ]);
  }

  return $summary;
}
```

### Format Date Parts

The `formatDateParts` method formats a date into individual parts (month, day, year) using the specified timezone.

```php
protected function formatDateParts(DrupalDateTime $date, $timezone) {
  return [
    'month' => $this->dateFormatter->format($date->getTimestamp(), 'custom', 'M', $timezone),
    'day' => $this->dateFormatter->format($date->getTimestamp(), 'custom', 'j', $timezone),
    'year' => $this->dateFormatter->format($date->getTimestamp(), 'custom', 'Y', $timezone),
  ];
}
```

## Summary

The `DateRangeTimezoneUsBadge` class extends the `DateRangeTimezoneUs` formatter to provide a badge-style display for date ranges. It offers flexible configuration options for displaying specific parts of the date and customizing the separator between start and end dates. The output is rendered using a custom Twig theme, making it easy to style and integrate into Drupal themes.
