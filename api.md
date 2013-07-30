# API Guide

## <a name='TOC'>Table of Contents</a>

  1. [Standard Calls](#standard-calls)  
  1. [Standard Response](#standard-response)  
  1. [ORM vs DB Queries](#orm-vs-db)

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

All objects returned should be true json representations of that object's non phi fields. PHI fields are included only when necessary or specifically requested. 
Objects can be embedded within their referencing parent object.
Any json encoded attributes should be decoded into hash form (json_decode($item, true)). 

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
  ```
  
Example for a call to get an inbox entry. Contains embedded patient, interaction and user objects. Patient object is limited to only those phi fields necessary. 

```php
{
  "id":1,
  "type":"referral",
  "user_id":4,
  "interaction_id":4,
  "organization_patient_id":18,
  "created":"2013-04-12 16:57:33.7514",
  "read":null,
  "patient": {
      "id":"18",
      "first_name":"Yay",
      "last_name":"Hopefully",
      "organization_patient_id":"18"
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
    },
    "message_id":null,
    "archived":null
  }
}
```
