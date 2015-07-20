---
layout: post
title:  "Backbone Events"
categories: UI
---

This is a quick write up of some Backbone Model basics to test the blog.

{% highlight javascript %}
var Student = Backbone.Model.extend({
  defaults: {
    id: null,
    classes: [ "Art", "Math", "English" ]
  },
  initialize: () => {
    // set up any behaviours here.
    this.on('summerVacation', this.resetClasses );
  },
  resetClasses: () => this.set( "classes", [] )
});
{% endhighlight %}

We can now trigger events on our students to get the expected behaviour.

{% highlight javascript %}
var sally = new Student({ name: "Sally" });
console.log( sally.get('classes') ); //=> ["Art", "Math", "English"]
sally.trigger( "summerVacation" );
console.log( sally.get('classes') ); //=> []
{% endhighlight %}

It even works across collections!

{% highlight javascript %}
var Class = Backbone.Collection.extend({
  model: Student
});

var artClass = new Class([
  new Student({ name: "Sally" }),
  new Student({ name: "Bobby" }),
  new Student({ name: "Pat" })
]);

// Check all the students
artClass.trigger( "summerVacation" );
artClass.pluck('classes');
//=> [ [], [], [] ]
{% endhighlight %}
