---
title: Print-friendly feature tables with CSS
author: Sugar
layout: post
category: blog
---
Recently at [work][1] I had to code (rather, re-code) a feature table for our [Shopping][2] service. 

We used images to denote the availability of features for different packages, adding them via a CSS `background` rule to all relevant table cells. The CSS code was initially like this:

<pre name="code" class="css">.available {
   background: url("img/tick.gif") no-repeat;
   background-position: 50% 50%;
}
</pre>

A simple `&mdash;` was used for cells that denoted that the feature is not available for the particular package. 

All fine and dandy, but my problem was that upon printing, the browser dismissed the background image of the &#8220;available&#8221; cells, printing them completely empty.

Initially, all &#8220;available&#8221; cells contained a non-breaking space, so I decided to change the emptiness to something more semantic, like `YES`, hiding it in the normal, screen CSS with some `text-indent` magic. Then I could use the print CSS to zero out the text-indent and bring the semantic text back to viewport, now that the background-image has been dismissed.

The whole trick is like that:

<pre name="code" class="xml"><table>
  <tr>
    <td class="available">
      YES
    </td>
       
  </tr>
  
</table>
</pre>

<pre name="code" class="css">.available {
   background: url("img/tick.gif") no-repeat;
   background-position: 50% 50%;
   text-indent: -9999em;
}

@media print {
   .available { 
       text-indent: 0;
       background-image: none;
   }
}
</pre>

Now the browser will show the tick images on screen, but will lose them upon printing, replacing them with the text that you put in your table cells.

We threw some background in there to avoid printing the background image anyway, just in case the browser wants to play tough.

A simple, effective tip when you don&#8217;t want to use inline images (ticks and x&#8217;es) to tables but want to keep the semantic value of the symbol in all media.

 [1]: http://www.phaistosnetworks.gr
 [2]: http://shopping.pathfinder.gr
