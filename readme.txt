=== Slack ===
Contributors:      akeda
Tags:              slack, api, chat, notification
Requires at least: 3.6
Tested up to:      3.8.1
Stable tag:        trunk
License:           GPLv2 or later
License URI:       http://www.gnu.org/licenses/gpl-2.0.html

This plugin allows you to send notifications to Slack channels when certain events in WordPress occur.

== Description ==

By default, there are two events that can be sent to Slack:

1. When a post is published
1. When there's a new comment

It's possible to add more events using `slack_get_events` filter. Here's an example to add new event when a user is logged in:

`
add_filter( 'slack_get_events', function( $events ) {
	$events['user_login'] = array(
		'action'      => 'wp_login',
		'description' => __( 'When user logged in', 'slack' ),
		'message'     => function( $user_login ) {
			return sprintf( '%s is logged in', $user_login );
		}
	);

	return $events;
} );
`

The new event will be shown on integration setting and if enabled anytime a user is logged in you'll get the notification in Slack.

**Development of this plugin is done on [GitHub](https://github.com/gedex/wp-slack). Pull requests are always welcome**.

== Installation ==

1. Upload **Slack** plugin to your blog's `wp-content/plugins/` directory and activate.
1. Add new **Incoming WebHooks** service in your Slack, the URL is `https://<SUBDOMAIN>.com/services/new/incoming-webhook` (replace `<SUBDOMAIN>` with your Slack's subdomain). Once created, note the URL of the service (you'll set it into integration entry in your WordPress).
1. Go to **Slack** menu in your WordPress to add the integration (make sure you're logged in as an Adminstrator).

== Screenshots ==

1. Integrations list. Yes, you can add more than one integration.
1. Edit integration screen.
1. Your channel get notified when some events occur.

== Changelog ==

= 0.1.0 =
Initial release