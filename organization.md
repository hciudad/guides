# RoundingWell Code Organization Guide

*A "better than nothing" approach to code organization.*

Taken from MVC and DDD concepts. 

## <a name='TOC'>Table of Contents</a>

### By Layer
  * [Application Layers (kohana)](#app)
    * [classes/validation](#appvalidation)  
    * [classes/controller](#appcontroller)
    * [classes/model](#appmodel)
    * [classes/service](#appservice)
  * [Domain Layers (POP classes)](#domain)
    * [Repositories](#domrepo)
    * [Values](#domvalue)
    * [Entities](#domentity)
    * [Services](#domservice)
    * [Permissions](#dompermissions)

### By Job
  * [I have work to do that is not business specific](#app)
  * [API input validation](#appvalidation)  
  * [Advanced API input validation](#appcontroller)
  * [API request/response handling](#appcontroller)
  * [DB queries/CRUD](#appmodel)
  * [Outside API queries/CRUD](#appmodel)
  * [An attribute has complicated functionality](#domvalue)
  * [An attribute or simple value has business rules associated with it](#domvalue)
  * [An attribute or simple value has logic you want to be universal across the domain](#domvalue)
  * [An object has complicated functionality](#domentity)
  * [An object has business rules associated with it](#domentity)
  * [An object has logic you want to be universal across the domain](#domentity)
  * [Modeling a business event or process](#domservice)
  * [An event or process has behavior/rules specific to the business](#domservice)
  * [You need to change/specify permissions for a requesting user on a resource](#dompermissions)


## <a name='app'>Application Layers</a>
This layer is for all the work that needs to happen that isn't really a business (domain) rule. The App layer asks the domain to answer questions and do jobs, **it does not attempt to do the work on it's own**. This is the realm of whatever framework/orm/etc you've chosen and any other classes you need to deal with infrastructure. For example, a patient is stored in the database, and the basic CRUD code to interact with that DB row belongs in the Application ([models](#appmodel) to be exact). However, the business rule that all requests for a patient be logged should be documented and enforced at the domain level. 

### <a name='appvalidation'>Application Validation (classes/validation)</a>

  - **Validating API input**: If at all possible, all forms of api input validation should happen in these classes. Examples: rules that require an input parameter to be a number, or to be among a list of options (though that list may be defined by the domain), the rule is specified in the validation classes.

### <a name='appcontroller'>Application Controllers (classes/controller/v2)</a>
  - **Possible API input Validation**: Perhaps an api input can only be confirmed once a model is retrieved or other work has been done. It's only this sort of validation th at is allowed in a controller, rather than in [classes/validation](#kohvalidation). 

  - **Traffic Cop**: Primary goal of a controller is to be a traffic cop. Marshalling together the necessary classes in order to actually do the job, and returning their response to the caller. 
  
  - **NO BUSINESS RULES OR LOGIC**

### <a name='appmodel'>Application Models (classes/model)</a>
  - **CRUD handling for various data stores**: Whether it's writing to a db or writing to an outside API, the grunt work of this belongs in a controller.
  
  - **Direct interation with a data store**: Wherever possible, the code to directly interact with a portion of a data store (aka selects on a db, gets on an api, etc), should be corralled in a function on the relevant model.

  - **NO BUSINESS RULES OR LOGIC**

### <a name='appservice'>Application Service (classes/service)</a>
  - **classes to handle infrastructure needs**: You may need a class to interact with a piece of infrastructure, like sending email, or interacting with the cryption servers. These contain nothing business-specific, just code that allows for easy use of a remote service.  

  - **NO BUSINESS RULES OR LOGIC**

## <a name='domain'>Domain Layers</a>
The domain is the heart/brain of the product. It attempts to model the business domain itself, using business-familiar terms and concepts. It should be written in plain old php classes, avoiding references to outside dependencies, such that it could (with minimal effort) be usable by different workers (ex: test suites) or a different application environment (like if you changed frameworks). Anything that is core to what roundingwell does should be abstracted down into the domain. 

### <a name='domrepo'>Domain Repositories (classes/domain/repo)</a>
  - **Bridge between the domain and the application models**: Repos are currently the only domain class we have that is allowed to directly reference classes/functions outside the domain. They are the mediator between the domain classes and the CRUD functions of the application models. 

  - **BUSINESS RULES/LOGIC SHOULD BE AVOIDED IN REPOS**

### <a name='domvalue'>Domain Values (classes/domain/value)</a>
  - **Modeling business needs for an attribute**: Occasionally you need to model something that doesn't really "stand on it's own". Maybe you want once place that handles all the formatting needs for a phone number or a timezone. Or perhaps the value is complex (like a survey cadence) and you want to corral logic/rules for it into one place. 

  - **BUSINESS RULES/LOGIC FOR THE VALUE BELONG HERE**

### <a name='domentity'>Domain Entity (classes/domain/entity)</a>
  - **Modeling business needs for an entity**: An entity can stand on it's own, or has an identity that the business itself would recognize. A user or a patient is an obvious example, but sometimes the distinction between entities and [Domain Values](#domvalue) can be a bit fuzzy. Use your best judgement. 

  - **BUSINESS RULES/LOGIC FOR THE ENTITY BELONG HERE**

### <a name='domservice'>Domain Service (classes/domain/service)</a>
  - **Modeling business needs for an event, process or service**: Occasionally there are processes/events that merit classes all their own, or perhaps a job that spans multiple entities and doesn't belong to any one of them. There you have services. A few examples might be turning on engagement. This is an event that spans the organization patient entity, the survey taker entity, and checkin Qs. This event was therefore abstracted out into it's own service class. Other examples are the process of creating a checkin, or the work to generate business statistics. Neither of these things have an "identity" nor are they an attribute of an entity. 

  - **BUSINESS RULES/LOGIC FOR THE SERVICE BELONG HERE**

### <a name='dompermissions'>Domain Permissions (classes/domain/permission)</a>
  - **Specifying permissions for a requesting user to a resource**: These classes specify what a requesting user is allowed to access in the api.  

  - **ONLY BUSINESS RULES FOR USER PERMISSIONS BELONG HERE**
