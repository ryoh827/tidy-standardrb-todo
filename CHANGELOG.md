# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Added `unsafe` parameter to support `standardrb --fix-unsafely`
  - Default is `false`, which performs only safe fixes as before
  - When set to `true`, it includes unsafe fixes in the execution

### Changed
- Improved test cases to verify both safe and unsafe mode behaviors
  - In safe mode, only `safe_only.rb` is fixed while other files remain unchanged
  - In unsafe mode, all files are fixed

## v1.0.0

### Added
- Initial release of standardrb-fix action
- Support for fixing standardrb violations with `fix_count` parameter
- Automatic generation of `.standard_todo.yml` for remaining violations
