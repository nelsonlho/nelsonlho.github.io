---
---

### Four Types of AngularJS Directive Restrictions

Many of those who use AngularJS may not realize that they have been using directives; `ng-app` and `ng-controller` are amongst the most commonly used Angular directives.  Developers may also write their own directives.  The benefit of having your own defined directives, other than eliminating redundancy by having reusable code, is that designers and other team members not familiar with JavaScript at all will have little difficulty understand what a well-named directive is for.

This article will quickly guide you through the four types of restrictions.

### Attribute

By default, your own defined directive will have an attribute restriction.  

{% highlight bash %}
var app = angular.module("BookApp", []).run(function($rootScope) {
    $rootScope.books = ["1984", "A Tale of Two Cities", "A Brave New World"];
});

app.controller("BookCtrl", function( $scope, $rootScope) {
  $scope.books = $rootScope.books;

});

app.controller("FirstBookCtrl", function($scope, $rootScope) {
  $scope.firstBook = $rootScope.books[0];
});
{% endhighlight %}

And on your view, put the following:

{% highlight bash %}
<div ng-app="BookApp" ng-controller="BookCtrl">
  <ul ng-repeat="book in books">
    <li>{{book}}</li>
  </ul>
  <div class="first-book" ng-controller="FirstBookCtrl">
    Book: {{firstBook}}
  </div>
</div>
{% endhighlight %}

Check out the code [here](http://codepen.io/nelsonlho/pen/NNjNwo)

Basically, both the `BookCtrl` and `FirstBookCtrl` have access to the `$rootScope`, which contains all of the books chosen, however `BookCtrl` shows all of these books while `FirstBookCtrl` only shows the first.

You may wonder why we would need another way of sharing between controllers.  However, be reminded that in a complicated application, many controllers will have access to the same `$rootScope`.  Giving other controllers to change what every controller may be dependent on may simply not be a good practice.

The same idea may go to other child/parent scope relationships, while children may have access to their parents' scopes.  What if you want to take away the ability for these controllers to alter the information that many other parts of your application may need to share?

### Using A Factory Service

Another way is to use a factory to create a singleton object.  You will need to alter your Angular code as follows:

{% highlight text %}
var app = angular.module("BookApp", []);

app.factory("BookService", function() {
  var books = ["1984", "A Tale of Two Cities", "A Brave New World"];

  return {
    all: function() {
      return books;
    },
    first: function() {
      return books[0];
    }
  };
});

app.controller("BookCtrl", function($scope, BookService) {
  $scope.books = BookService.all();
});

app.controller("FirstBookCtrl", function($scope, BookService) {
  $scope.firstBook = BookService.first();
});
{% endhighlight %}

View the code [here](http://codepen.io/nelsonlho/pen/pydqrJ).

Voila!  You will still see the same results in your view.



---

Copyright &copy; [Nelson Ho](http://www.github.com/nelsonlho).
