---
title: Using BEM in the Real World&#58; Pitfalls &amp; Advice
author: Sugar
layout: post
category: blog
---
It feels that new structured naming conventions for CSS are popping up every day. The way I see it, this means that we’re all working on bigger, more complex CSS codebases, and conjuring random class names on a whim just won’t cut it anymore.

One of the first conventions I liked was BEM. I first read about it in a [blog post by Harry Roberts](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) back in 2013, who used simple examples to explain the basic idea. It looked like a great solution for creating self-documented, self-contained reusable modules to me.

BEM is one of those things that look deceivingly simple to use, but it can be surprisingly easy to mess up. If you start abusing it, you can come up with an unwieldy codebase in dire need of refactoring very quickly. I know. I’ve been there.

These are some ideas that stuck with me the past year that I’ve been working with BEM on the [Workable](http://www.workable.com) codebase:

#### Avoid element nesting

When you’re getting started with BEM, there’s a big chance you’ll end up with some pretty long selector names which mimic your HTML structure. Something like this:

{% highlight html %}
<div class="block">
  <div class="block__element1">
    <div class="block__element1__element2"></div>
  </div>
</div>
{% endhighlight %}

{% highlight scss %}
.block {}
.block__element1 {}
.block__element1__element2 {}
{% endhighlight %}

Needless to say, this doesn’t look good, especially if you add modifiers to the mix:

{% highlight scss %}
.block__element1__element2—modifier {}
.block__element1—modifier1__element {}
{% endhighlight %}

I admit using selectors like these as my first foray into BEM. They’re still there in the Workable CSS. I’m not proud of it, but then again, who doesn’t feel shame when looking at their old code?

I found out the best way to do BEM is to keep it as flat as possible. Using a selector like <code class="inline">.block__element1__element2</code> presumes that <code class="inline">element2</code> will always be a child of <code class="inline">element1</code> in the markup, and you want to avoid that. Just stick to one level of nesting:

{% highlight html %}
<div class="block">
  <div class="block__element1">
    <div class="block__element2"></div>
  </div>
</div>
{% endhighlight %}

{% highlight scss %}
.block {}
.block__element1 {}
.block__element2 {}
{% endhighlight %}

This is a better solution in two ways: your selectors will be looking shorter and prettier, and you can easily make changes to your markup without having to refactor a bunch of CSS classes.

#### Use SMACSS state classes for common modifiers

I admit it took me a while to grasp this one. While coding up our modules, I realised that a lot of the modifier classes I used were all about common states like disabled, hover, active etc.

{% highlight scss %}
.block--hover {}
.block__element--active {}
.block__element--disabled {}
{% endhighlight %}

Since these are all pretty common states that apply to a lot of elements, I now tend to favour using [SMACSS](https://smacss.com/)-style state classes instead of longer BEM modifier classes:

{% highlight scss %}
.block.is-hovered {}
.block__element.is-active {}
.block__element.is-disabled {}
{% endhighlight %}

It doesn’t look much different in CSS, but check out the difference in markup:

{% highlight html %}
<div class="block block--hover">
  <div class="block__element block__element--active">
    ...
  </div>
</div>
{% endhighlight %}

instead of

{% highlight html %}
<div class="block is-hovered">
  <div class="block__element is-active">
    ...
  </div>
</div>
{% endhighlight %}

I think it looks much cleaner, and now you can use BEM modifier class for module-specific states that make sense.

I find this easier when collaborating with Javascript developers as well. In 90% of the cases, you don't need to ask for a specific modifier class, all they need to add is an <code class="inline">.is-{state}</code> class and you’re good to go.

#### Keep your Sass structure flat

I've repeated this piece of advice many times, especially to new Sass users. It’s not particularly tied to BEM-style codebases.

Repeat after me: *there’s no reason to mimic your HTML structure in Sass*.

{% highlight scss %}
.block {}
.block__element {}
.block__element--modifier {}
{% endhighlight %}

instead of

{% highlight scss %}
.block {
  .block__element {
    .block__element--modifier {
    }
  }
}
{% endhighlight %}

Up till recently, we used Sass nesting to mentally group blocks of code that belong to the same module. There's no need to do this any more, since BEM already allows us to check which element belongs to which block, just by looking at the class name.

Nesting your rules will increase specificity and make maintenance much harder in the long run. It also makes your Sass code look much more complicated than it really is. Since your aim should be keeping your CSS specificity as low as possible, avoid nesting your BEM classes (and while you’re at it, avoid using IDs for styling as well).

#### You don’t have to use BEM for everything

One of the most common questions new adopters ask is “how do I know when I should and when I shouldn’t use BEM”? I don’t have the perfect answer to that, but I’ll say it does get easier with experience.

Since it’s so good in describing reusable, self-contained modules, I automatically switch to BEM mode when coding anything that goes into our <code class="inline">modules</code> folder. On the other hand, I don’t use BEM for layout classes, helper classes, base styles and scaffolding.

There’s another catch: third-party code. In Workable, we still have some leftover [Bootstrap](http://getbootstrap.com) CSS, mainly because some Bootstrap scripts are very handy and coding our own modals and tooltips would take precious development hours (plus it’d be boring as heck). This code is inconsistent with our BEM style, but since it’s not easy to tweak third-party Javascript just to follow a CSS naming convention, we choose to be fine with that.

#### Conclusion

In the world of [XXLCSS](https://speakerdeck.com/sugarenia/xxlcss-how-to-scale-css-and-keep-your-sanity), there’s no silver bullet, no one-solution-fits-all. Just choose the solution that looks best for your project at the moment and don’t lose much sleep over it.

BEM seemed (and still seems) to me like a great way to add order to CSS chaos. I’d advise you to not think about it too much before trying it out. Worst case scenario, you end up with some really long weird class names you can search & replace anytime.

Also important: no reason to refactor your project every few months just because a new, shiny naming convention came out! That’s what gives us a bad rep, folks.

<small>I’m pretty sure there’s a dark room somewhere where software engineers are probably laughing their asses off right now.</small>
