# RoundingWell Code Style Guide

*A mostly reasonable approach to code style*

Taken from style guides for: airbnb, kohana, pear


## <a name='TOC'>Table of Contents</a>

### By Job
  * [API input validation](#kohvalidation)  
  * [Advanced API input validation](#kohcontroller)
  * [API request/response handling](#kohcontroller)
  * [DB queries/CRUD](#kohmodel)
  * [Outside API queries/CRUD](#kohmodel)

### By Layer

  * Kohana/MVC Layers
    * [classes/validation](#kohvalidation)  
    * [classes/controller](#kohcontroller)
    * [classes/model](#kohmodel)
  * Domain Layers
    * [Repositories](#repos)
    * [Entities, Values & Services](#entvalserv)
    * [Permissions](#permissions)


## <a name='kohvalidation'>classes/validation</a>

  - **Validating API input**: If at all possible, all forms of api input validation should happen in these classes.

## <a name='kohcontroller'>classes/controller/v2</a>
  - **Possible API input Validation**: Perhaps an api input can only be confirmed once a model is retrieved or other work has been done. It's only this sort of validation that is allowed in a controller, rather than in [classes/validation](#kohvalidation). 

  - **Traffic Cop**: Primary goal of a controller is to be a traffic cop. Marshalling together the necessary classes in order to actually do the job, and returning their response to the caller. 
  
  - **NO BUSINESS RULES OR LOGIC SHOULD BE IN CONTROLLERS**

## <a name='kohmodel'>classes/model</a>
  - **CRUD handling for various data stores**: Whether it's writing to a db or writing to an outside API, the grunt work of this belongs in a controller.
  
  - **Direct interation with a data store**: Wherever possible, the code to directly interact with a portion of a data store (aka selects on a db, gets on an api, etc), should be corralled in a function on the relevant model.

  - **NO BUSINESS RULES OR LOGIC SHOULD BE IN MODELS**
