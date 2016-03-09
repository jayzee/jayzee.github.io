---
layout: post
title: "Authentication Token and the Coming Robot Invasion"
date: 2016-03-07 22:10:04 -0500
comments: true
categories:
---

<strong>What the hell is this?</strong>

<img src="http://www.joshzizmor.com/fi/authentication_token.png">


WTF? Rails is just generating a long string of letters and numbers and nobodies wondering what is going on?!? Are we being tracked? Are we being monitored by an alien race living on the dark side of the moon? How many more days until skynet? Is it a doomsday clock!?! Or is it just the government tracking everything we do?

<img src="http://static.comicvine.com/uploads/original/10/106298/3763872-7663450062-indep.jpg" >

Turns out this often misunderstood automatically generated piece of code is protecting us from <strong>cross site request forgery</strong>, a term that does not roll off the tongue, so just call it CSRF.

<strong>That doesn't clear anything up. What is CSRF?</strong><br>

CSRF is a vulnerability that arises from the way that applications trust a browser's sessions identification. During a CSRF attack, the attacker tricks a separate web application into executing actions. It can potentially trick the victim into submitting malicious actions. CSRF attacks cannot retrieve data but can change states.

Here's an example, let's say you are using a web site called, 'ForgotTofeedMyCat.com.' (FTFMYC) Meanwhile you have another browser tab open to 'FishFoodFast.com'. You click on a picture of fish on FishFoodFast.com that has malicious code. This code utilizes that fact that you are logged into ForgotToFeedmyCat.com and sends a request to ForgotToFeedmyCat.com asking to delete your account including your 1,000,000 rewards points that you have spent years earning.

Luckily Rails 4 and above automatically protects you from the dreaded CSRF attack! Rails 3 has a cookie based solution which can still be attacked so upgrade to Rails 4 immediately. Rails 3 utilized cookies instead of the Rails session helper which left if vulnerable to CSRF attacks.

<img src="https://top50sf.files.wordpress.com/2011/08/mars-attacks-opener.jpg">

<strong>So how does Rails 4 and above do this magic?</strong><br>
The protect_from_forgery method! <i>Protect_from_forgery</i> is included by default in the application_controller.rb and it is automatically applied when generating new applications.

Here's the high level on how it works. Rails leverages cryptographically random tokens. It places one token in the hidden field, this is the long string of numbers that we see if we inspect the page. It also places one in the user's session. A user session is a piece of memory that maintains a small amount of data about the user. For example if a user put anything in their shopping cart this could potentially be in the session data.

Every time the server has an action it generates and sends  a new token as part of it's response to the browser. When a user responds they resend this token back to the server. If this doesn't match the last one the server sent to you, your request gets aborted since it's likely malicious.

This long string of numbers is secretly added as a hidden input field (aka authenticity_token) to every form.

And if you want to devise your own random token here's the code that Rails uses. It's located in lib/devise.rb
```
def self.friendly_token
  SecureRandom.base64(15).tr('+/=lIO0', 'pqrsxyz')
end
```

::base64 generates a random base64 string. That means there are 64 characters that are available to appear in each spot of the string. The number 15 sets the length of the random string as 15 characters long. Tr works kind of like gsub except its looking for characters instead of strings. Here's an example:

```
'abcde'.tr('bda', '123')
#=> "31c2e"

'abcde'.tr('bcd', '123')
#=> "a123e"
```

The authentication_token is only applied to POST, PATCH and DELETE requests. GET requests do not have tokens since they don't create, alter or destroy.... unlike our future robot masters!

<img src="https://static.perrotin.com/vue/photo/9471_1.jpg?=20150729121805">
