A lot of tickets. Here are the list:

About the payment / invoice related:
The Old ones (before I was sick):

1. Cancel and partial refund.
From: Josh Bois <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: Current
Ultimate Dashboard PRO: Current
Please cancel our license and issue a partial refund for the unused time. It just renewed about a month ago but we wanted to cancel. Otherwise we will have to charge back the full amount with our credit card company


1. Need a refund: I bought extra license by mistake.
From: Martin Löfgren <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.8.17
Ultimate Dashboard PRO: 3.11.2
Hi,
I logged into your site since I hade problems updating to latest version.
By mistake I bought another license, on order #37461, although I already had a recently renewed the license. So now I have paid twice for the plugin.

Can you please help me with a refund?


3. Invoice.
From: Dominik Briechle <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: PRO 2
Ultimate Dashboard PRO: PRO 2
Hello, I just placed an order with you and was charged VAT on the invoice, but that is incorrect due to the reverse charge mechanism. Could you please correct this?

---

New ones:

1. How to un-cancel (to renewal) my subscription ( UDB Plugin ).
From: Andi Buchner <[EMAIL_ADDRESS]>
Hi!
How can I set my subscription again to renewal?


2. Need a refund
From: lars rabe <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 487f0dc5561fccd152b6f1aa40f663a9
Ultimate Dashboard PRO: 487f0dc5561fccd152b6f1aa40f663a9
Hello,

I am not using this plugin anymore.
I would like a refund!


3. Need to close down my account ( BAB Plugin )
From: Sam Crossley <[EMAIL_ADDRESS]>
License: -
Version: -
Hello,

Please could you close down my account.

---

Plugin issues related:

1. Page Access Denied for "Shop Manager" user Role.
From: Chris McMahon <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.11.3
Ultimate Dashboard PRO: 3.11.3
i have user group called shop manager, this is to allow access to employees to help manage the website. i have a plugin that i had created and want them to be able to access called SSW Quotes, i have added the widget and the link to the shop manager as well as the menu editor. when we try to access it from shop manager profile it  says " Sorry, you are not allowed to access this page." thought on how to let access to this

I have checked: I think, he needs to give manage_options cap for the shop manager role.


2. Why is Elementor showing on the side menu when we have it not displaying?
From: Omar Ali <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.8.17
Ultimate Dashboard PRO: 3.11.3
Hi,
This is becoming a challenge lately, I'm sure you're probably tired of it too.
The main culprits are Elementor and Element Pack by BDThemes.
These two always show up in the menus are various times.  How can we resolve this and not have to deal with this issue so frequently?
I have screenshots to show you, but your support form doesn't allow for uploads: https://ultimatedashboard.io/support/#support-form
Please help.

I can't reproduce this one yet. Maybe we should ask for temporary login to investigate further.


3. Errors loading Elementor Theme Builder after update.
From: David Chastain <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.8.17
Ultimate Dashboard PRO: 3.11.3
Hi,

After updating to the latest version, I notice that if I have moved the Elementor Admin Menu items via Ultimate Dashboard, I see an error, "Sorry, you are not allowed to access this page" when trying to access the Theme Builder page, whether I click the admin menu item or just try to reload from an already open URL. The page loads normally if I reset the admin menu, but that's not ideal when there are a bunch of other edits that need to be recreated. Any ideas what the issue could be? I'm guessing that Elementor might be inserting their menus in to the admin in a non-standard way. The newer Elementor versions place their menu obnoxiously high up. Any suggestions would be much appreciated!

I can't reproduce this one yet. Maybe we should ask for temporary login to investigate this further.
But if I login as Editor user, I can replicate.


4. How to hide the admin bar?
From: Andi Buchner <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.8.17
Ultimate Dashboard PRO: 3.11.3
Hi!
Even when I add in the visibility dielt editor and author the admin bar remains visible:man-shrugging::skin-tone-2:
It wound be perfect if I could individual adminbars for each user like in AAM.

I can't reproduce this one yet. Maybe we should ask for temporary login to investigate this further.


5. "Sorry you can't access this page" with Elementor Theme Builder.
From: James <[EMAIL_ADDRESS]>
Hey,

Just recently, I've been unable to access Elementor's Theme Builder area with the Ultimate Dashboard Pro plugin active, giving me "Sorry you can't access this page" message with Admin access. Once I disabled the plugin, I have access. I've been racking my brain, and can't find a fix, so I was wondering if there was a solution for this?


