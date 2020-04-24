---
title: Track Embedded Mailchimp Forms in Google Analytics
subtitle: A quick tutorial on how to  track Mailchimp sign up forms in Google
  Analytics via Google Tag Manager
date: 2020-04-24T20:26:45.453Z
summary: A quick tutorial on how I went about tracking Mailchimp forms on a
  website using Tag Manager. This allowed me to see which pages were generating
  the most sign ups to a Mailchimp list and would allow me to further optimise
  designs and placements of the forms to increase sign up rate.
draft: true
featured: false
authors:
  - ""
image:
  filename: mailchimp-icon-300x300.png
  focal_point: Smart
  preview_only: false
---
A quick tutorial on how I went about tracking Mailchimp forms on a website using Tag Manager. This allowed me to see which pages were generating the most sign ups to a Mailchimp list and would allow me to further optimise designs and placements of the forms to increase sign up rate. Historically you would have had to put event tracking on the submit button but Tag Manager’s Form Submission trigger type means you can now track successful submissions on embedded forms like this one. This trigger type is especially useful for when you don’t have control on what happens after a form is submitted.

## 1. Get the Mailchimp Form Code

In your Mailchimp account go to Lists > \[list name] > Sign Up Forms > Embedded Forms. You’ll then get a few options as to the way your form will display. For this example I’ll use a condensed format that just asks for an email input.

Notice the HTML code created in the image below – the red line highlighted is the ID of the form and this is what Tag Manager will use to identify it.

[INSERT IMAGE]

## 2. Track Form Submissions in Analytics

Once the form is on your page and now armed with the form ID you can set up your Tag Manager trigger. You can setup your trigger exactly like in the image below.

[INSERT IMAGE]

Once your trigger is set up you can now create your event. This will push the form submission into your Google Analytics account. Remember to think about Event naming conventions so that the category, action and label all make sense when they’re used for very different things. So this trigger uses your standard Universal Analytics tag type – fill in the values but remember the ‘Value’ tag is optional and can be left blank.

[INSERT IMAGE]

The trigger for this tag is what you just setup so apply this to the tag and you’re done. You can now go into Preview mode in Tag Manager and test this out for real on your site. If you submit a form successfully then you should see the event fire. Once your testing is complete then publish your new container version and see your Analytics account populate with your new Event.

## Word to the wise...

Don't be tempted to try and track this using the double opt in confirm URL from Mailchimp's opt in process. In Mailchimp if your list is set to use double opt in then you're sent an email to verify your email address. Clicking the link takes you to a 'thank you' page with a button link back to your website. The website is set at at Mailchimp's list level so you could make that website URL do the event tracking for a goal – but that isn’t wise for two reasons. First, if you try and use a query string value (e.g. ?registration=1) Mailchimp won't let you do it! They don't like you putting anything but a normal URL without a query value in the list settings, so it would need to be something like domain.com/signup-success. Secondly, this isn't a very effective method of tracking. A user can do the double opt in and just close the tab without clicking the button so you'll miss out on tracking.