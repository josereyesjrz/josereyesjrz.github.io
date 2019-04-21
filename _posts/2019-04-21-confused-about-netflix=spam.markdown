---
layout: post
title:  "Confused about Netflix spam"
---
Today I checked my spam folder, because why not? I noticed I had spam message about my Netflix membership having been put on hold. I checked the sender email and sure enough it was an emailer.netflix.com email address. I was confused as it seemed to be legit. I checked my Netflix account settings and it was not on hold, and in fact I had set a different email address in my account than the one that received the spam email. I assumed maybe the fake netflix email address had unicode characters or something. I decided to check the raw email and this is what I found:

	Received-SPF: Fail (protection.outlook.com: domain of emailer.netflix.com does
	 not designate 139.162.229.236 as permitted sender)
	 receiver=protection.outlook.com; client-ip=139.162.229.236;
	 helo=li1514-236.members.linode.com;

Clearly, someone tried to spoof the sender with a Netflix email address, from a linode email server. Checking a real netflix email:

	ARC-Authentication-Results: i=1; mx.google.com;
       dkim=pass header.i=@netflix.com header.s=snogjgwpbj2zu6oq3sqnwholf5r3tejk header.b="ik/Oj61/";
       dkim=pass header.i=@amazonses.com header.s=6gbrjpgwjskckoa6a5zn6fwqkn67xbtw header.b=epY6I7NO;
       spf=pass (google.com: domain of
       0100016a268c3f50-468a3d14-4679-4144-9940-12306dc09f7b-000000@mailer.netflix.com
       designates 54.240.41.45 as permitted sender)

Obviously we see that this is a real Netflix email from their mail servers. Also, the corrent address is mailer.netflix.com.

The moral of the story is, phishing goes beyond checking the address. This was a convincing, real looking email with an actual netflix.com address. Without knowledge about how email works, someone looking at their spam inbox maybe have thought it was a false positive and possibly fall into a scam. Maybe email software should expose to the end user why a certain message was flagged as spam.