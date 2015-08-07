# XTube Frontend Style Guide() {
## Table of Contents

  1. [Naming Conventions](#naming)
  2. [Accessors](#accessors)
  3. [Events](#events)
  3. [jQuery](#jquery)

## Naming Conventions
- [1.1](#1.1) <a name='1.1'></a> Use camelCase when naming class or id selectors.

    ```html
    <!-- bad -->
    <div class="first-class second_class" id="my-div"></div>

    <!-- good -->
    <div class="firstClass secondClass" id="myDiv"></div>
    ```

- [1.2](#1.2) <a name='1.2'></a> Use camelCase when naming objects, functions, and instances.

    ```javascript
    // bad
    var thisismystring = '';
    const this_is_my_object = {};
    function c() {}

    // good
    var thisIsMyString = '';
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

- [1.3](#1.3) <a name='1.2'></a> Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - [1.4](#1.4) <a name='1.3'></a> Use PascalCase when naming constructors or classes.

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // good
    var User = function() {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User();
    ```

  - [1.5](#1.5) <a name='1.5'></a> Use different selectors for css and javascript.

    ```html
    <!-- bad -->
    <div class="classSelector" id="idSelector"></div>

    <!-- good -->
    <div class="classCssSelector classJavascriptSelector" id="classJavascriptSelector"></div>
    ```


  - [1.6](#1.6) <a name='1.6'></a> Don't use id selectors for CSS.

    ```html
    <!-- bad -->
    <div id="idCSSSelector"></div>

    <!-- good -->
    <div class="classCssSelector"></div>
    ```
- [1.6](#1.6) <a name='1.6'></a> If your file exports a single class, your filename should be exactly the name of the class.
    ```javascript
    // file contents
    var CheckBox = function(){
      // ...
    }

    // in some other file
    // bad
    './checkBox.js';

    // bad
    './check_box.js';

    // good
    './CheckBox.js';
    ```

    **[⬆ back to top](#table-of-contents)**


    ## Accessors

      - [1.1](#1.1) <a name='1.1'></a> Accessor functions for properties are not required.
      - [1.2](#1.2) <a name='1.2'></a> If you do make accessor functions use getVal() and setVal('hello').

        ```javascript
        // bad
        dragon.age();

        // good
        dragon.getAge();
        ///////////////////////////////
        // bad
        dragon.age(4);

        // good
        dragon.setAge(4);
        ```

      - [1.3](#1.3) <a name='1.3'></a> If the property is a `boolean`, use `isVal()` or `hasVal()`.

        ```javascript
        // bad
        if (!dragon.age()) {
          return false;
        }

        // good
        if (!dragon.hasAge()) {
          return false;
        }
        ```

      - [1.4](#1.4) <a name='1.4'></a> Create get() and set() functions.

        ```javascript
        var Jedi = function() {
          var bla = 'blubb';

          setBla(val) {
            bla = val;
          }

          getBla() {
            return bla;
          }
        }
        ```

  **[⬆ back to top](#table-of-contents)**

## Events

  - [3.1](#3.1) <a name='3.1'></a> When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```javascript
    // bad
    $(this).bind('click', function(e) {
      // do something
    });
    ```

    prefer:

    ```javascript
    // good
    $(this).on('listingUpdated', function(e) {
      // do something
    });
    ```

  **[⬆ back to top](#table-of-contents)**

  ## jQuery

    - [4.1](#4.1) <a name='4.1'></a> Use as less as possible jQuery.

      ```javascript
      // bad
      var users = ['user1', 'user2'];
      $.each(users, function(index, user) {
        // do something with user
      });

      // bad
      var userName = $('#selector').html();

      // bad
      $('#selector').html('<h1>User</h1>');

      // bad
      $('#selector').addClass('active');

      // good
      var userName = document.getElementById('selector').innerHTML;

      // good
      document.getElementById('selector').innerHTML = '<h1>User</h1>';

      // good
      document.getElementById('selector').className += ' active';

      //good
      var users = ['user1', 'user2'],
      i = 0, l = users.length;
      for(; i<l; i++) {
        var user = users[i];
        // do something with user
      }
      ```

    - [4.2](#4.2) <a name='4.2'></a> Prefix jQuery object variables with a `$`.

      ```javascript
      // bad
      const sidebar = $('.sidebar');

      // good
      const $sidebar = $('.sidebar');
      ```

    - [4.3](#4.3) <a name='4.3'></a> Cache jQuery lookups.

      ```javascript
      // bad
      function setSidebar() {
        $('.sidebar').hide();

        // ...stuff...

        $('.sidebar').css({
          'background-color': 'pink'
        });
      }

      // good
      function setSidebar() {
        var $sidebar = $('.sidebar');
        $sidebar.hide();

        // ...stuff...

        $sidebar.css({
          'background-color': 'pink'
        });
      }
      ```

    - [4.4](#4.4) <a name='4.4'></a> For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
    - [4.5](#4.5) <a name='4.5'></a> Use `find` with scoped jQuery object queries.

      ```javascript
      // bad
      $('ul', '.sidebar').hide();

      // bad
      $('.sidebar').find('ul').hide();

      // good
      $('.sidebar ul').hide();

      // good
      $('.sidebar > ul').hide();

      // good
      $sidebar.find('ul').hide();
      ```

  **[⬆ back to top](#table-of-contents)**

}