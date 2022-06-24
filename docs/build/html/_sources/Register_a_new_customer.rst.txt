.. Siddhartha Sample documentation master file, created by
   sphinx-quickstart on Fri Jun 24 12:53:04 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Register a new customer
#######################

+----------------+-------------------------------------------------------------------------------------+
| POST           |  /v1/customers                                                                      |  
+----------------+-------------------------------------------------------------------------------------+

This request registers a new customer in Xylem Cloud.

**Prerequisite**

1. The application must be created and registered.

2. You must have the following registration key pair values returned from the application registration process:

    - ``serviceId``

    - ``apiKey``

HTTP Request
------------
https://{xxxx cloud public address}/xcloud/v1/customers

Request header
--------------

- Content-Type = application/json
- Accept = application/json
- X-Auth = keycloak

Example Request
---------------

.. code-block:: json

    { 
     "name": "customer1",
      "address": "3649 Lady Bug Drive Staten Island, NY 10312",
      "customerId": "CustomerEast",
      "phoneNumber": "555-966-0696",
      "email": "fred@flintstone.com",
      "status": "ACTIVE",
      "properties": "{\"hours\":\"EST\"}"
      }

Request body
------------

Body parameters
***************

.. list-table:: 
   :widths: 20 30 60
   :header-rows: 1

   * - Name
     - Datatype
     - Description
   * - Name

       *required*


     - string 
     - The name of the customer

       The name supports the following ASCII characters:

       * Alphanumeric characters
       * Spaces
       * Dashes
       * Underscores
       * Periods

       Example: ``EastCoast`` 

   * - address

       *required*


     - string
     - The address of the customer

       The address supports all the unicode characters.

       Example: ``3649 Lady Bug Drive``

   * - customerId

       *required*


     - string
     - The customer ID of the customer that must be associated with the application
     
       The customerId supports the following ASCII characters:

       * Alphanumeric characters
       * Spaces
       * Dashes
       * Underscores
       * Periods

       Example: ``12fr43w667yfeeety644``

   * - phoneNumber

       *required*

     - string
     - The phone number of the customer

       The phoneNumber supports all the unicode characters.

       Example: ``555-966-0696``
  
   * - email

       *optional*

     - string
     - The email address of the customer

       The email supports all the unicode characters.

       Example: ``test@xylem.com``

   * - status

       *required*

     - enum
     - The activation status of the customer in Xylem Cloud

       * ``ACTIVE`` - Customer is active in Xylem application
       * ``INACTIVE`` - Customer is inactive in Xylem application

       Example: ``ACTIVE``
        
   * - properties

       *optional* 

     - object
     - The customer configurable properties

  

Example Response
-----------------

.. code-block:: json

    {
         "resultMessage": "The customer is registered successfully!",
         "customerId": "CustomerEast"
    }


Response parameters
*******************

.. list-table:: 
   :widths: 20 30 60
   :header-rows: 1

   * - Name
     - Datatype
     - Description
   * - resultMessage
     - string 
     - Returns the following result message:
       
       *The customer is registered successfully!*

   * - customerId
     - string
     - Returns the customer ID of the customer that is successfully added


    
Status code
-----------

.. list-table:: 
   :widths: 20 30 60
   :header-rows: 1

   * - Error Code
     - Description
     - Recovery
   * - 200
     - The customer is registered successfully! 
     - The request was successful.
   * - 400
     - Bad Request
     - The input parameters in the request body are either incomplete or in the wrong format.

   * - 401
     - Unauthorized
     - You are not authorized to make this request. Log in to Xylem Cloud and try again.

   * - 500
     - Internal server error
     - Service is currently unavailable. Your request could not be processed. Wait a few minutes and try again. 

