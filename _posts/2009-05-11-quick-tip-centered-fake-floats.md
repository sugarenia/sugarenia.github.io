---
title: 'Quick Tip: Centered Fake Floats'
author: Sugar
layout: post
permalink: /archives/web-design/quick-tip-centered-fake-floats
---
Up till (relatively) recently, I had a major gripe with HTML & CSS. I couldn&#8217;t find a proper, efficient, semantic way to *center align left floated elements*.  
Gee, what a mouthful, even writing about it gets me edgy.

Of course there were ways, but I couldn&#8217;t sympathise with any of them. I, for example, always stumbled upon this problem while styling pagination links for galleries and image carousels.

Then came the day when `display: inline-block` became famous and, as by magic, everything changed. After a bit of tinkering, I found an efficient and (mostly) cross-browser way to center elements, without resolving to floats.

You can follow the technique below or skip directly to the witty, quick & dirty [demo I&#8217;ve come up with][1]. Go on, I dare you.

### T3h HTML

So what do we have here? Nothing too fancy, just a simple unordered list:

<pre name="code" class="xhtml"><ul>
  <li>
    <a href="#">‹ Previous</a>
  </li>
  	
  <li>
    <a href="#">1</a>
  </li>
  	
  <li>
    <a href="#">2</a>
  </li>
  	
  <li>
    <a href="#">3</a>
  </li>
  	
  <li>
    <a href="#">4</a>
  </li>
  	
  <li>
    <a href="#">5</a>
  </li>
  	
  <li>
    <a href="#">Next ›</a>
  </li>
  
</ul>
</pre>

### T3h CSS, take #1

So we want this list centered, with each element neatly next to its previous. OK, let&#8217;s get down to business:

<pre name="code" class="css">ul	{
	margin: 20px;
	padding: 0;
	list-style-type: none;
	text-align: center;
}

li	{
	display: inline-block;
	margin: 0;
	padding: 0;
	list-style-type: none;
}

li a	{
	text-decoration: none;
	color: #555;
	padding: 4px 6px;
	border: 1px solid #ccc;
	margin: 0 4px;
}

li a:hover	{
	border: 1px solid #999;
	color: #333;
	background-color: #f2f2f2;
}</pre>

Wee! Looks cool. Now the tricky part: let&#8217;s start the browser testing&#8230;

*(5 minutes later)*

Phew! Firefox, Safari, Opera and Internet Explorer 8 seem to be working fine with it!

And Internet Explorer 6 and 7&#8230; Well&#8230;

<div style="text-align: center">
  <a href="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie6.png"><img class="alignnone size-thumbnail wp-image-1032" title="ie6" src="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie6-330x261.png" alt="ie6" width="330" height="261" /></a>
</div>

<div style="text-align: center">
  <a href="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie7.png"><img class="alignnone size-thumbnail wp-image-1033" title="ie7" src="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie7-330x247.png" alt="ie7" width="330" height="247" /></a>
</div>

Let&#8217;s say they don&#8217;t love inline-block to bits.

### T3h CSS, take #2

Hmmm&#8230; How about turning `display: inline-block` to `display: inline`? Internet Explorer loves `display: inline`! And maybe a little of this trusty ole jar of [hasLayout][2] cream we always have available on our web-des shelf. Let&#8217;s add a `zoom: 1` declaration to `li a`s and see what happens (I used the star and the star-plus hack to target IE6 and IE7 only, but in real life designs, you really should use [conditional stylesheets][3]):

<pre name="code" class="css">* html li	{ display: inline; }
*+html li	{ display: inline; }

li a	{
	text-decoration: none;
	color: #555;
	padding: 4px 6px;
	border: 1px solid #ccc;
	margin: 0 4px;
	zoom: 1;
}</pre>

<div style="text-align: center">
  <a href="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie6b.png"><img class="alignnone size-thumbnail wp-image-1036" title="ie6b" src="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie6b-330x261.png" alt="ie6b" width="330" height="261" /></a>
</div>

<div style="text-align: center">
  <a href="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie7b.png"><img class="alignnone size-thumbnail wp-image-1037" title="ie7b" src="http://blog.sugarenia.com/wp-content/uploads/2009/05/ie7b-330x247.png" alt="ie7b" width="330" height="247" /></a>
</div>

Tada! Mission accomplished. Pat yourself at the back and go get a cup of tea, you&#8217;ve deserved it.

<small>Disclaimer: I don&#8217;t claim this will work in older versions of proper browsers (namely, Firefox 2 or Safari 2 or yada yada). Frankly, I don&#8217;t care, and neither should you. It works fine for the occasion here and there when you want to center stuff. If you have a better / cleaner solution, I&#8217;d be glad to hear all about it in the comments.</small>

 [1]: http://blog.sugarenia.com/demo/CenteredFakeFloats/
 [2]: http://www.satzansatz.de/cssd/onhavinglayout.html
 [3]: http://css-tricks.com/how-to-create-an-ie-only-stylesheet/
