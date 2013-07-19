# RoundingWell Code Style Guide

*A mostly reasonable approach to code style*

Taken from: airbnb, kohana


## <a name='TOC'>Table of Contents</a>

  1. [Spacing & Tabbing](#whitespace)  
  1. [Blocking](#blocking)
  1. [Comments](#comments)
  1. [Naming Conventions](#naming-conventions)
  1. [Strings](#strings)
  1. [Arrays](#arrays)
  1. [Conditionals](#conditionals)
  1. [Logic Flow](#logicflow)
 
## <a name='whitespace'>Spacing & Tabbing</a>

  - **Indentation**: Indent blocks are 4 spaces. Use of the tab key should be translated to this. This helps to avoid problems with diffs and tab/spacing blends not formatting properly in IDEs.

    ```php
    if ($istrue) {
        print "it's true!";
    }
    ```
    
  - **Align Equals**: When dealing with several rows of assignments or array specification, align the equals sign (within reason)

    ```php
    // bad
    $this = "that";
    $another_var = "another"
    $really_long_variable = "this other string";
    $settings = array(
        "one" => 1,
        "fourteen" => 14,
        "twenty-one hundred" => 2100,
    );
    
    // good
    $this            = "that";
    $another_var     = "another"
    $really_long_var = "this other string";
    $absurdly_long_and_itd_be_silly_to_align_with_me = "hello";
    $settings = array(
        "one"                => 1,
        "fourteen"           => 14,
        "twenty-one hundred" => 2100,
    );
    ```
   
  - **Leading Braces**: Place 1 space before the leading brace.

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
    
  - **Long Method Chains**: Use indentation when making long method chains.

    javascript:
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
    
    php:
    ```php
    // bad
    $rows = $this->where('dob', '=',$patient['dob'])->and_where('lower_first_name','=',$patient['lower_first_name'])->and_where('lower_last_name', '=',$patient['lower_last_name'])->find_all();

    // good
    $rows = $this->where('dob', '=',$patient['dob'])
                 ->and_where('lower_first_name','=',$patient['lower_first_name'])
                 ->and_where('lower_last_name', '=',$patient['lower_last_name'])
                 ->find_all();

    ```    

    **[[⬆]](#TOC)**

## <a name='blocking'>Blocking</a>
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

    // bad
    function() { return false; }

    // good
    function() {
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

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

  - Use `// TODO:` to annotate solutions to problems

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
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
    
  - **Wrapping Conditionals**: When the conditional is super long, wrap to the next line, beginning with the logical operator

    ```php
    // bad
    if (!isset($this->current_risks[$risk_id]) && isset($this->closed_risks[$risk_id]) && $this->closed_risks[$risk_id]['closed'] >= $hit['latest_ts']) {
        // ...stuff...
    }

    // good
    if (!isset($this->current_risks[$risk_id]) && isset($this->closed_risks[$risk_id]) 
        && $this->closed_risks[$risk_id]['closed'] >= $hit['latest_ts']) {
        // ...stuff...
    }
    ```

    **[[⬆]](#TOC)**


