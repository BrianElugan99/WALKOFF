# Changelog
<!-- Use the tags Added, Changed, Deprecated, Removed, Fixed, Security, and
     Contributor to describe changes -->
## [Unreleased]

## [0.5.2]
###### 2017-12-20

### Fixed
* Fixed a bug where the config host and port were not initialized before
  the server started.

## [0.5.1]
###### 2017-12-14

### Fixed
* A bug fix for case management due to a typo in the TS.

## [0.5.0]
###### 2017-11-29

### Added
* New user-friendly playbook editor
* Host and port can now be specified on the command line
* App-specific conditions and transforms
  * Conditions and transforms are now located in apps rather than in core, so
    they can be more easily created
* Branches now contain a "priority" field which can be used to determine the
  order in which the branches of a given action are evaluated
* Arguments to actions, conditions, and transforms which use references can
  select which component of the referenced action's output to use.
* Migration scripts to help ease a variety of backward-breaking changes --
  `migrate_workflows.py` and `migrate_api.py`
* Scripts to create Sphinx documentation have been added to the repository


### Changed
* Custom interfaces with event handling
  * Interfaces are no longer attached to apps; they are now their own plugins
    and are contained in the `interfaces` directory
  * Interfaces can use new decorator functions to listen and respond to all
    events in Walkoff as they occur
* Better triggers
  * Triggers are no longer specified in the database. Instead, each individual
    action in a workflow can have its own set of conditions which can act as
    breakpoints in a workflow. You can send data to them through the server and
    have that data validated against a set of conditions before the action can
    resume.
  * You can still start a workflow from the beginning through the server
* Renamed workflow components for clarity
  * "steps" have been renamed "actions"
  * "next steps" have been renamed "branches"
  * "flags" have been renamed "conditions"
  * "filters" have been renamed "transforms"
* Script used to start the server has been renamed `walkoff.py`
* ZeroMQ keys are contained in the `.certificates` directory
* Playbook file format changes
  * Branches are now contained outside of actions, creating two top-level
    fields.
  * Branches have a `source_uid` and a `destination_uid` instead of just a
    `name` field
  * The `start` step on a workflow is indicated with the start step's UID
    instead of its name
  * The `app` and `action` fields of actions, conditions, and transforms have
    been renamed `app_name` and `action_name` respectively.
  * Conditions and transforms contain an `app_name` field instead of just an
    `action` field
  * We have removed the `widgets` field and the `risk` field from actions
  * Devices for actions are specified by id rather than by name
  * Actions' `inputs` field, as well as conditions' and transforms' `args`
    field has been renamed `arguments` and is now a complete JSON object
  * Playbooks now contain a `walkoff_version` field which will be used to
    indicate which version of WALKOFF created them. This will be helpful in the
    future to migrate workflows to new formats
* Minor changes to api.yaml schema
  * `dataIn` has been renamed `data_in`
  * `termsOfService` has been renamed `terms_of_service`
  * `externalDocs` has been renamed `external_docs` and is always an array
* Performance of worker processes has been improved by removing gevent from
  child processes and reducing polling
* The blinker Signals used to trigger events have been wrapped in a
  WalkoffEvent enum
* Internal sockets used for ZeroMQ communication have been moved to
  `core.config.config`
* Actions which are defined inside of a class must supply a device, or the
  workflow will fail on initialization
* The REST API to get the APIs of apps has been enhanced significantly and
  returns all of the API


### Removed
* Unfortunately, event-driven actions have been broken for some time now. We
  have removed this functionality, but are working on an even better
  replacement for them in the meantime
* We have removed accumulated risk from workflows and risk from steps. This
  feature will be re-added at a future date
* We have removed widgets from the backend. This feature will be reimplemented
  later.
* Backend support for adding roles to users has been removed. All users are
  administrators as they have been in previous releases. There was never a UI
  component for this feature, and it was breaking some other components for
  editing users. Roles will be re-added in the next release.

### Security
* HTTPS is enabled by default if certificates are placed in the
  `.certificates` directory.

### Contributor
* Coverage.py is used to generate test coverage report. Travis-CI will fail if
  the code coverage is below 81% This percentage will rise over time


## [0.4.2]
###### 2017-11-09

### Fixed
* Bug fixes to Playbook editor
* Bug in global action execution

## [0.4.1]
###### 2017-11-03

### Fixed
* Bug fixes to playbook editor

## [0.4.0]
###### 2017-10-30

### Changes
* Custom devices
    - Apps define their own fields needed in their devices
* Global app actions
    - Actions no longer need to be defined in a class
* Security enhancements
* Performance improvements and bug fixes

## [0.3.1]
###### 2017-09-25

### Fixed
* Bug Fixes

## [0.3.0]
###### 2017-09-15

### Added
* Brand new UI 
* Better concurrent execution of CPU-bound workflows
* Multiple workflows can be executed on the same scheduler
* New Scheduler UI page
* New Case Management UI

### Changed
* Improved REST API
* Workflows are now stored as JSON

### Fixed
* Bugs and performance improvements

### Security
* Enhanced security using JSON Web Tokens
* Workflows are stored as JSON

## [0.2.1]
###### 2017-07-14

### Added
* Event-driven app actions
* Multiple return codes for actions and error handling

### Changed
* Apps are now located in Walkoff-Apps repo
* Workflow results are stored in case database

### Fixed
* Bug fixes and performance improvements

## [0.2.0]
###### 2017-06-21

### Added
* New app specification using YAML metadata files
    * Better input validation using JSON schema
    * Arguments can be string, integer, number, arrays, or JSON objects
* Workflow animation during execution in the workflow editor
* Results from previously executed actions can be used later in workflows
* Better worfkflow monitoring during execution
* New apps
    * NMap
    * Splunk
    * TP-Link 100 Smart Outlet

### Fixed
* UI styling and bug fixes
* Bug fixes and performance improvements

## [0.1.2]
###### 2017-05-25

### Added
* New Lyfx playbook

### Fixed
* Bug fixes to UI and apps


## [0.1.1]
###### 2017-05-25

### Added

* OpenAPI Specification for server endpoints and connexion Flask app
* New Apps
    * AR.Drone
    * Ethereum Blockchain
    * Facebook User Post
    * Webcam
    * Watson Visual Recognition
    * Tesla
    * Lifx
* Better error handling in server endpoints
* Bug fixes
* Swagger UI documentation

### Changed
* UI improvements


## [0.1.0]
###### 2017-05-15

Initial Release
