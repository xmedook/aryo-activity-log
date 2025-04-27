# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.1] - 2025-04-27

### Added
- GitHub SSH key authentication for secure repository access
- Performance optimizations in wp-config.php:
  - Increased memory limits (256MB for WP, 512MB for admin)
  - Disabled post revisions to reduce database size
  - Extended autosave interval to 5 minutes
  - Enabled page caching
  - Disabled file editing in admin
- Server-level optimizations in .htaccess:
  - GZIP compression for faster page loads
  - Browser caching rules for static assets
  - Keep-Alive connections
  - Expires headers for improved caching
- Added readme-ai.md documentation

### Fixed
- Corrected plugin directory structure by moving files from nested wp-content to the plugin root
- Fixed repository configuration to use SSH instead of HTTPS

### Changed
- Updated Git repository to use dev branch for development work
- Improved local WordPress performance through configuration optimizations

### Removed
- Eliminated redundant nested directory structure
- Removed unnecessary AI_DOCUMENTATION.md and README.md files

