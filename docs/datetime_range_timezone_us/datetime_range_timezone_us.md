# DateRangeTimezoneUs.php

This file defines a custom field formatter for the Drupal CMS, specifically for formatting date ranges with timezone information in a US-specific format. The class `DateRangeTimezoneUs` extends the `DateRangeTimezone` class and provides additional functionality and settings.

## Namespace and Imports

```php
namespace Drupal\datetime_range_timezone_us\Plugin\Field\FieldFormatter;

use Drupal\datetime_range_timezone\Plugin\Field\FieldFormatter\DateRangeTimezone;
use Drupal\Core\Field\FieldItemListInterface;
use Drupal\Core\Form\FormStateInterface;
use Drupal\Core\Datetime\DrupalDateTime;
use Drupal\datetime_range\Plugin\Field\FieldType\DateRangeItem;
```

## Class Definition

### Annotation

The class is annotated with `@FieldFormatter` to define it as a field formatter plugin.

```php
/**
 * Plugin implementation of the 'Default' formatter for 'daterange_timezone'.
 *
 * @FieldFormatter(
 *   id = "daterange_timezone_us",
 *   label = @Translation("Default US"),
 *   field_types = {
 *     "daterange_timezone"
 *   }
 * )
 */
class DateRangeTimezoneUs extends DateRangeTimezone {
```

### Default Settings

The `defaultSettings` method defines the default settings for the formatter, including a custom format type for dates that fall on the same day.

```php
public static function defaultSettings() {
  return [
    'format_type_same_day' => 'medium',
  ] + parent::defaultSettings();
}
```

### View Elements

The `viewElements` method generates the renderable array for the field items, formatting the start and end dates and handling cases where the start and end dates are on the same day.

```php
public function viewElements(FieldItemListInterface $items, $langcode) {
  $build = [];
  foreach ($items as $delta => $item) {
    $timezone = $this->getTimezone($item);
    $start = $item->start_date ? $this->formatDate($item->start_date, $this->getSetting('format_type'), $item->timezone) : '';
    $end = $item->end_date ? $this->formatDate($item->end_date, $this->getSetting('format_type'), $item->timezone) : '';

    if (!empty($item->start_date) && !empty($item->end_date)) {
      $start_date = $item->start_date->getTimestamp();
      $end_date = $item->end_date->getTimestamp();
      if ($start_date !== $end_date) {
        if (date('d.m.Y', $start_date) === date('d.m.Y', $end_date)) {
          $end = $item->end_date ? $this->formatDate($item->end_date, $this->getSetting('format_type_same_day'), $item->timezone) : '';
        }
      }
    }

    $build[$delta] = [
      '#theme' => 'datetime_range_timezone',
      '#start_date' => $start,
      '#end_date' => $end,
      '#separator' => $this->getSetting('separator'),
      '#timezone' => $timezone,
    ];
  }
  return $build;
}
```

### Get Timezone

The `getTimezone` method returns the timezone abbreviation for the given date range item.

```php
protected function getTimezone(DateRangeItem $item) {
  $timezone = NULL;
  if ($this->getSetting('display_timezone') && $item->timezone) {
    $dt = new \DateTime($item->value, new \DateTimeZone($item->timezone));
    $timezone = $dt->format('T');
  }
  return $timezone;
}
```

### Settings Form

The `settingsForm` method defines the settings form for the formatter, allowing users to configure the date format for end dates that fall on the same day as the start date.

```php
public function settingsForm(array $form, FormStateInterface $form_state) {
  $form = parent::settingsForm($form, $form_state);
  $form['format_type_same_day'] = [
    '#title' => $this->t('Date format for end date'),
    '#description' => $this->t('If the start and end date are on the same day, this format will be used for the end date.'),
  ] + $form['format_type'];
  $form['display_timezone']['#weight'] = 10;
  return $form;
}
```

### Settings Summary

The `settingsSummary` method provides a summary of the formatter settings.

```php
public function settingsSummary() {
  $summary = [];

  $date = new DrupalDateTime();
  $summary[] = $this->t('Format: @display', ['@display' => $this->formatDate($date, $this->getSetting('format_type'))]);
  $summary[] = $this->t('Format for end date: @display', ['@display' => $this->formatDate($date, $this->getSetting('format_type_same_day'))]);

  if ($separator = $this->getSetting('separator')) {
    $summary[] = $this->t('Separator: %separator', ['%separator' => $separator]);
  }

  $summary[] = $this->t('@action the timezone', [
    '@action' => $this->getSetting('display_timezone') ? 'Showing' : 'Hiding',
  ]);

  return $summary;
}
```

### Format Date

The `formatDate` method formats a date object according to the specified format type and timezone.

```php
protected function formatDate(DrupalDateTime $date, $format_type = 'medium', $timezone = NULL) {
  return $this->dateFormatter->format($date->getTimestamp(), $format_type, '', $timezone);
}
```

This class provides a custom formatter for date ranges with timezone information, tailored for US-specific formatting needs.
