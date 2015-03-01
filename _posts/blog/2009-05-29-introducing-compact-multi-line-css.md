---
title: 'Introducing: Compact Multi-line CSS!'
author: Sugar
layout: post
category: blog
---
Ah, the smell of freshly written CSS code on Friday nights. What&#8217;s not to love.

Over my (few) years of web design experience, I&#8217;ve become <del>anal</del> pretty worked up with what my code looks like. It must be an old trauma from my university years, where well-written code well, let&#8217;s say, wasn&#8217;t exactly the norm (*.c include files* &#8211; yes, I&#8217;ve seen that with my very own eyes). As a result, be it HTML or CSS or PHP or Javascript, I can now proudly say: [I write girl code][1].

(Don&#8217;t look at this site source code &#8211; it&#8217;s not mine. It&#8217;s an adapted template &#8211; yep, don&#8217;t ask when my new template will launch).

One thing that&#8217;s pretty important while authoring CSS for relatively large projects is the way you structure it. We&#8217;ve already discussed [single-line or multi-line][2] in this blog, plus the way you define sections and so-called variables in your CSS are already known topics. But I&#8217;ve decided to beat that dead horse a bit more.

### Multi-line doesn&#8217;t cut it and single-line sucks

There&#8217;s a way to structure CSS that I want to experiment with.

I think that multi-line CSS is very readable but a total waste of whitespace and bandwidth. I also think that single-line CSS can become exceptionally tedious, especially with properties like `border-radius`, that require at least three lines to work relatively consistently across all modern browsers. Working in multi-line CSS and converting it to single-line just before publishing sounds a bit like an overkill to me, all those back and forths!

So what do we get when we mix the best elements of both methods?

The *compact multi-line CSS* structure! Tada!

\*crickets chirping in background\*

Well yeah, lemme show you how it&#8217;s (supposed to be) done.

### How it&#8217;s done

In compact multi-line CSS, you keep the multi-line-ity of it all, but you group &#8220;relevant&#8221; properties. You know which they are: `margin` goes hand in hand with `padding`, `position` loves `top`, `left`, `right`, `bottom`, `font` properties should propably go hand in hand with `line-height` and `letter-spacing`, et cetera, et cetera.

Let&#8217;s take an excerpt of my [CSS3.gr][3] CSS and try to convert it:

<pre class="css">.about-more h4	{
	padding: 0;
	margin: 0;
	border: none;
	color: #666;
	font: 14px Georgia, "Times New Roman", serif;
	text-transform: none;
	letter-spacing: normal;
	position: relative;
}</pre>

In compact multi-line, that would be:

<pre class="css">.about-more h4	{
	margin: 0; padding: 0;
	font: 14px Georgia, "Times New Roman", serif; text-transform: none; letter-spacing: normal;
	border: none;
	color: #666;
	position: relative;
}</pre>

We&#8217;ve gone from 8 lines to 5, without sacrificing readability much. How about:

<pre class="css">#footer-disclaimer	{
	text-align: center;
	font: 10px Georgia, "Times New Roman", serif;
	text-transform: uppercase;
	background: url(./themes/site_themes/css3/skeleton/disclaimer-bg.png) no-repeat top;
	color: #97ACA3;
	letter-spacing: 1.2px;
	padding: 20px 0 10px;
	margin-top: -10px;
}</pre>

&#8230;which gets the short treatment to&#8230;

<pre class="css">#footer-disclaimer	{
	font: 10px Georgia, "Times New Roman", serif; text-align: center; text-transform: uppercase; letter-spacing: 1.2px;
	background: url(./themes/site_themes/css3/skeleton/disclaimer-bg.png) no-repeat top; color: #97ACA3;
	margin-top: -10px; padding: 20px 0 10px;
}</pre>

That&#8217;s 8 lines to 3! Quite a score, innit?

Of course, your mileage may vary and benefits won&#8217;t always be that obvious. Nevertheless, nothing restricts you from further improving this method, by alphabetizing your inline properties or put them in the order that just feels logical for you (for me, `width` is always before `height` and `margin` before `padding`).

I haven&#8217;t used it (yet), but I think I&#8217;ll try it in the [FancyCage][4] CSS I&#8217;m putting together. Well it&#8217;s no [Typekit][5], but it may help you a bit while structuring CSS.

Hey, at least I tried.

 [1]: http://developers.slashdot.org/story/08/06/16/1212240/Do-Women-Write-Better-Code
 [2]: http://blog.sugarenia.com/archives/web-design/call-to-designers-single-line-or-multi-line-css
 [3]: http://www.css3.gr
 [4]: http://www.fancycage.com
 [5]: http://blog.typekit.com/2009/05/27/introducing-typekit/
