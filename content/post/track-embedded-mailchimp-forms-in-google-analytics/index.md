---
title: Track Embedded Mailchimp Forms in Google Analytics
subtitle: A quick tutorial on how to  track Mailchimp sign up forms in Google
  Analytics via Google Tag Manager
date: 2020-04-24T20:26:45.453Z
summary: A quick tutorial on how to track Mailchimp sign up form submissions in
  Google Analytics via Google Tag Manager
draft: false
featured: false
authors:
  - Myles
tags:
  - email
  - ""
image:
  filename: mailchimp-icon-300x300.png
  focal_point: Smart
  preview_only: false
---
A quick tutorial on how I went about tracking Mailchimp forms on a website using Google Tag Manager (GTM). This allowed me to see which pages were generating the most sign ups to a Mailchimp list and would allow me to further optimise designs and placements of the forms to increase sign up rate. Historically you would have had to put event tracking on the submit button but Tag Manager's *Form Submission* trigger type means you can now track successful submissions on embedded forms like this one. This trigger type is especially useful for when you don’t have control on what happens after a form is submitted.

## 1. Get the Mailchimp Form Code

In your Mailchimp account go to Lists > \[list name] > Sign Up Forms > Embedded Forms. You will then get a few options as to the way your form will display.

Let's have a look at (a stripped back version of) Mailchimp's embed code:

```
<!-- Begin Mailchimp Signup Form -->
<link href="//cdn-images.mailchimp.com/embedcode/classic-10_7.css" rel="stylesheet" type="text/css">
<style type="text/css">
	#mc_embed_signup{background:#fff; clear:left; font:14px Helvetica,Arial,sans-serif; }
	/* Add your own Mailchimp form style overrides in your site stylesheet or in this style block.
	   We recommend moving this block and the preceding CSS link to the HEAD of your HTML file. */
</style>
<div id="mc_embed_signup">
<form action="https://packtpub.us11.list-manage.com/subscribe/post?u=[USERVALUE]&amp;id=[LISTVALUE]" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">
	<h2>Subscribe</h2>
<div class="indicates-required"><span class="asterisk">*</span> indicates required</div>
<div class="mc-field-group">
	<label for="mce-EMAIL">Email Address  <span class="asterisk">*</span>
</label>
	<input type="email" value="" name="EMAIL" class="required email" id="mce-EMAIL">
</div>
	<div id="mce-responses" class="clear">
		<div class="response" id="mce-error-response" style="display:none"></div>
		<div class="response" id="mce-success-response" style="display:none"></div>
	</div>    <!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
    <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_693897ba2220b83ddb807103a_c970747b22" tabindex="-1" value=""></div>
    <div class="clear"><input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
    </div>
</form>
</div>
<!--End mc_embed_signup-->
```

We're most interested in the **<form>** element and in particular the ID attribute which is *id="mc-embedded-subscribe-form"*.

## 2. Track Form Submissions in Analytics

Once the form is on your page and now armed with the form ID you can set up your Tag Manager trigger. You can setup your trigger exactly like in the image below.

\[INSERT IMAGE]

Once your trigger is set up you can now create your event. This will push the form submission into your Google Analytics account. Remember to think about Event naming conventions so that the category, action and label all make sense when they’re used for very different things. So this trigger uses your standard Universal Analytics tag type – fill in the values but remember the ‘Value’ tag is optional and can be left blank.

\[INSERT IMAGE]

The trigger for this tag is what you just setup so apply this to the tag and you’re done. You can now go into Preview mode in Tag Manager and test this out for real on your site. If you submit a form successfully then you should see the event fire. Once your testing is complete then publish your new container version and see your Analytics account populate with your new Event.

## Word to the wise...

Don't be tempted to try and track this using the double opt in confirm URL from Mailchimp's opt in process. In Mailchimp if your list is set to use double opt in then you're sent an email to verify your email address. Clicking the link takes you to a 'thank you' page with a button link back to your website. The website is set at at Mailchimp's list level so you could make that website URL do the event tracking for a goal – but that isn’t wise for two reasons. First, if you try and use a query string value (e.g. ?registration=1) Mailchimp won't let you do it! They don't like you putting anything but a normal URL without a query value in the list settings, so it would need to be something like domain.com/signup-success. Secondly, this isn't a very effective method of tracking. A user can do the double opt in and just close the tab without clicking the button so you'll miss out on tracking.