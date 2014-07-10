# RoundingWell Code Organization Guide

*A probably not at all, but better than nothing, reasonable approach to code organization.*

Taken from MVC and DDD concepts. 

## <a name='TOC'>Table of Contents</a>

### By Job
  * [API input validation](#appvalidation)  
  * [Advanced API input validation](#appcontroller)
  * [API request/response handling](#appcontroller)
  * [DB queries/CRUD](#appmodel)
  * [Outside API queries/CRUD](#appmodel)
  * [An attribute has complicated functionality](#domvalue)
  * [An attribute or simple value has business rules associated with it](#domvalue)
  * [An attribute or simple value has logic you want to be universal across the domain](#domvalue)

### By Layer
  * [Application Layers (kohana)](#app)
    * [classes/validation](#appvalidation)  
    * [classes/controller](#appcontroller)
    * [classes/model](#appmodel)
  * [Domain Layers](#domain)
    * [Repositories](#domrepo)
    * [Values](#domvalue)
    * [Entities](#domentity)
    * [Services](#domservice)
    * [Permissions](#dompermissions)


## <a name='app'>Application Layers</a>

### <a name='appvalidation'>Application Validation (classes/validation)</a>

  - **Validating API input**: If at all possible, all forms of api input validation should happen in these classes.

### <a name='appcontroller'>Application Controllers (classes/controller/v2)</a>
  - **Possible API input Validation**: Perhaps an api input can only be confirmed once a model is retrieved or other work has been done. It's only this sort of validation that is allowed in a controller, rather than in [classes/validation](#kohvalidation). 

  - **Traffic Cop**: Primary goal of a controller is to be a traffic cop. Marshalling together the necessary classes in order to actually do the job, and returning their response to the caller. 
  
  - **NO BUSINESS RULES OR LOGIC SHOULD BE IN CONTROLLERS**

### <a name='appmodel'>Application Models (classes/model)</a>
  - **CRUD handling for various data stores**: Whether it's writing to a db or writing to an outside API, the grunt work of this belongs in a controller.
  
  - **Direct interation with a data store**: Wherever possible, the code to directly interact with a portion of a data store (aka selects on a db, gets on an api, etc), should be corralled in a function on the relevant model.

  - **NO BUSINESS RULES OR LOGIC SHOULD BE IN MODELS**

## <a name='domain'>Domain Layers</a>

### <a name='domrepo'>Domain Repositories (classes/domain/repo)</a>
  - **Bridge between the domain and the application models**: Repos are currently the only domain class we have that is allowed to directly reference classes/functions outside the domain. They are the mediator between the domain classes and the CRUD functions of the application models. 

  - **BUSINESS RULES/LOGIC SHOULD BE AVOIDED IN REPOS**

### <a name='domvalue'>Domain Values (classes/domain/value)</a>
  - **Modeling business needs for an attribute**: Occasionally you need to model something that doesn't really "stand on it's own". Maybe you want once place that handles all the formatting needs for a phone number or a timezone. Or perhaps the value is complex (like a survey cadence) and you want to corral logic/rules for it into one place. 

  - **BUSINESS RULES/LOGIC OK**
