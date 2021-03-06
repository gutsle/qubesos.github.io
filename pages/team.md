---
layout: default
title: Team
permalink: /team/
redirect_from:
- /people/
- /doc/QubesDevelopers/
- /wiki/QubesDevelopers/
---

<div id="team-core" class="more-top">
  {% assign core_count = 0 %}
  {% assign maintainers_count = 0 %}
  {% assign emeritus_count = 0 %}
  {% for team in site.data.team %}
  {% if team.type == "core" %}
  {% assign core_count = core_count | plus:1 %}
  <div class="row team team-core">
    <div class="col-lg-2 col-md-2 col-sm-5 col-xs-12 text-center">
    <div class="picture more-bottom">
      {% if team.picture %}
      <img src="/attachment/site/{{team.picture}}" title="Picture of {{team.name}}">
      {% else %}
      <i class="fa fa-user"></i>
      {% endif %}
    </div>
    </div>
    <div class="col-lg-4 col-md-4 col-sm-7 col-xs-12">
      {% assign name_array = team.name | split:" " %}
      <h4 class="half-bottom">{{team.name}}</h4>
      <em class="role half-bottom">{{team.role}}</em>
      <a href="mailto:{{team.email}}" class="add-right"><i class="fa fa-envelope"></i> Email</a>
      {% if team.website %}
      <a href="{{team.website}}" class="add-right" target="blank"><i class="fa fa-link"></i> Website</a>
      {% endif %}
      {% if team.twitter %}
      <a href="https://twitter.com/{{team.twitter}}" target="blank"><i class="fa fa-twitter"></i> Twitter</a>
      {% endif %}
    </div>
    <div class="col-lg-6 col-md-6 col-sm-12 col-xs-12 text-center">
      {% if team.fingerprint %}
      <span class="fingerprint" title="{{team.name}}'s PGP Encryption Key Fingerprint">{{team.fingerprint}}</span>
      {% endif %}
      {% if team.pgp_key %}
      <a href="{{team.pgp_key}}"><i class="fa fa-key"></i> Get {{name_array[0]}}'s PGP Encryption Key</a>
      {% endif %}
    </div>
  </div>
  {% endif %}
  {% endfor %}
</div>
<hr class="more-bottom">
<div class="row team more-top more-bottom">
  <div class="col-lg-12 col-md-12 col-sm-12">
    <h2 class="text-center">Emeritus</h2>
    {% for team in site.data.team %}
    {% if team.type == "emeritus" %}
    {% assign emeritus_count = emeritus_count | plus:1 %}
    {% include team-simple.html %}
    {% endif %}
    {% endfor %}
  </div>
</div>
<hr class="more-bottom">
<div class="row team">
  <div class="col-lg-12 col-md-12 col-sm-12">
    <h2 class="text-center more-bottom">Community Contributors</h2>
    <p>Qubes would not be where it is today without the input of the many users, testers, and developers of all skill levels who have come together to form this thriving community. The community's discussions take place primarily on the <a href="/doc/mailing-lists/">Qubes mailing lists</a>.</p>
  </div>
</div>
{% assign non_community_count =  core_count | plus:maintainers_count | plus:emeritus_count %}
{% assign community_count =  site.data.team | size | minus:non_community_count %}
{% assign community_half = community_count | divided_by:2 | plus:1 %}
{% assign community_shown =  0 %}

<div class="row team">
  <div class="col-lg-6 col-md-6 col-sm-6 col-xs-12">
    {% for team in site.data.team %}
    {% if team.type == "community" %}
    {% if community_shown < community_half %}
    {% include team-simple.html %}
    {% elsif community_shown == community_half %}
    </div>
    <div class="col-lg-6 col-md-6 col-sm-6 col-xs-12">
    {% include team-simple.html %}
    {% else %}
    {% include team-simple.html %}
    {% endif %}
    {% assign community_shown = community_shown | plus:1 %}
    {% endif %}
    {% endfor %}
  </div>
</div>
