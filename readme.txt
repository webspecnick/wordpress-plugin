Mailgun for WordPress
=====================

Contributors: Mailgun, sivel, lookahead.io, m35dev
Tags: mailgun, smtp, http, api, mail, email
Requires at least: 3.3
Tested up to: 4.8
Stable tag: 1.5.8.4
License: GPLv2 or later


Easily send email from your WordPress site through Mailgun using the HTTP API or SMTP.


== Description ==

[Mailgun](http://www.mailgun.com/) is the email automation engine trusted by over 10,000 website and application developers for sending, receiving and tracking emails. By taking advantage of Mailgun's powerful email APIs, developers can spend more time building awesome websites and less time fighting with email servers. Mailgun supports all of the most popular languages including PHP, Ruby, Python, C# and Java.

One particularly useful feature of this plugin is that it provides you with a way to send email when the server you are on does not support SMTP or where outbound SMTP is restricted since the plug-in uses the Mailgun HTTP API for sending email by default. All you need to use the plugin is a [Mailgun account](http://www.mailgun.com/). Mailgun has a free account that lets you send up to 200 emails per day, which is great for testing. Paid subscriptions are available for increased limits.

The latest version of this plugin adds support for Mailgun list subscription. Using the shortcode, you can place a form on an article or page to allow the visitor to subscribe to one or more lists. Using the widget, you can provide subscription functionality in sidebars or anywhere widgets are supported e.g. footers.

The current version of this plugin only handles sending emails, tracking and tagging and list subscription. 


== Installation ==

1. Upload the `mailgun` folder to the `/wp-content/plugins/` directory or install directly through the plugin installer
2. Activate the plugin through the 'Plugins' menu in WordPress or by using the link provided by the plugin installer
3. Visit the settings page in the Admin at `Settings -> Mailgun` and configure the plugin with your account details
4. Click the Test Configuration button to verify that your settings are correct.
5. Click View Available Lists to review shortcode settings for lists in your Mailgun account that you may wish to help users subscribe to


== Frequently Asked Questions ==

- Testing the configuration fails when using the HTTP API

Your web server may not allow outbound HTTP connections. Set `Use HTTP API` to "No", and fill out the configuration options to SMTP and test again.

- Testing the configuration fails when using SMTP

Your web server may not allow outbound SMTP connections on port 465 for secure connections or 587 for unsecured connections. Try changing `Use Secure SMTP` to "No" or "Yes" depending on your current configuration and testing again. If both fail, try setting `Use HTTP API` to "Yes" and testing again.

If you *have* to use SMTP and something is still going horribly wrong, enable debug mode in WordPress and also add the `MG_DEBUG_SMTP` constant to your `wp-config.php`, like so:

`
define( 'MG_DEBUG_SMTP', true );
`

- Can this be configured globally for WordPress Multisite?

Yes, using the following constants that can be placed in wp-config.php:

`
MAILGUN_USEAPI       Type: boolean
MAILGUN_APIKEY       Type: string
MAILGUN_DOMAIN       Type: string
MAILGUN_USERNAME     Type: string
MAILGUN_PASSWORD     Type: string
MAILGUN_SECURE       Type: boolean
MAILGUN_FROM_NAME    Type: string
MAILGUN_FROM_ADDRESS Type: string
`

- What hooks are available for use with other plugins?

`mg_use_recipient_vars_syntax`
  Mutates messages to use recipient variables syntax - see
  https://documentation.mailgun.com/user_manual.html#batch-sending for more info.

  Should accept a list of `To` addressses.

  Should *only* return `true` or `false`.

`mg_mutate_message_body`
  Allows an external plugin to mutate the message body before sending.

  Should accept an array, `$body`.

  Should return a new array to replace `$body`.

`mg_mutate_attachments`
  Allows an external plugin to mutate the attachments on the message before
  sending.

  Should accept an array, `$attachments`.

  Should return a new array to replace `$attachments`.

- What hooks are available for use with other plugins?

`mg_use_recipient_vars_syntax`
  Mutates messages to use recipient variables syntax - see
  https://documentation.mailgun.com/user_manual.html#batch-sending for more info.

  Should accept a list of `To` addressses.

  Should *only* return `true` or `false`.

`mg_mutate_message_body`
  Allows an external plugin to mutate the message body before sending.

  Should accept an array, `$body`.

  Should return a new array to replace `$body`.

`mg_mutate_attachments`
  Allows an external plugin to mutate the attachments on the message before
  sending.

  Should accept an array, `$attachments`.

  Should return a new array to replace `$attachments`.


== Screenshots ==

1. Configuration options for using the Mailgun HTTP API
2. Configuration options for using the Mailgun SMTP servers
3. Administration option to View Available Lists for subscription
4. Setting up a Subscription Widget
5. Using a Subscription Code
6. Subscription Form Seen By Site Visitors


== Changelog ==

= 1.5.8.4 (2017-06-28): =
- Packaging fix which takes care of an odd filtering issue (https://wordpress.org/support/topic/1-5-8-3-broke-the-mg_mutate_message_body-filter)

= 1.5.8.3 (2017-06-13): =
- Fix a bug causing only the last header value to be used when multiple headers of the same type are specified (https://wordpress.org/support/topic/bug-with-mg_parse_headers/)
- Added `pt_BR` translations (thanks @emersonbroga)

= 1.5.8.2 (2017-02-27): =
- Fix a bug causing empty tags to be sent with messages (#51)
- Add `mg_mutate_message_body` hook to allow other plugins to modify the message body before send
- Add `mg_mutate_attachments` hook to allow other plugins to modify the message attachments before send
- Fix a bug causing the AJAX test to fail incorrectly.

= 1.5.8.2 (2017-02-27): =
- Fix a bug causing empty tags to be sent with messages (#51)
- Add `mg_mutate_message_body` hook to allow other plugins to modify the message body before send
- Add `mg_mutate_attachments` hook to allow other plugins to modify the message attachments before send
- Fix a bug causing the AJAX test to fail incorrectly.

= 1.5.8.1 (2017-02-06): =
- Fix "Undefined property: MailgunAdmin::$hook_suffix" (#48)
- Fix "Undefined variable: from_name on every email process" (API and SMTP) (#49)
- Admin code now loads only on admin user access

= 1.5.8 (2017-01-23): =
* Rewrite a large chunk of old SMTP code
* Fix a bug with SMTP + "override from" that was introduced in 1.5.7
* SMTP debug logging is now controlled by `MG_DEBUG_SMTP` constant

= 1.5.7.1 (2017-01-18): =
* Fix an odd `Undefined property: MailgunAdmin::$defaults` when saving config
* Fix strict mode notice for using `$mailgun['override-from']` without checking `isset`

= 1.5.7 (2017-01-04): =
* Add better support for using recipient variables for batch mailing.
* Clarify wording on `From Address` note
* Detect from name and address for `phpmailer_init` / SMTP now will honour Mailgun "From Name / From Addr" settings
* SMTP configuration test will now provide the error message, if the send fails
* Fix `undefined variable: content_type` error in `wp-mail.php` (https://wordpress.org/support/topic/minor-bug-on-version-version-1-5-6/#post-8634762)
* Fix `undefined index: override-from` error in `wp-mail.php` (https://wordpress.org/support/topic/php-notice-undefined-index-override-from/)

= 1.5.6 (2016-12-30): =
* Fix a very subtle bug causing fatal errors with older PHP versions < 5.5
* Respect `wp_mail_content_type` (#37 - @FPCSJames)

= 1.5.5 (2016-12-27): =
* Restructure the `admin_notices` code
* Restructure the "From Name" / "From Address" code
* Add option to override "From Name" / "From Address" setting set by other plugins
* Fix a bug causing default "From Name" / "From Address" to be always applied in some cases
* Moved plugin header up in entrypoint file (https://wordpress.org/support/topic/plugin-activation-due-to-header/#post-8598062)
* Fixed a bug causing "Override From" to be set to "yes" after upgrades

= 1.5.4 (2016-12-23): =
* Changed some missed bracketed array usages to `array()` syntax
* Fix `wp_mail_from` / `wp_mail_from_name` not working on old PHP / WP versions
* Add a wrapper for using `mime_content_type` / `finfo_file`

= 1.5.3 (2016-12-22): =
* Changed all bracketed array usages to `array()` syntax for older PHP support
* Redesigned `Content-Type` processing code to not make such large assumptions
* Mailgun logo is now loaded over HTTPS
* Fixed undefined variable issue with from email / from name code

= 1.5.2 (2016-12-22): =
* Added option fields for setting a From name and address

= 1.5.1 (2016-12-21): =
* Fixed an issue causing plugin upgrades from <1.5 -> >=1.5 to deactivate

= 1.5 (2016-12-19): =
* Added Catalan language support (@DavidGarciaCat)
* Added Spanish language support (@DavidGarciaCat)
* Added German language support (@lsinger)
* Fixed incorrect SMTP hostname
* Applied PSR standards across codebase
* Applied open tracking bugfix
* Applied tags bugfix
* Applied `Mailgun Lists` admin panel bugfix
* Fixed click tracking dropdown
* Fixed click tracking and open tracking
* Now try to process *all* sent mails as HTML, see L201 wp-mail.php for details
* Mailgun logo now loads on both admin pages ;)
* Now using the Mailgun API v3 endpoint!
* Configuration test will now present either an error from the API or the HTTP response code + message

= 1.4.1 (2015-12-01): =
* Clarify compatibility with WordPress 4.3

= 1.4 (2015-11-15): =
* Added shortcode and widget support for list subscription

= 1.3.1 (2014-11-19): =
* Switched to Semantic Versioning
* Fixed issue with campaigns and tags

= 1.3 (2014-08-25): =
* Added check to ignore empty attachments

= 1.2 (2014-08-19): =
* Fixed errors related to undefined variable. https://github.com/mailgun/wordpress-plugin/pull/3

= 1.1 (2013-12-09): =
* Attachments are now handled properly.
* Added ability to customize tags and campaigns.
* Added ability to toggle URL and open tracking.

= 1.0 (2012-11-27): =
* Re-release to update versioning to start at 1.0 instead of 0.1

= 0.1 (2012-11-21): =
* Initial Release

