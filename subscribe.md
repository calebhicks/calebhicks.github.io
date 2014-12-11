---
layout: page
permalink: /subscribe/index.html
title: Subscribe
description: "Subscription options to stay updated with {{site.name}}"
---

## A few ways to keep up with CalebHicks.com:

* Follow the author on [Twitter][1]
* Follow the site itself on [Twitter][2]
* Subscribe via [RSS][3]
{% if site.MCusername %}* Subscribe to e-mail updates  {% endif %}

{% if site.MCusername %}
<!-- Begin MailChimp Signup Form -->
<div id="mc_embed_signup">
	<form action="http://{{site.MCusername}}.us5.list-manage.com/subscribe/post?u={{site.MCu}}&amp;id={{site.MClistid}}" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate subscribe" target="_blank" novalidate>
			<h3 style="text-align:center;"></h3>
		<div class="mc-field-group">
			<label for="mce-EMAIL" class="vh">Email Address </label>
			<input type="search" value="" name="EMAIL" class="required email searchword" id="mce-EMAIL" placeholder="Enter your e-mail to receive updates when {{site.author}} publishes">
		</div>
		<div id="mce-responses" class="clear">
			<div class="response" id="mce-error-response" style="display:none"></div>
			<div class="response" id="mce-success-response" style="display:none"></div>
		</div>
		<div class="clear" style="display:none;">
			<input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button">
		</div>
	</form>
</div>

<!--End mc_embed_signup-->
{% endif %}

[1]: http://twitter.com/calebhicks
[2]: http://twitter.com/calebhickscom
[3]: http://www.calebhicks.com/feed.xml