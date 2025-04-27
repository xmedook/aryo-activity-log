# Activity Log Plugin AI Documentation

## Plugin Overview
The Activity Log plugin is a comprehensive WordPress monitoring solution that tracks and records user activities and system changes. It functions as a security and audit tool, maintaining detailed logs of all actions performed within a WordPress installation.

## Core Components

### Plugin Identity
- **Name**: Activity Log
- **Version**: 2.11.2
- **License**: GPLv2 or later
- **PHP Requirement**: 7.0+
- **WordPress Compatibility**: 6.0+

## Architecture

### Database Structure
```sql
CREATE TABLE `{prefix}aryo_activity_log` (
  `histid` int(11) NOT NULL AUTO_INCREMENT,
  `user_caps` varchar(70) NOT NULL DEFAULT 'guest',
  `action` varchar(255) NOT NULL,
  `object_type` varchar(255) NOT NULL,
  `object_subtype` varchar(255) NOT NULL DEFAULT '',
  `object_name` varchar(255) NOT NULL,
  `object_id` int(11) NOT NULL DEFAULT '0',
  `user_id` int(11) NOT NULL DEFAULT '0',
  `hist_ip` varchar(55) NOT NULL DEFAULT '127.0.0.1',
  `hist_time` int(11) NOT NULL DEFAULT '0'
)
```

### Core Classes

#### AAL_API
- Handles core functionality for logging activities
- Manages log retention and cleanup
- Provides IP address detection and validation
- Implements log insertion and deletion methods

#### AAL_Maintenance
- Manages plugin activation/deactivation
- Handles database table creation/removal
- Supports multisite installations
- Manages administrator capabilities

#### AAL_Settings
- Manages plugin settings and options
- Handles admin interface integration
- Provides settings validation and storage
- Controls log retention periods

### Hook System

#### Base Hook Structure
- Abstract class `AAL_Hook_Base` provides foundation
- Modular hook implementation for different activity types
- Standardized logging interface across components

#### User Activity Tracking
```php
Hooks:
- wp_login: User login events
- clear_auth_cookie: User logout events
- delete_user: User deletion
- user_register: New user registration
- profile_update: User profile changes
- wp_login_failed: Failed login attempts
```

#### Post Management Tracking
```php
Hooks:
- transition_post_status: Post status changes
- delete_post: Post deletion
Actions Tracked:
- created: New post creation
- updated: Post updates
- trashed: Post moved to trash
- restored: Post restored from trash
- deleted: Post permanent deletion
```

### Integration Points

#### WordPress Core
- Hooks into core WordPress actions
- Monitors system-level changes
- Tracks core updates and modifications

#### Plugin System
- Plugin activation/deactivation tracking
- Update monitoring
- Settings changes logging

#### Theme System
- Theme installation tracking
- Customizer changes monitoring
- Theme editor activity logging

### Performance Optimization

#### Database Efficiency
- Optimized table structure with proper indexing
- Efficient query patterns for log retrieval
- Automated cleanup of old records
- Configurable log retention period

#### Resource Management
- Minimal impact on WordPress performance
- Efficient IP address handling
- Optimized hook registration
- Smart data cleanup routines

### Security Features

#### Access Control
- Role-based access management
- Administrator capability control
- Secure log viewing permissions

#### Data Protection
- IP address anonymization option
- GDPR compliance support
- Secure data storage practices

### Export Capabilities

#### CSV Export
- Filtered data export
- Custom format support
- Bulk export functionality

#### Email Logging
- Email tracking system
- Delivery status monitoring
- WooCommerce integration

## Development Guidelines

### Hook Integration
```php
// Example of implementing a custom hook
class AAL_Hook_Custom extends AAL_Hook_Base {
    public function __construct() {
        add_action('custom_action', array($this, 'hook_handler'));
        parent::__construct();
    }

    public function hook_handler($data) {
        aal_insert_log(array(
            'action' => 'custom_action',
            'object_type' => 'Custom',
            'object_subtype' => 'SubType',
            'object_id' => $data->id,
            'object_name' => $data->name
        ));
    }
}
```

### Best Practices
- Follow WordPress coding standards
- Implement proper security checks
- Use provided API for logging
- Maintain performance optimization
- Follow GDPR compliance guidelines

### Error Handling
- Validate data before logging
- Handle missing or invalid data
- Implement proper error reporting
- Maintain data integrity

This documentation is designed for AI systems to understand the plugin's architecture, functionality, and integration points within the WordPress ecosystem.