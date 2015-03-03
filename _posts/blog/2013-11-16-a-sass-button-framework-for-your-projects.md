---
title: 'Sass Sundays: A Button Framework for your Projects'
author: Sugar
layout: post
category: blog
redirect_from: "/archives/web-design/a-sass-button-framework-for-your-projects"
---
I love Sass. It&#8217;s my bread & butter these days &#8211; I read, write and research Sass for most of my workday. Heck, for most of my day. It really transformed the way I work.

Sass really shines in making boring, repetitive styling more efficient and, dare I say, fun. I also happen to love styling buttons but their styling can get redundant after a while, so let&#8217;s get to that!

I posted a <a href="http://sassmeister.com/gist/7482701" target="_blank">simple button framework</a> in Sassmeister yesterday. Let&#8217;s take a deeper look at it.

{% highlight html %}
<button class="btn btn--primary">Primary button</button>
<button class="btn btn--primary">Secondary button</button>
{% endhighlight %}

The HTML is pretty straightforward. Just a <code class="inline">&lt;button&gt;</code> and two classes. The first class adds the basic styles, stuff like typography and padding, while the second class determines its colours. Quite basic.

I prefer using multiple classes when coding HTML because I like the luxury of using just one class (<code class="inline">.btn</code> in this case) to target all buttons in a module. Sure, I could use a selector like <code class="inline">[class^="btn--"]</code> but an extra class just works better for me.

I also use the <a href="http://bem.info/method/" target="_blank">BEM syntax</a> for this. BEM is a convention created by the intelligent folks at <a href="http://company.yandex.com" target="_blank">Yandex</a> which I consider one of the best ways to write modular CSS. I won&#8217;t say more, just read this <a href="http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/" target="_blank">excellent article</a> by <a href="https://twitter.com/csswizardry" target="_blank">Harry Roberts</a> on that.

Now, the magic. I use Sass & Compass in this example, but this can easily be done in vanilla Sass as well. 

{% highlight scss %}
// ----
// Sass (v3.3.0.rc.1)
// Compass (v0.13.alpha.10)
// ----
 
@import "compass";

// Basic button styles
.btn {
  cursor: pointer;
  border: none;
  border-radius: 2px;
  display: inline-block;
  text-align: center;
  vertical-align: middle;
  padding: 8px 16px;
  box-shadow: 0 1px 2px black(0.1), inset 0 1px 0 white(0.15), inset 0 -1px 0 black(0.15);
  font: bold 14px "Helvetica Neue", Helvetica, sans-serif;
  white-space: nowrap;
  
  &#038;:active,
  &#038;.active {
    outline: none;
    position: relative;
    top: 1px;
    box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.15);
  }
}
 
// Button mixin
@mixin button($background-color, $text-color) {
  @include background(linear-gradient(lighten($background-color, 3%), darken($background-color, 3%)));
  color: $text-color;
 
  @if lightness($text-color) < 50% {
    text-shadow: 0 1px 0 rgba(255, 255, 255, 0.6);
  } @else {
    text-shadow: 0 -1px 0 rgba(0, 0, 0, 0.3);
  }
 
  &#038;:hover,
  &#038;.hover { 
    @include background(linear-gradient(lighten($background-color, 5%), darken($background-color, 1%)));
    text-decoration: none;
  }
}
 
// Colour variations
.btn--primary   { @include button(#ea6ca4, #fff); }
.btn--secondary { @include button(#d6d6d6, #707070); }
{% endhighlight %}

First, I add some basic styles to the <code class="inline">.btn</code> class. That way, even if I don&#8217;t add a second class for some reason, I still have a simple button that doesn&#8217;t look broken. This class also includes the <code class="inline">:active</code> state styles, since these are common for all buttons (a tiny nudge downwards and a different shadow).

Then I create a button mixin which will generate all colour-related styles for our buttons. It takes two arguments, the background color and text colour respectively. It creates a light gradient by combining a slightly darker and a slightly lighter version of the background colour, then checks to see if the background is dark or light and adds a bottom white or top black shadow to create an inset effect. It also adds hover styles by tweaking the background gradient to a lighter effect.

And that&#8217;s pretty much it! Check the section below for some tweaks you could do. Now get this into a _buttons.scss partial and get cracking!

#### Possible optimizations

As I mentioned above, I&#8217;m a fan of the multi-class approach. If you wish to just use one class for your buttons, you can convert the .btn class above to a <a href="http://sass-lang.com/documentation/file.SASS_REFERENCE.html#placeholder_selectors_" target="_blank">placeholder</a> (%btn), then you can extend it in each of your colour classes to get the same result. That&#8217;s what <a href="http://t.co/GiQxiw1GUJ" target="_blank">Elyse Holladay</a> does in <a href="http://t.co/NhqdOB47uL" target="_blank">her take here</a>.

You can also automate the text colour depending on the background and thus reduce the number of arguments of the button mixin to one. You can use the text-shadow trick I&#8217;ve used above or one of the more advanced techniques that can be found in this <a href="http://t.co/Q1DleoH2PV" target="_blank">amazing presentation</a>. So much win!
