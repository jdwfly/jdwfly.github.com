---
layout: post
title: Drupal, Webforms, and Garlic.js
published: true
---

I love the [Webform](http://drupal.org/project/webform) module. It is by far the best form module in [Drupal](http://drupal.org/). I have used it for so many things that I am sure the creator did not originally intend but it is just so useful.  
Over the last few days one of the sites I maintain needed functionality only fill out a part of the webform and then come back to fill in the rest later. Good news to me is that webform already has this functionality, but the bad news is the UI is terrible. Once enabled the user has to consciously go to the bottom of the form and click the save draft button to save their answers if they are not quite done. In my opinion this should happen seamlessly without the user ever intervening in the process.  

So I ended finding [Garlic.js](http://garlicjs.org). Now I will mention this isn't the only kid on the block for this but it was the first one I found thanks to the [Javascript Weekly](http://javascriptweekly.com) email. Here are my reasons why I choose this:

* Doesn't save to the database (no half-filled forms)
* User doesn't have to think about it
* Small JS library

Should be pretty straight forward add the javascript file and proper attributes and you are done right? Nope, this is where it got tricky and the main reason I wrote this article. To help those poor souls who just want it work.

## Adding the Javascript
This part was pretty simple. I downloaded Garlic.js from their site and threw the garlic.js file into the same folder as my custom module. Since I already had a custom module for this site I just had to add this code.  

<script src="https://gist.github.com/4096800.js?file=module.php"> </script>

This will quite simply load the garlic.js file only on the pages that are nodes of type webform. It is a pretty small file so if you just wanted to always include it through [hook_init](http://api.drupal.org/api/drupal/modules!system!system.api.php/function/hook_init/7) as well.  

## Adding the Attribute to Webforms
This is where things got sticky. Partly because I can be a moron sometimes and read documentation and not comprehend what it is saying and partly because webform (or some other module) was clobbering the attributes on the form. I blame webform because I needed something to blame. I went the [hook_form_alter](http://api.drupal.org/api/drupal/modules!system!system.api.php/function/hook_form_alter/7) route with no luck because of the clobbering issue. Next I tried doing it from the theme layer with the webform-form.tpl.php and that also turned up dry. Finally I figured the only way I could do it was to override the theme_form in my template.php file. Yay it worked!!! Code below.  

<script src="https://gist.github.com/4096831.js?file=template.php"> </script>

## Updating JQuery
But alas, there was a javascript error on the page now. Pesky javascript errors! Of course this was to do with the fact that JQuery version in Drupal is archaic. Also it was not actually mentioned which version of JQuery is needed on the Garlic.js site, but you are going to need at least 1.7 due to the .on function they are using. Thanks to this question on [Drupal Answers](http://drupal.stackexchange.com/questions/28820/how-do-i-update-jquery-to-the-latest-version-i-can-download/) it was easy enough to get JQuery 1.7 installed. Simply download and install the latest dev release of [Jquery Update](http://drupal.org/project/jquery_update) for 7.x of course. Download, install, and configure it to use 1.7 through it's admin page. 
I will say that there were some warnings about updating to 1.7 that some javascript things will be broken. I didn't experience the same problems but they are probably there somewhere.

## Finally
Is this a quick and dirty way to get it done? Yes, but I don't really care. I just needed it to work and this is how I got it done. In hindsight it might be good to make a module instead, but then I would have to use something other than the hook_theme. Either way it works, and at the end of the day that is what matters to me.