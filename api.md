# API Guide

## <a name='TOC'>Table of Contents</a>

Basics:
  1. [Urls](#urls)  
  1. [Validation](#validation)
  1. [Errors](#errors)


More Detail:
  1. [Where API Calls Go](#api-location)  
  1. [Standard Calls](#standard-calls)  
  1. [Standard Response](#standard-response)  
  1. [API Parameters](#api-parameters)  

PHI: 
  1. [Decryption](#decryption)
  1. [You Decrypt it You Log it](#decrypt-and-log)

Performance:
  1. [ORM vs DB Queries](#orm-vs-db)



## <a name='urls'>Urls</a>

  - **API urls should be descriptive for readability and so apache logs stay informative**

  Bad: gateway/get (xdata: {model: user, id: 1})

  Good: user/get/1

## <a name='validation'>Validation</a>

  - **There should be one consistent place to see/adjust requirements for api input. Input is checked before any other work is done**

  Bad: rules sprinkled throughout controllers and models.

  Bad: rules **only** enforced on save actions of models (additional model checks are fine, but should not be first line)
  

  Good example: all rules for an api call are defined in classes/validation/{controller name}.php Those rules are checked before the controller begins to work.

## <a name='errors'>Errors</a>

  - **ALL errors should be of a consistent format, using proper response codes, with actionable detail in the body.**

  Bad response: '' (status code 200)

  Bad response: '' (status code 500)

  Bad response: operation failed (status code 400)

  Bad response: last name cannot be empty (status code 400)
  
  
  Good response: {last_name: "not empty", first_name: "not empty"} (status code 400)

  Good response: {id: "not found"} (status code 404)
 

## <a name='api-location'>Where API Calls Go</a>

Occassionally it isn't so obvious which controller an api should reside in. Rule of thumb: what is the core object you 
are returning? That's the controller it goes in, and everything else is an embedded object. 

An example: you need to write a new API that returns all the inbox entries a clinician has. Inbox entries are really 
just glue that pulls together an interaction on a risk, the user that wrote it, and the patient it relates to. It may 
be tempting to put this on the interaction api, but the core of what you are getting is an inbox entry. It goes in
an inbox controller, and the core object it returns is a list of inbox entries. The interaction,patient,etc are all 
embedded within their entry. 

## <a name='standard-calls'>Standard Calls</a>

  - **{object}/get/{id}**: Returns an item along with any embedded dependencies. 
  
  - **{object}/getby?filter1=a&filter2=b**: Returns an array of items of identical structure to what /get returns. This call typically accepts filters. Occassionally the filter is a list of ids - in this case the filter parameter should be passed by post to prevent hitting a max for GET length.

  - **{object}/all**: Typically an alias for /getby without filters.

  - **{object}/create**: Creates a new object. The return of this api should be the same as if you had called /get for the new object.

  - **{object}/update/{id}**: Updates an existing object. The return of this api should be the same as if you had called /get for the object.

  - **{object}/archive/{id}**: Indicates a soft delete of an object. Returns integer 1 if successful.

  - **{object}/delete/{id}**: True delete of an object. Returns integer 1 if successful.

Other api calls exist when the standard set cannot satisfy. 


## <a name='standard-response'>Standard Response</a>

Current style: A json object is returned, blending object fields and any additional meta or relationships. 

Future: 
* All objects returned should be true json representations of that object's non phi fields. 
* PHI fields are included only when necessary or specifically requested. 
* Objects can be embedded within their referencing parent object via the _related or _related_collections attribute.
* Any json encoded attributes should be decoded into hash form (json_decode($item, true)).
* Any calculated field (next checkin date, days since discharge, etc) should be returned in a _meta attribute, not mixed in with model fields

Example for a call to get response answers for a checkin (has a json attribute, no embedded objects, no phi):

```php
[
  {
    "id":98,
    "response_id":372,
    "content_id":null,
    "message_id":4,
    "content_type":"message",
    "content_json":"{\"label\":\"A message from Man Ager:\",\"body\":\"Here's me message\",\"type\":\"message\"}",
    "question":null,
    "content_option_id":null,
    "answered_by":30,
    "answered_by_role":"patient",
    "answer_numeric":null,
    "answer_string":null,
    "answer_ts":"2013-07-24 20:13:42.112631",
    "content":{"label":"A message from Man Ager:","body":"Here's me message","type":"message"},
    "answer":null
  },
  {
    "id":99,
    "response_id":372,
    "content_id":356,
    "message_id":null,
    "content_type":"radio",
    "content_json":"{\"label\":\"Did you weigh yourself this morning?\",\"type\":\"radio\"}",
    "question":"Did you weigh yourself this morning?",
    "content_option_id":762,
    "answered_by":30,
    "answered_by_role":"patient",
    "answer_numeric":null,
    "answer_string":"yes",
    "answer_ts":"2013-07-24 20:13:45.865674",
    "content":{"label":"Did you weigh yourself this morning?","type":"radio"},
    "answer":"yes"
  },
  ...
]
```
 
Example for a call to get a group. Contains an embedded list of users associated with the group. 

```php
{
  "id":1,
  "organization_id":1,
  "name":"Example Group",
  "meta_json":null,
  "_related_collections": {
    "users":[
      {
        "id":4,
        "organization_id":1,
        "role":"physician",
        "status":"active",
        "first_name":"Logo",
        "middle_initial":null,
        "last_name":"Test",
        "email":"kim.hatcher+logo@roundingwell.com",
        "activity_emails":true,
        "login":"kim.hatcher+logo@roundingwell.com",
        "salt":"d5736019cf664a68c8ff9bd94d88facd",
        "mobile_phone":""
      },
      ...
     ]
  }
}
```
  
Example for a call to get an inbox entry. Contains embedded patient, interaction and user objects. 
Patient object is limited to only those phi fields that were necessary. 

```php
{
  "id":1,
  "type":"referral",
  "user_id":4,
  "interaction_id":4,
  "organization_patient_id":18,
  "created":"2013-04-12 16:57:33.7514",
  "read":null,
  "_related": {
    "patient": {
        "id":"18",
        "first_name":"Yay",
        "last_name":"Hopefully",
        "organization_patient_id":"18",
        "_meta": {
            "days_since_discharge": 6
        }
      },
    "interaction": {
      "id":"4",
      "user_id":"1",
      "patient_risk_id":"1",
      "type":"comment",
      "type_category":"",
      "comment":"I like :::4::: !",
      "close_risk":"0",
      "created":"2013-04-12 16:57:33.642038",
      "message_id":null,
      "archived":null,
      "_related": {
        "user": {
          "id":"1",
          "organization_id":"1",
          "role":"nurse",
          "status":"active",
          "first_name":"Man",
          "last_name":"Ager",
          "email":"exmanager@roundingwell.com",
          "activity_emails":"1",
          "login":"exmanager@roundingwell.com",
          "pass":"$2a$08$G\/YlFYIl3LRxeJlOp4DWiu7dplI3Rmf90W9jKZL8nERDlq.wY9ijC",
          "salt":"0c821f675f132d790b3f25e79da739a7",
          "permissions":"{\"manage_users\":1,\"view_messages\":1}"
        }
      }
    }
  }
}
```


## <a name='api-parameters'>API Parameters</a>

  - **GET Parameters**: 
  GET (or query) params include both params embedded in the url (/patient/get/1) and typical GET query string params (?f1=a&f2=b). If the parameter does not affect any stored value, but simply influences a search, it should be a GET parameter. GET parameter validation rules are given in the controller validation class under the function name {action}_query_rules 

  Validation Example:
```php
    // in classes/validate/{controller_name}.php
    public function get_query_rules()
    {
        return array(
            'id' => array(
                array('not_empty'),
                array('digit'),
            ),
        );
    }
```
  
  An exception to the GET parameter rule is if you need to get all objects that match a list of ids. This list can be of variable length, and so it risks maxing out GET length restrictions. GET params that can be of large length lists should be passed in as POST. 
  
  - **POST Params**: If a parameter could be of long length, or if it affects a stored value, it should be passed in as post. Post validation rules are given in the controller validation class under the function name {action}_rules

  Validation Example:
```php
    public function create_rules()
    {
        return array(
            'role'  => array(
                array('not_empty'),
                array('in_array', array(':value', array('nurse', 'physician', 'dietitian', 'social', 'coordinator', 'other', 'admin'))),
            ),
            'login' => array(
                array('not_empty'),
                array('min_length', array(':value', 3)),
                array('max_length', array(':value', 50)),
            ),
            'pass' => array(
                array('min_length', array(':value', 4)),
                array('max_length', array(':value', 71)),
            ),
            ...
     }
```

## <a name='decryptioin'>Decryption</a>

  - **You can send a hash or a zero-indexed array of hashes**

  - **Minimize Hits**: If you have a large number of objects to decrypt, it's better to combine the phi in one array and send it all in one batch. 
  
## <a name='decrypt-n-log'>You Decrypt it You Log it</a>

Use decrypt? Odds are you need to log phi access. The only exception is if you decrypted something simply to do 
a calculation on the value, and you did NOT return any decrypted phi in the api's return. 

Requests to log access take place in the action of the api at the controller level. Every api controller has a function available to it, $this->access_log(), to handle the logging details for you.

```php
// you returned two patients' first and last names in the api call
$patient_ids = array(1,2);
$this->access_log($patient_ids, 'Decrypted patient name.', array('first_name', 'middle_initial', 'last_name'));

// you decrypted direct messages for patient id 1
$this->access_log(array(1), "decrypted direct messages", null, array('messages' => $array_of_message_ids));

// you decrypted patient id 1's name AND comments on one of their risks
$this->access_log(array(1), "", array('first_name','last_name'), array('interactions' => $array_of_int_ids));
```

## <a name='orm-vs-db'>ORM vs DB Queries</a>

ORMs are pretty and concise for manipulating and creating rows in the db. If all you need is an array of rows, DB queries is the way to go. So, in general:

When dealing with gathering potentially large sets of information: DB queries

When you want to create/manipulate one db row: ORM 

If you want to use ORM to get sets of data that include joins, ensure that you are getting eager rather than lazy loading sub objects. 
