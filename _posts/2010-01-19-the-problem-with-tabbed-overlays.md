---
title: The Problem with Tabbed Overlays
author: Sugar
layout: post
permalink: /archives/web-design/the-problem-with-tabbed-overlays
---
Tabs (earlier) and overlays (later) are two of the most widely used web interface patterns. By using them, one can organize a complex user interface in seconds, guiding the user to see what he&#8217;s meant to see and not get confused by other modules of the application.

When combined though, an interesting little beast emerges: the *tabbed overlay*.

A service that uses this kind of overlays is [Google Docs][1]. I use Google Docs often, mainly to collaborate with greek bloggers on interviews that consist a part of my monthly columns at [PC Magazine][2].

The tabbed overlay is used when you try to invite other people to your document. You try it with me: head to [Google Docs][1] and click on *Share* > *Invite people*. You add an e-mail address or two in the invite textarea, you add a message, you click send and invitations go their merry way. You can also change permissions by clicking on the *Advanced permissions* tab and making the necessary changes.

<div class="img" style="margin: 18px 0">
  <img class="alignnone size-full wp-image-1183" title="docs1" src="http://blog.sugarenia.com/wp-content/uploads/2010/01/docs1.png" alt="docs1" width="520" height="362" />
</div>

But what if you want to invite people and change permissions, all in one step?

Unfortunately, Google Docs does not support that. You can either do one or another, since when you click on the *Advanced permissions* tab, the submit button changes from *Send* to *Save & close*. This led to an interesting error by my part, the other day.

I&#8217;ve filled in some e-mail addresses and then clicked on *Advanced permissions*. I then clicked on *Save & close*, thinking that the invitations will be sent anyway, since I&#8217;ve filled in the relevant details in the previous tab. Alas! *Save & close* just saved my permission settings and never sent my invitations.

Needless to say, I was kinda confused when I was informed that my invitation hasn&#8217;t been received. After tinkering a bit with the interface, I got it: I was wrong. The form does not &#8220;remember&#8221; my data from another tab and submits it all together. I must first invite people, then change the permissions. However, strictly from a user point of view, it would make sense if I could just enter my data in all tabs, hit one submit button and be done with, no?

This is one of the cases that the use of this UI module is not optimal. It&#8217;s not a major faux pas on Google&#8217;s part, but the fact that it even got me, a web designer who&#8217;s dabbling into UI design daily, is quite interesting. What about users that do not know about the form submission mechanics?

Maybe a different kind of UI magic should be in place there &#8211; for example, I&#8217;d move the two checkboxes from the *Advanced permissions* tab under a *More options* header on the *Invite people* tab, which would be hidden by default and visible on demand. Something like this: (expanded view)

<div class="img" style="margin: 18px 0">
  <img class="alignnone size-full wp-image-1188" title="docs2" src="http://blog.sugarenia.com/wp-content/uploads/2010/01/docs21.png" alt="docs2" width="520" height="362" />
</div>

I think it makes more sense that way &#8211; and we could skip the underwater usability reef that&#8217;s lurking there.

 [1]: http://google.com/docs
 [2]: http://e-pcmag.gr
