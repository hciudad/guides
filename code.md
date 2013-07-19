# RoundingWell JavaScript Style Guide() {

*A mostly reasonable approach to code style*


## <a name='TOC'>Table of Contents</a>

  1. [Spacing & Tabbing](#whitespace)
  1. [Logic Flow](#logicflow)
  1. [Conditionals](#conditionals)


## <a name='whitespace'>Spacing & Tabbing</a>
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
    
  - **Block Indentation**: Indent blocks are 4 spaces. Use of the tab key should be translated to this.

    ```php
    if ($istrue) {
        print "it's true!";
    }
    ```
    
    **[[⬆]](#TOC)**

## <a name='conditionals'>Conditionals</a>
  - **Wrapping Conditionals**: When the conditional is cumbersomely long, wrap to the next line, beginning with the logical operator

    ```php
    // bad
    if (!isset($this->current_risks[$risk_id]) && isset($this->closed_risks[$risk_id]) && $this->closed_risks[$risk_id]['closed'] >= $hit['latest_ts']) {
        ...
    }

    // good
    if (!isset($this->current_risks[$risk_id]) && isset($this->closed_risks[$risk_id]) 
        && $this->closed_risks[$risk_id]['closed'] >= $hit['latest_ts']) {
        ...
    }

    **[[⬆]](#TOC)**
