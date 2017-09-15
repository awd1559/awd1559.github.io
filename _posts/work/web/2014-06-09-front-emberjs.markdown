---
layout:     post
title:      "emberjs"
subtitle:   " \"web front emberjs\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: web
permalink: /web/emberjs
tags:
    - web
---
> - [web front目录](/web/front)





# [emberjs](http://emberjs.com/)
- [source code on github](https://github.com/emberjs/ember.js)
- [addons](emberaddons.com)

#### update ember

```
npm uninstall -g ember-cli
npm cache clean
bower cache clean
npm install -g ember-cli
```


```
// new project
ember new [name]


// run it
ember serve
ember s
localhost:4200 


ember g route about
app/routes/about.js
export default Ember.Route.extend({
  model() {
    return [];
  }
});

ember g model person
app/models/person.js
import Model from 'ember-data/model';
import attr from 'ember-data/attr';
export default Model.extend({
    title:attr(),
    owner::attr(),
    city:attr(),
    type:attr(),
    iamge:attr(),
    bedrooms:attr()
});

in route/index.js model() 
return this.store.findAll('person');


ember g controller [name]



ember g component listing

```


//hbs template

```
{{ #each model as |a| }}
 {{ a }}
{{ /each }}

{{ #link-to 'about' class="button" }}
{{ /link-to }}
```


#### plugins

```
ember install ember-cli-template-lint
powed by ember-template-lint
.template-lintrc.js
    bare-strings
    block-indentation
    html-comments
    triple-curlies
    nested-interactive
    self-closing-void-elements
    img-alt-attributes
    invalid-interactive



ember install ember-cli-flash

template:
<button {{action "save"}}>Hide Body</button>

{{#each flashMessages.queue as |flash|}}
  {{flash-message flash=flash}}
{{/each}}

controller:
actions: {
save: function () {
    const flashMessages = Ember.get(this, 'flashMessages');
        flashMessages.success('Successfully saved!');
    }
}



ember install ember-cli-mirage
client side Http server to send fake json data to browser



ember install ember-infinity

ember install ember-responsive
app/breakpoints.js

controller:
this.get('media.isMobile'); 

template:
{{#if media.isDesktop}}
  Desktop view!
{{/if}}


ember install ember-composable-helpers


ember install ember-browserify
npm install --save-dev my-cool-module

import MyCoolModule from "npm:my-cool-module";
```



