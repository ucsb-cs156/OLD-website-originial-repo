---
title: Head First Java, 2nd Edition
layout: default
desc: Main textbook for learning Java
custom_sort_order: 1
used_this_quarter: true
---


Head First Java, 2nd Edition is a *very old* book; it came out in 2005 and introduced the new *Java version 5*.  

Two notes:
* In spite of how old it is, it still holds up as one of the best introduction to some of the most confusing aspects of Java.
* Finally at long last, a new version, [Head First Java 3rd edition](/textbooks/HFJ3), is coming out that will cover Java 17.  It's being released a little bit at a time; as of March 2022, just five chapters were available.

{% include read_hfj_online.html %}

<div id="chapters" data-role="collapsible" data-collapsed="false">
  <h2>Reading Notes, by Chapter</h2>
    <ul>
      {% assign hfj_chapters = site.hfj | sort: 'sort_key' %}
      {% for chapter in hfj_chapters %}
         <li><a href="{{chapter.url}}">Chapter {{chapter.chapter}}</a>&mdash;{{chapter.desc}}</li>
      {% endfor %}
    </ul>
</div>


Other chapters may be available here:  <https://foo.cs.ucsb.edu/56wiki/index.php/HFJ>
