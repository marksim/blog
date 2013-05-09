---
layout: post
title: Fixing "Freemium" issues in the App Store
categories: blog op-ed
---
Recently, Apple allowed Apps that are free to add in-app charges in order to allow users to "try before they buy."

Interestingly, <a title="BrainJuice, LTD" href="http://drinkbrainjuice.com/">BrainJuice</a>, a developer of the game <a title="Arcade Hockey" href="http://drinkbrainjuice.com/arcade-hockey">Arcade Hockey</a> recently decided to move to this freemium model, but made a major mistep in my opinion.  The original app was $0.99, but the newly updated version is free, but contains ads.  In order to turn off the ads, you must pay $0.99, which will mean that you basically paid twice for the same app.  There might be a bug fix or two here and there, but nothing deserving of doubling the price of an app.

To me, this feels like a bait and switch, but the author insists there was no other way.   He asserts that it was highly undesireable to create a second free version of the app because of the way their APIs keys work with a third party service they use.  I think there *was* a way around this, which I'll explain here:
<ol>
	<li> BEFORE you switch to the freemium model, you create a new update that "phones home" with a unique identifier for the device which "registers" the device</li>
	<li> Give the users at least a month to download the update and launch it once so that they are officially "tagged"</li>
	<li> Within the freemium app, create a check if the "ads" flag is still on to check the server to see if the device ID is in the "nice" list.  If so, turn the flag off... your user has already paid.</li>
	<li> If not, turn on a "dont check" flag so you don't have to keep checking and wasting lots of bandwidth.</li>
</ol>
Does this approach have its problems?   Of course.   If the users somehow misses the "middle" upgrade, then they miss out.   It also puts you at risk for security issues.  However, it does afford you the ability to *grant* users a free copy at your whim.

Unfortunately, because BrainJuice didn't think through the problem the whole way, they have abandoned a good and vocal portion of their fanbase--so this doesn't help them at all.

But for you who are thinking of transitioning... think twice, and get it right.
