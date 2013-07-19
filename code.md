# RoundingWell Code Style Guide

*A mostly reasonable approach to code style*

Taken from: airbnb, kohana


## <a name='TOC'>Table of Contents</a>

  1. [Spacing](#whitespace)  
  1. [Braces](#braces)
  1. [Comments](#comments)
  1. [Naming Conventions](#naming-conventions)
  1. [Strings](#strings)
  1. [Arrays](#arrays)
  1. [Conditionals](#conditionals)
  1. [Logic Flow](#logicflow)
 
## <a name='whitespace'>Spacing</a>

  - **Indentation**: Indent blocks are 4 spaces. Use of the tab key should be translated to this. This helps to avoid problems with diffs and tab/spacing blends not formatting properly in IDEs.

    ```php
    if ($istrue) {
        print "it's true!";
    }
    ```
    
  - **Align Equals**: When dealing with repetitive assignments, align the assignments where reasonable to support readability.

    ```php
    // bad
    $what = "that";
    $another_var = "another"
    $really_long_variable = "this other string";
    $settings = array(
        "one" => 1,
        "fourteen" => 14,
        "twenty-one hundred" => 2100,
    );
    $user->setConfig('sms_phone_number', '615-123-1234', true);
    $user->setConfig('notify_on_alert', 'this@that.com', true);
    $user->setConfig('is_admin', 'y', false);
    $user->setConfig('debug_level', 'high', true);
    $user->setConfig('sms_phone_number', '615-123-1234', true);
    
    
    // good
    $what            = "that";
    $another_var     = "another"
    $really_long_var = "this other string";
    $absurdly_long_and_itd_be_silly_to_align_with_me = "hello";
    $settings = array(
        "one"                => 1,
        "fourteen"           => 14,
        "twenty-one hundred" => 2100,
    );
    $user->setConfig('sms_phone_number', '615-123-1234',  true);
    $user->setConfig('notify_on_alert',  'this@that.com', true);
    $user->setConfig('is_admin',         'y',             false);
    $user->setConfig('debug_level',      'high',          true);
    $user->setConfig('sms_phone_number', '615-123-1234',  true);
    ```
   
  - **Long Method Chains**: Use indentation when making long method chains.

    javascript (subsequent lines are appropriately indented, beginning with '.'):
    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();
    ```
    
    php (subsequent lines are indented and begin with '->'):
    ```php
    // bad
    $rows = $this->where('dob', '=',$patient['dob'])->and_where('lower_first_name','=',$patient['lower_first_name'])->and_where('lower_last_name', '=',$patient['lower_last_name'])->find_all();

    // good
    $rows = $this->where('dob', '=',$patient['dob'])
        ->and_where('lower_first_name','=',$patient['lower_first_name'])
        ->and_where('lower_last_name', '=',$patient['lower_last_name'])
        ->find_all();

    ```    

  - **Spacing Before Parenthesis**: 

    When the parenthesis is to wrap a conditional, preceed with a space
    ```php
    // bad
    if(test) return false;
    
    // good
    if (test) return false;
    ```
    
    When the parenthesis is part of a function call, don't add any spaces
    ```php
    // bad
    my_function ();
    
    // good
    my_function();
    ```
    

  - **Space Before Leading Braces**: Place 1 space before the leading brace.

    ```php
    // bad
    function test(){
      // ...
    }

    // good
    function test() {
      // ...
    }
    ```
    
    **[[⬆]](#TOC)**

## <a name='braces'>Braces</a>
  - **Use [K&R Style](http://en.wikipedia.org/wiki/Indent_style#K.26R_style) for bracketing**
  
  - **Use braces with all multi-line blocks**

    ```php
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }
    ```

    **[[⬆]](#TOC)**


## <a name='comments'>Comments</a>
  - Use `/** ... */` for multiline docblock style comments. Inner lines begin with `*`
  - Use `//` for single line comments
   
    ```php
    // bad
    // sayhello() says hello to the given 
    // name and returns true if successful.
    //
    // @param <String> name
    // @return <Boolean> printed
    function sayhello($name) {
        
        /** say hello to my user **/
        print "hello, $name";
        
        return true;
    }

    // good
    /**
     * sayhello() says hello to the given
     * name and returns true if successful.
     *
     * @param <String> name
     * @return <Boolean> printed
     */
    function sayhello($name) {

        // say hello to my user
        print "hello, $name";
        
        return true;
    }
    ```

  - Use `// FIXME:` to annotate problems

    ```php
      // FIXME: shouldn't use a global here
      if ($global_var) print 'hello';
    ```

  - Use `// TODO:` to annotate solutions to problems

    ```php
      // TODO: max should be configurable
      for ($i=0; $i<5; $i++) print 'hello';
    ```

    **[[⬆]](#TOC)**


## <a name='naming-conventions'>Naming Conventions</a>

  - Avoid single letter names. Be descriptive with your naming.

    ```php
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - **Use lowercase snake_case** when naming variables and functions

    javascript:
    ```javascript
    // bad
    var OBJEcttsssss = {};
    var thisIsMyObject = {};
    var this-is-my-object = {};
    function c() {};


    // good
    var this_is_my_object = {};
    function this_is_my_function() {};
    ```

    php:
    ```php
    // bad
    $LotsOfThings = '';
    
    // good
    $lots_of_things = '';
    ```
    
  - **Class names should be Path_To_ClassName** for class definition. All class files are named lowercase, and their directory path from the root class directory is part of the class name. 

    A class that exists in:
    ```
    /classes
        /animals
            tigercub.php
    ```
    
    Should be named **Animals_TigerCub**
    
    
    **[[⬆]](#TOC)**

  - **Protected or private class variables are underscore prefixed**

    ```php
    // bad
    protected $length;
    
    // good
    protected $_length;
    ```
    
  - **Constants are all uppercase snake_case**

    ```php
    // bad
    define('MyFlag',1);
    define('my_flag',1);
    
    // good
    define('MY_FLAG',1);
    ```
  
    
    **[[⬆]](#TOC)**


## <a name='strings'>Strings</a>

  - **Use single quotes** `''` for strings that don't require interpolation

    ```php
    // bad
    $name = "Bob Parr";

    // good
    $name = 'Bob Parr';
    ```

  - **Use double quotes** `""` for strings that require interpolation. Vars are embedded in the string.
    
    ```php
    // bad
    $string = 'My name is ' . $name . "\n and you are at " . $this->location;

    // good
    $string = "My name is $name\n and you are at {$this->location}\n";
    ```
    
## <a name='conditionals'>Conditionals</a>
  - **Use `===` and `!==` over `==` and `!=`.**

  - **Use Shortcuts**: 
  
    ```php
    // bad
    if (name !== '') {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (count($items) > 0) {
      // ...stuff...
    }

    // good
    if (count($items)) {
      // ...stuff...
    }
    ```
    
  - **Wrapping Conditionals**: When the conditional is super long, wrap to the next line, beginning with the logical operator. Opening brace goes on a line by itself.

    ```php
    // bad
    if ((condition1
         || condition2)
        && condition3
        && condition4) 
    {
        // ... stuff
    }
    ```

    For very complex conditionals, it may be better to break the conditional down. 
    ```php
    $is_this = (condition1 || condition2);
    $is_that = (condition3 && condition4);
    if ($is_this || $is_that) {
        // ....
    }
    ```

  - **Trenary**: Fine for use, but keep it simple.

  ```php
  // all good
  $foo = ($a == $b) ? $a : $b;
  $foo = $a ? $a : $b;

  // complex statements can be broken across lines
  $foo = ($condition1 == $condition2)
       ? $positive_result
       : $negative_result;
  ```

  Avoid use when casting can solve the problem:
  ```php
  // bad
  $flag = ($f == TRUE) ? TRUE : FALSE;
  
  // good
  $flag = (bool) $f;
  ```

  **[[⬆]](#TOC)**


