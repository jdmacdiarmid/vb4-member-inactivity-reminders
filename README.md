#EMAIL REMINDERS FOR INACTIVE USERS v2.2.1 
This extension is for vBulletin v3.8 and up.

# About vBulletin
vBulletin is a proprietary Internet forum software package sold by MH Sub I, LLC doing business as vBulletin. It is written in PHP and uses a MySQL database server. Similar products include XenForo, WordPress, Joomla, Drupal, MyBB, and phpBB.

## Credits

Like others before me, I've been using this mod quite a while on previous versions of vBulletin. Since updates and support for older 
versions had stopped, I figured I would make my own modifications and help others that have enjoyed it as well. I want to add back 
in some of the previous functionality that has been left out as well as add some new functionality. 

I want to give full credit thanks to the developers of versions 1.0.6 to 1.1.3 from which this was derived:

C Braithwaite 
<http://www.vbulletin.org/forum/member.php?u=126221>

robertjandreu
<http://www.vbulletin.org/forum/member.php?u=230904>

## What does it do? 
From time to time, members may forget to revisit your forum whether it's due to a busy schedule or maybe they forgot to bookmark the url to your site. For whatever reason, this modification will send out reminder emails to members that have been inactive on your site based on their last activity date, inactivity threshhold and several other options. 

Here is a list of features which can be changed through the Admin Control Panel (AdminCP):

### Enable or Disable Extension
This allows the forum admin to turn the mod on or off.

### Inactivity Grace Period
Set the number of days a user can be inactive (grace period) before email is sent. 

Example: If Inactivity Grace Period is set for 60 days. Member FooBarBob has been inactive for a while. On day 61, FooBarBob will begin receiving reminder emails.

### Send Email Once
If Yes, when members become inactive they will receive one reminder only. 

### Reminder Email Frequency
This determines how often an email is sent to members after receiving their first reminder. 

### Reminder Email Format
Allows the forum admin to set what format emails are sent - TEXT or HTML.

### Reminder Email Subject
Allows the forum admin to customize the subject line. This is configurable in the vBulletin language file and can be translated.

### Reminder Email Body
Allows the forum admin to customize the email body. This is configurable in the vBulletin language file and can be translated.

### Usergroups to be sent a reminder email.
Allows the forum admin to choose what member groups to include. 

### Exclude User Ids.
Edit number of emails send totally (Max Reminders)

Example: If the Send Once option is set to false, and this option is set to 50. Inactive members will only receive 50 reminders.

### Log All Inactive Users Contacted
Opt-Out Feature for members - Include an opt-out link in reminder email. (Thanks to Gene Steinberg)

## Install Instructions

* Important: v2 and UP will not work on older releases of vBulletin. This was written specifically for vBulletin 4.x
* If you have a previous version of this mod installed, I strongly recommend backing up your reminder email subject and body. This mod will over-write any changes you made to them. 
* In Version 2.x, Reminder Email Contents has been moved to using vbphrases. Look in the install.txt file with this upload for a list of phrases used in this mod.

1. Upload file in the upload folder to your server
2. If you have installed one of the old versions, you will need to uninstall it.
3. Go to Plugs & Products -> Product Manager -> Add New Product.
4. Import the product xml from the zip file.
5. Go to Vbulletin "Settings" -> Options -> Inactivity Reminder Emails.
6. Configure as needed.

Note: This mod installs a plugin that adds a link in your footer, however 
it can be disabled via the AdminCP. If you find this mod useful, please don't disable this option.

### Update 

** UpDate 2.2.0 **
* Removed logic to base inactivity on Last Post or Last Visit date. Inactivity is now based on 
Last Activity Date. 
* Removed option to select what to base inactivity on from the mod settings screen. 
* Fixed a couple typos in SQL update queries.
* Exporting the following additional values which can be used in reminder email templates if desired:
  $lastvisit 	- Formatted Date/Time Value - members last visit to the site.
  $lastactivity - Formatted Date/Time Value - members last activity on the site.
  $lastpost	- Formatted Date/Time Value - members last post date on the site.
  $lastreminder - Formatted Date/Time Value - Date member was sent last reminder email.
  $days_since_lastpost - Number of days since member last posted.
  $days_since_lastreminder - number of days since last reminder was sent.

