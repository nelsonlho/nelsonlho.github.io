---
---

### Factory vs Service in AngularJS

This seems to be an on going discussion in the AngularJS community:  What is the difference between a factory and a service, and when should either one be used?

Cynics from the ReactJS community will simply reply, "That's why in React, there is only one way to do most of the things."  

### Quick Example

Consider the example 'Hello World' as stated below:

{% highlight bash %}
var myApp = angular.module('myApp', []);

//service, a simpler
myApp.service('helloWorldFromService', function() {
    this.sayHello = function() {
        return "Hello, World!";
    };
});

//factory, more complicated
myApp.factory('helloWorldFromFactory', function() {
    return {
        sayHello: function() {
            return "Hello, World!";
        }
    };
});

{% endhighlight %}

You may not see much of a difference here, since factory and function can do pretty much the same stuff.  However, since in services we need to use the `this` keyword, we will need to instantiate a new class object.  In factories, however, we only need to get the returned values.

### For the Sake of Consistency, Use Factories

The AngularJS community prefers factories, so therefore we will find many more answers on StackOverflow related to factories than to services.  In fact, [John Papa's guide](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#factories) clearly states that factories should be used since a services are too similar to them.

---

Copyright &copy; [Nelson Ho](http://www.github.com/nelsonlho).
