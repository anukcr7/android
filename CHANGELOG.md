# Changelog

## Version 2.2.1

### New features

* Russian translation!
* TLSv1.3 support
* Location messages now include the batteryStatus in line with iOS (#841)
* Added explicit remote configuration preference toggle
* Reverted the `tst` field of location/waypoint/transition messages to mean the time that the event occurred. Added a new `created_at` field to these types with the timestamp of the message creation.

### Bug fixes

* Prevent crash when a user inputs an invalid MQTT URL (#852)
* Fix an issue related to remoteCommands not being received or handled correctly (#842)
* Config import no longer crashes when waypoints are absent (#818)
* Map now correctly updates the blue dot when in foreground
* Configuration management screen now shows waypoints that will be exported
* Monitoring mode button should now be correct when Map activity is resumed

## Version 2.2.0

### New features

* Created a changelog!
* Logs now viewable and shareable from within the application (Status -> View Logs)
* Debug logs are now toggleable from the logs viewer UI
* Migrated preferences to androidx library
* MQTT errors are now displayed more clearly on the connection status.
* Locator intervals are now user-configurable, and differentiated between significant changes and move modes.
* Clearing a contact sends a zero-length payload rather than a JSON message for type `MessageClear`, in line with the iOS app and booklet
* Users can specify the MQTT client ID explicitly
* Removed confusion around MQTT auth (no username vs anonymous). Now, not supplying a username = anonymous auth
* Added French translations

### Bug fixes

* MQTT processor should be more stable at re-connecting when disconnected
* Improved reliability of internal message queue / backoff mechanism when unable to send a message
* Fixed some issues on the welcome screens on older (API<=24) devices
* Fixed race conditions in usage of the MQTT client
* Fixed input weirdness when trying to edit latlngs in the region UI
* Fixed some bugs in the configuration import / export handling
* Fixed a bug where MQTT tried to connect without a valid configuration
* Fixed a bug preventing users from putting the mode into low power mode
* Stale incoming locations are only discarded if the preference is set
* All messages have the current time populated into the `tst` field, as opposed to the time of the last location fix
* Better reliability in reading from mis-typed preferences.
* Few general lint / stability fixes

## Version 2.1.3

### New features

* `dontReuseHttpClient` config key to create a new HTTP client on every request. Can fix stuck queue on certain devives (see #656)
* Removed locator interval and displacement UI settings because they were misunderstood causing too much confusion for many users
* made locator accuracy configurable in signifficant mode with locatorPriority configuration key
* Improve display of error conditions
* Remote reportLocation command triggers new location fix (thanks to @grheard)
* Added debug log toggle in preferences
* Removed region place picker because API was retiered by Google

### Bug fixes

* wrong long press label of report button
* crash on invalid http headers
* http connection not closed correctly on errors
* location request not setup again on locator parameter change
* include debugLog configuration key in export and editor
* some translations
* Downgraded MQTT library to fix several issues
* Back buttons and arrows in preferences
* Monitoring mode not saved/restored correctly
* Removed test location listener that could crash the background service

## Version 2.1.2

### New features

* Debug logger that can export application logs to a HTML file. See our booklet for more details.

### Bug fixes

* Crash in VersionFragment when no suitable browser is installed
* Wrong wtst unit in waypoint messages (#631)
* Crash when setting illegal username in HTTP mode
* Crash when setting invalid geofence parameter

## Version 2.1.1

### Bug fixes

* waypoint transitions were sent in quiet mode
* reportLocation command was ignored in MQTT mode (#627)
* wrong data types for alt, vel attributes in location message (#629)
* crashes in WelcomeActivity
* crash during EncryptionProvider initialization
* crash when receiving waypoint message without radius
* Setup screen got stuck on restrictions page
* Improved error reporting (#567)

## Version 2.1.0

### New features

* Foreground/Background mode replaced by monitoring modes (quiet => No automatic location reports/passive location gathering, manual => Only automatic region location reports/passive location gathering, significant => automatic location reports/active location gathering based on Wifi/Cell location, move => frequent location reports/active location gathering based on GPS). Significant changes mode corresponds to the old behavior.
* Locator displacement and interval only influence significant location monitoring mode
* Monitoring modes displayed in notification when endpoint state is idle or connected
* Prefilling new region with current location
* Added estimated distance to contacts in details view
* Moved background jobs to Android Work Manager. Reconnect/Ping jobs now have a minimum interval of 15 minutes.
* Spanish translation. Thanks to @Kaysera.
* Improved dependency handling and fixed several bugs

### Bug fixes

* Waypoint import not working probperly
* Config import not displayed correctly
* Crash on first launch
* Locations not correctly requested
* Removed copy mode
* Removed GUI to configure unauthenticated connections. auth preferences key can still be set via configuration editor if unauthenticated connections are really required

## Version 2.0.0

### New features

* Removed support for bluetooth beacons because that feature accounted for over 90% of all crashes
* Removed support for shared waypoints. Waypoints are now always treated as shared
* Removed support for our hosted public MQTT platform
* Added ping functionality that will trigger a location report periodically
* Added support for Opencage Geocoder as alternative to Google
* Added custom useragent to HTTP mode to better identify the app in logs
* Added altitude to extended data publishes
* New algorithm for region detection that is assisted by location publishes
* Added support for inregions element of location publishes

### Bug fixes

* Fixed encryption issues with HTTP mode
* Rewrote backend service from the ground up to work more reliable on modern Android versions that prevent many actions when the app is in the background.
