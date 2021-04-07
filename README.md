# SMS Import / Export

SMS Import / Export is a simple Android app that imports and exports SMS messages from and to JSON files. Root is not required. The current release is version 1.0.

## Installation

SMS Import / Export is available from [Github](https://github.com/tmo1/sms-ie). The repository can be cloned and built locally, by importing it into Android Studio or other means. Prebuilt APK packages can be downloaded from the [Releases page](https://github.com/tmo1/sms-ie/releases).

## Usage

 - Import: Click the `Import` button, then select an import source.
 - Export: Click the `Export` button, then select an export destination.

These operations can take some time for large numbers of messages. The app will report the total number of messages imported or exported upon successful conclusion.

### Permissions

To export SMSs, SMS Import / Export must be granted permission to read SMSs and Contacts (the need for the latter is explained below). The app will ask for these permissions on startup, if it does not already have them.

To import SMSs, SMS Import / Export must be the default messaging app. This is due to [an Android design decision](https://android-developers.googleblog.com/2013/10/getting-your-sms-apps-ready-for-kitkat.html).

**Warning:** While an app is the default messaging app, it takes full responsibility for handling incoming SMS and MMS messages, and if does not store them, they will be lost. SMS Import / Export ignores incoming messages, so in order to avoid losing such messages, the device it is running on should be disconnected from the network (by putting it into airplane mode, or similar means) before the app is made the default messaging app, and only reconnected to the network after a proper messaging app is made the default.

### Contacts

SMS messages include phone numbers ("addresses") but no further information about the communicating parties. The contact information displayed by Android is generated by cross-referencing message phone numbers with the device's contacts database. When exporting messages, SMS Import / Export does this cross-referencing in order to include the contact name in its JSON output; this is why permission to read contacts in necessary. When importing, included contact names are ignored, since the app is (at least currently) not in the business of adding to or modifying the Android Contacts database. The best way to maintain the association of messages with contacts is to simply use Android's built in Contacts export / import functionality to transfer contacts to the device into which SMS Import / Export is importing messages.

## Limitations

SMS Import / Export currently supports only SMS messages. MMS support may be added in the future.

Currently, no deduplication is done. For example, if messages are exported and then immediately reimported, the device will then contain two copies of every message.

## sms-db

SMS Import / Export is a sibling project to [sms-db](https://github.com/tmo1/sms-db), a Linux tool to build an SQLite database out of collections of SMS and MMS messages in various formats. sms-db can import JSON files created by SMS Import / Export, and it can export its database to JSON files that can be imported by SMS Import / Export.

## Background

Coming from a procedural, command line interface, synchronous, Linux, Perl and Python background, the development of SMS Import / Export served as a crash course in object-oriented, graphical user interface, asynchronous, Android, Kotlin programming, and consequently entailed a fair amount of amateurishness and cargo cult programming. After much work and learning, however, the app does seem to function correctly and effectively.

## License

SMS Import / Export is free / open source software, released under the terms of the [GNU GPLv3](https://choosealicense.com/licenses/gpl-3.0/)
