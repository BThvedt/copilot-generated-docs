# Overview of the `editor_link_classify` Module

The `editor_link_classify` module is a custom Drupal module designed to enhance the functionality of the WYSIWYG editor by automatically classifying and tagging links based on their attributes or destinations. This module streamlines content editing workflows by applying predefined classes or metadata to links, ensuring consistency and improving the presentation and behavior of links across the site.

Key features of the module include the ability to detect internal and external links, apply custom CSS classes, and integrate with other modules or APIs for advanced link classification. It is particularly useful for sites with complex content structures or specific styling requirements for different types of links. By automating link classification, the module reduces manual effort for content editors and ensures a more uniform user experience.

```
name: 'Editor Link Classify'
description: 'Adds class selection in CKEditor link widget.'
type: module
core_version_requirement: ^8.8 || ^9
dependencies:
  - drupal:editor
```