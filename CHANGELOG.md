
# Changelog

## [1.0.4] - 2026-09-01

### Fixed
- The completed-workout sync (`getCompletedWorkouts`) no longer crashes the
  host app. All writes to shared collections - the workout list, the
  per-workout detail dictionary, the metrics dictionary and the GPS route
  points - now go through serial queues instead of being mutated from
  concurrent HealthKit callbacks (a data race that corrupted memory and
  killed the process).
- Values crossing the platform channel are now converted to codec-safe types
  first (`channelSafeValue`): dates become ISO8601 strings and unknown types
  become their string description instead of raising a fatal
  `NSInternalInconsistencyException` ("Unsupported value for standard codec").
  Applied to workout-event metadata and session-id metadata values.

## [1.0.3] - 2025-09-08

### Changed
- Readme.md Improved

## [1.0.2] - 2025-09-08

### Changed
- Updated repository URLs to point to correct GitHub account (xhayankhan)
- Updated author information and contact details in README and podspec
- Added professional author section with GitHub profile image and social links
- Fixed topics in pubspec.yaml to comply with pub.dev requirements (reduced to 5 topics)
- Updated LinkedIn profile link to correct URL

## [1.0.1] - 2025-09-08

### Changed
- Updated repository URLs to point to correct GitHub account (xhayankhan)
- Updated author information in podspec
- Fixed topics to comply with pub.dev requirements

## [1.0.0] - 2025-09-08

### Added
- Initial release of flutter_workout_bridge
- WorkoutKit integration for custom workout creation
- HealthKit integration for comprehensive data retrieval
- Apple Watch workout scheduling
- GPS route and heart rate data access
- Pre-built workout templates
- Workout data analysis utilities
- Native iOS SwiftUI preview components

### Features
- Custom structured workouts with intervals
- Real-time workout scheduling to Apple Watch
- Detailed workout history with metrics
- GPS tracking and elevation data
- Heart rate monitoring and analysis
- Permission management system