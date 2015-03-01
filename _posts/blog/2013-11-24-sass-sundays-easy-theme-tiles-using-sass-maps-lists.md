---
title: 'Sass Sundays: Easy theme tiles using Sass maps &#038; lists'
author: Sugar
layout: post
category: blog
---
As I was browsing <a href="https://kuler.adobe.com" target="_blank">Kuler</a> for colour inspiration the other day, I started wondering: what&#8217;s an easy way to automate colour theme thumbnail generation with Sass? It took me about half an hour to come up with a widget I was satisfied with and I promptly posted it on <a href="http://sassmeister.com" target="_blank">Sassmeister</a>.

<a href="http://sassmeister.com/gist/7597251" target="_blank">Take a look at the finished result</a> (and then come back for the detailed writeup).

The HTML is pretty straightforward: a simple unordered list, because that seemed the semantic thing to do. I wanted the whole thing to be as simple as possible, so I just added two classes, <code class="inline">theme</code> (which provides the basic styling) and <code class="inline">theme--themename</code>, which specifies the theme shown.

{% highlight scss %}
<ul class="theme theme--crisp">
  <li>#313340</li>
  <li>#f0f0e3</li>
  <li>#f9c27b</li>
  <li>#ef8531</li>
  <li>#f36519</li>
</ul>

<ul class="theme theme--funky">
  <li>#da0054</li>
  <li>#ff692b</li>
  <li>#fbd726</li>
  <li>#009e8f</li>
  <li>#62b240</li>
</ul>

<ul class="theme theme--autumn">
  <li>#f6484f</li>
  <li>#fbe4b1</li>
  <li>#a9c886</li>
  <li>#417455</li>
  <li>#1d4148</li>
</ul>
{% endhighlight %}

And here is the Sass code used to generate the pretty thumbnails:

{% highlight scss %}
.theme {
  margin-bottom: 20px;
  font-size: 0; // take care of inline-block whitespace

  li {
    width: 30px;
    height: 30px;
    display: inline-block;

    &:first-child {
      border-radius: 4px 0 0 4px;
    }
    &:last-child {
      border-radius: 0 4px 4px 0;
    }
  }
}

$themes: (
  crisp: #313340 #f0f0e3 #f9c27b #ef8531 #f36519,
  funky: #da0054 #ff692b #fbd726 #009e8f #62b240,
  autumn: #f6484f #fbe4b1 #a9c886 #417455 #1d4148
);

@each $theme, $colours in $themes {
  @for $i from 1 through length($colours) {
    $colour: nth($colours, $i);

    .theme--#{$theme} li:nth-child(#{$i}) {
      background: $colour;
    }
  }
}
{% endhighlight %}

I first specify all the common styles in the <code class="inline">theme</code> class. This is all pretty simple stuff, except maybe for that <code class="inline">font-size: 0</code> hack which is a handy way to <a href="http://css-tricks.com/fighting-the-space-between-inline-block-elements/" target="_blank">remove the space between inline-block elements</a>. Normally, I would reset this in the <code class="inline">li {}</code> rule, but in this case I wanted to hide the list items anyway, so I skipped that.

Then, I use the much anticipated <a href="https://github.com/nex3/sass/blob/master/doc-src/SASS_CHANGELOG.md#sassscript-maps" target="_blank">SassScript maps</a> (coming in Sass 3.3) to create a theme collection. Each entry consists of a key (the theme name) and a <a href="http://sass-lang.com/documentation/file.SASS_REFERENCE.html#lists" target="_blank">Sass list</a> used as value (the theme colours). To make it all work, I use two nested loops: for each theme, I go through the colours and assign each of them as the background colour of the appropriate list item. Tada!

So how do I add a new theme? I just add another unordered list with a new <code class="inline">theme--themename</code> class and I add the new entry to the <code class="inline">$themes</code> map in Sass. Simple as that!

#### Possible optimizations

This won&#8217;t work in Internet Explorer < 8, because <a href="http://caniuse.com/#feat=css-sel3" target="_blank">nth-child is not supported there</a>. Still searching for the best way to make this backwards compatible, but I don&#8217;t expect I&#8217;ll lose much sleep over it.

If you need to read more on Sass lists and maps, take a look at Una&#8217;s <a href="http://blog.unakravets.com/post/67057158293/use-sass-3-3-maps-to-make-on-the-fly-color-guides" target="_blank">excellent post about generating colour guides</a> as well as these excellent posts by Hugo Giraudel on <a href="http://hugogiraudel.com/2013/07/15/understanding-sass-lists/" target="_blank">understanding Sass lists</a> and <a href="http://hugogiraudel.com/2013/08/08/advanced-sass-list-functions/" target="_blank">advanced Sass list functions</a>.