6. Your plugin is crashing Elementor when clicking on Theme Builder.
From: Matt Lance <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.8.17
Ultimate Dashboard PRO: 3.11.3
Hi,
On all of the sites that we use your plugin, 100% of them are creating an error message when clicking on Elementor's Theme Builder.  See below an email thread discussing this with Elementor.

Here’s a screencast: https://screencasts.intelliplans.com/recordings/xH1QUJFDxGMwVhhSXd66

Elementor Support wrote:

I finally able to identify the cause of this issue, after doing a troubleshoot and deactivation of your plugin. I found out that your Ultimate Dashboard PRO is the one causing an issue from Elementor theme builder. I highly suggest that you reach out from their end so they could check the conflict from Elementor.


7. Login Customizer WebP support and Elementor admin menu hover conflict
From: Danny Wisholm <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.8.17
Ultimate Dashboard PRO: 3.11.3
Hi Ultimate Dashboard Support,

I would like to report two issues.

First, `.webp` background images are removed when saving the Login Customizer. It looks like `sanitize_image()` in `ultimate-dashboard/helpers/class-content-helper.php` validates against a MIME whitelist that does not include:

```php
'webp' => 'image/webp'
```

So the selected WebP image previews correctly, but after saving, the `udb_login['bg_image']` value is sanitized back to an empty value. Could you please add WebP support to the Login Customizer image sanitizer?

Second, there seems to be a compatibility issue with Elementor’s new admin submenu/sidebar navigation. On Elementor admin pages, Elementor adds the body class `e-has-sidebar-navigation` and loads a rule like this:

```css
.e-has-sidebar-navigation #adminmenu li.menu-top:hover,
.e-has-sidebar-navigation #adminmenu li.opensub > a.menu-top,
.e-has-sidebar-navigation #adminmenu li.wp-has-current-submenu,
.e-has-sidebar-navigation #adminmenu li.wp-has-submenu:hover,
.e-has-sidebar-navigation #adminmenu li > a.menu-top:focus {
   background: transparent;
}
```

This overrides the admin menu hover background color configured in Ultimate Dashboard. The hover color briefly flashes, then disappears, while viewing Elementor admin pages. If Ultimate Dashboard is disabled, the native WordPress admin menu hover behavior works as expected.

Could you please check compatibility with Elementor’s new admin menu/sidebar navigation and ensure Ultimate Dashboard’s configured admin menu hover color still applies?

I have checked for the WebP file on Login Customizer (for Background Image), and confirmed it's not working / not supported yet.

---

1. License Limit Reached (UDB)
From: Andy Morris <[EMAIL_ADDRESS]>
License: [license_key]
Ultimate Dashboard: 3.8.17
Ultimate Dashboard PRO: 3.11.2

Subject: license limit reached

Message Body:
I have created a staging site for updates. I didn't deactivate before cloning my site so I'm sure I've got two sites running the same license key.

I deactivated the plugin on staging7.calvaryumc.com
I followed the directions here: https://ultimatedashboard.io/docs/license-key-issues/

I still have it giving me a error: Your license key has reached its activation limit.

In addition...even though my license key was emailed to: andy@calvaryumc.com, I can't seem to log in or reset my password. I get the message -Error: There is no account with that username or email address.


2. Invalid Item ID (WPBF_Premium)
From: Adrian Righi <[EMAIL_ADDRESS]>
License: [license_key]
Premium Version: Newest
Theme Version: Newest
Website: https://malea-pilates.de/
Subject: False Key
Message Body:
Hello there,
on my new customer website the license key won't work. It says: Invalid Key.
Even though I already have 11 websites connected.


3.  Invalid Item ID (WPBF_Premium)
From: ABU ISSAC <[EMAIL_ADDRESS]>
License: [license_key]
Premium Version: Ultimate Dashboard PRO
Theme Version: 3.8.17
Website: ktini.com
Subject: licence key is inactive
Message Body:
Dear Team
The license key seems to be inactive for the ultimate dashboard pro
i just bought it yesterday

4. Close Account (WPBF)
From: Sam crossley <[EMAIL_ADDRESS]>
Subject: Close Account

Message Body:
Please could you close this account. Thank you
