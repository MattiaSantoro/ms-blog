---
title: "Contact"
layout: single
sitemap: true
permalink: /contact/
author_profile: true
---

<!-- 
<p>You can reach me via email: <br><strong><em><a href="mailto:hi@matsan.it">hi@matsan.it</a></em></strong></p>
 -->

<style>
  .email-revealer::after {
    content: "\68\69" "\40" "\6d\61\74\73\61\6e\2e\69\74";
  }
</style>

<p>
  You can reach me via email: <br>
  <strong>
    <em>
      {% include secure-email.html 
         user="hi" 
         domain="matsan.it" 
         text='<span class="email-revealer"></span>' 
      %}
    </em>
  </strong>
</p>