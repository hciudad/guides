# RoundingWell Code Style Guide

*A mostly reasonable approach to code style*

Taken from style guides for: airbnb, kohana, pear


## <a name='TOC'>Table of Contents</a>

  1. [Spacing](#whitespace)  
  1. [Braces](#braces)
  1. [Comments](#comments)
  1. [Naming Conventions](#naming-conventions)
  1. [Strings](#strings)
  1. [Conditionals](#conditionals)
  1. [Best Practices](#best-practices)
 
## <a name='whitespace'>Spacing</a>

  - **Indentation is 4 spaces**: Indent blocks are 4 spaces. Use of the tab key should be translated to this. This helps to avoid problems with diffs and tab/spacing blends not formatting properly in IDEs.

    ```php
    if ($istrue) {
        print "it's true!";
    }
    ```
    
  - **Align Similar Blocks**: When dealing with repetitive assignments/blocks, align values where reasonable to support readability.

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
   
  - **Long Method Chains are Wrapped and Indented**: Use line breaks and indentation when making long method chains.

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

  - **Spacing Before Opening Parenthesis**: 

    When the parenthesis opens a control structure (if/else/while/for/etc), preceed with a space.
    ```php
    // bad
    if(test) return false;
    
    // good
    if (test) return false;
    ```
    
    When the parenthesis is part of a function call, don't add any spaces.
    ```php
    // bad
    my_function ();
    
    // good
    my_function();
    ```
    

  - **1 Space Before Leading Braces**: Place 1 space before the leading brace.

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
  - **Use [K&R Style](http://en.wikipedia.org/wiki/Indent_style#K.26R_style) for bracketing functions**
  
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
  - **Use `/** ... */` for multiline docblock style comments**. Inner lines begin with `*`
  - **Use `//` for single line comments**
   
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

    **[[⬆]](#TOC)**


## <a name='naming-conventions'>Naming Conventions</a>

  - **Avoid single letter names.** Be descriptive with your naming.
  - **Use Lowercase snake_case for Variables and Functions**
  - **Class File Names and Directories are Lower Case**
  - **Class names should be like Path_To_ClassName**
  - **Example:**

    Assuming a class exists in:
    ```
    /classes
        /animals
            tigercub.php
    ```
    

    ```php
    // bad
    class cub
    {
        public $FoodOptions = array('fish','people');
        protected $paws = 4;
        
        function f() 
        {
            return $this->FoodOptions;
        }
        
        function Growl() 
        {
            print "rawwwr";
        }
    }


    // good
    class Animals_TigerCub
    {
        public $food_options = array('fish','people');
        protected $_paws = 4;
        
        function get_food() 
        {
            return $this->food_options;
        }
        
        function growl() 
        {
            print "rawwwr";
        }
    }
    ```

    **[[⬆]](#TOC)**


## <a name='strings'>Strings</a>

  - **Use Single Quotes Where Possible** `''` for strings that don't require interpolation

    ```php
    // bad
    $name = "Bob Parr";

    // good
    $name = 'Bob Parr';
    ```

  - **Use Double Quotes When Necessary** `""` for strings that require interpolation. Vars are embedded in the string.
    
    ```php
    // bad
    $string = 'My name is ' . $name . "\n and you are at " . $this->location;

    // good
    $string = "My name is $name\n and you are at {$this->location}\n";
    ```
    
## <a name='conditionals'>Conditionals</a>
  - **Understand when to use `===` and `!==` vs `==` and `!=`.**

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

## <a name='best-practices'>Best Practices</a>
  - **Return Early**: It'd be best to bail out of a function early rather than wrap main logic in a large if statement.
  
  ```php
  // bad
  function test($string) {
      if (is_string($string)) {
          // .... 
          // lots
          // of
          // stuff
          // going
          // on
          return true;
      } 
      else {
          return false;
      }
  }

  // good
  function test($string) {
      if (!is_string($string)) return false;
      
      // .... 
      // lots
      // of
      // stuff
      // going
      // on
      return true;
  }
  ```
  
  
  - **Use `// FIXME:` to annotate problems**

    ```php
      // FIXME: shouldn't use a global here
      if ($global_var) print 'hello';
    ```

  - **Use `// TODO:` to annotate solutions to problems**

    ```php
      // TODO: max should be configurable
      for ($i=0; $i<5; $i++) print 'hello';
    ```
    
  **[[⬆]](#TOC)**