Please let me know if you would like other values made available. 

** Update 2.1.5**

* Full Rewrite - Mod no longer has the option of adding a footer credit to the end of 
  your website nor will it add a footer credit to outgoing emails. Enable/Disable options
  for on the mod settings screen in the AdminCP have also been removed.

* New Reminder Optout: Currently this is only accessable from emails being sent out.
  Please let members know that they may receive one more email at which time they can 
  choose to optout/unsubscribe by clicking on the embedded link or copying/paste it into
  their browser. 

* Logic used to determine when emails are sent out has been corrected. I'm basically 
  subtracting the current date from the last visit date or the last post date 
  (depending on how you have it set in the mod settings screen) to get the number of
  days it's been. That number is then compared with the grace period setting along with
  the other settings in the mod settings screen. 

  For instance: This query snippet will get the number of days since the last post date.
  TIMESTAMPDIFF(DAY, FROM_UNIXTIME(lastpost), FROM_UNIXTIME(UNIX_TIMESTAMP()))

  Mod will process members who have become inactive and never received a reminder first.
  It will then process members who are still inactive and have not received a reminder since 
  they received their previous reminder based on the frequency set in the mod settings screen.

* Issues when emails were sent out had the incorrect "From" address and listed the host domain name.
  This should be resolved now.

* Issue regarding special characters in the usernames trying to be added to the database has been resolve.

* New data fields have been implimented for keeping track of when reminders are sent out and how 
  many a member has received. If you have a had this mod installed since version 1.1.4, it will look for
  those fields and rename them so you do not loose previous data in those fields, otherwise new fields will
  be added.

* I've added the ability to turn off the admin report. In this version, if it is enabled, you may receive 
  2 reports.  One report for members that have never received a reminder and one for members who haven't received
  a reminder since the last reminder based on the frequencey setting in the mod settings screen,

* Reminder's sender and email address are correctly determined now. Should now reflect site name with the webmasteremail address 
  as the reply to.

* There may be other things fixed. Just no way of really tracking them yet. You should see my office. I have sticky notes all over 
  the place. LOL  j/k  :)

** Update 2.1.1 (3/30/2010) - Bug Fix **
* FIX - Removed extra where clause in query where scheduled task script was performing an update when inactive reminders where based on last post count.
* FIX - Email Phrase Templates - Changed $bburl variable to $forumurl to correct a broken unsubscribe link. 
* NEW - Includes tool to reset the date and count of reminder emails that were previously sent to users. This tool is mainly for testing purposes. 

** Update 2.1.0 (3/26/2010) - Bug Fixs and some new features **
* Edit number of emails send totally
* Choose whether inactivity is based on members "Last Post" or their "Last Activity"
* Keep a log of all inactive users contacted
* Opt-Out Feature for members - Include an opt-out link in reminder email. (Thanks to Gene Steinberg) 
* Added a link to the bottom of the default email template phrases that members can use to unsubscribe from reminder emails.

** Update 2.0.1 (03/15/2010 9:00pm) - Bug Fix **
* FIX - Issue related to processing users in a batch
configuration. Mod was checking for a field length 
greater than zero instead of a numeric value greater
than zero. 

** Update 2.0.0 (03/15/2010) **
* NEW - Complete rewrite of addon 
* NEW - Can specify number of users to process at one time. 
* NEW - Send reminder emails in either text or html format.
* NEW - Email subject and message body is vbphrased.

** Update 1.1.4 (03/05/2010) **
* FIX - Would continue to send out email more often than specified intervals
        due to incorrect setting in cron job.
* NEW - Exclude userids from processing. 

** Todo: **
* Multiple Email Templates
* Detect bounced email, mark it as bounced so the user is not to be contacted again so as to avoid spam, 
  and then move that user into a seperate usergroup.
* Automatically send a message to the member via PM about the bounced email problem. That way if and when they login, 
  they know there's a problem and can write to site admin with their new email address. (Thanks to Gene Steinberg)
* Specify alternative emails to send to reduce repetition

If you have any other features that you would like to have added, please let me know.
