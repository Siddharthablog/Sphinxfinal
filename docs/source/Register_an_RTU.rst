.. Siddhartha Sample documentation master file, created by
   sphinx-quickstart on Fri Jun 24 12:53:04 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Register a new RTU
#######################

+----------------+-------------------------------------------------------------------------------------+
| POST           |  /v1/rtu-registry                                                                   |  
+----------------+-------------------------------------------------------------------------------------+

This request registers a new Remote Telemetry Unit (RTU) in Xylem Cloud.


HTTP Request
------------
https://{xxxx cloud public address}/xcloud​/v1​/rtu-registry

Request header
--------------

- Content-Type = application/json
- Accept = application/json
- Date = UTC timestamp
- Content-MD5 = MD5 hash of the content passed
- Authorization = API Key token (xCLOUD <token>)

Security
--------
You must have the following permission to call this endpoint.

``device:registration:admin``

Example Request
---------------

.. code-block:: json

    {
    "manufacturerId": "manufacturedId1",
    "registrations": [
        {
            "registrationId": "2a3b4dddde3ddddd2233",
            "publicKey": "publicKey1",
            "status": "VALID"
        },
        {
            "registrationId": "2a3b4d77de3ddddd2233",
            "publicKey": "publicKey2",
            "status": "INVALID"
        }
    ]
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
   * - manufacturerId

       *required*

     - string 
     - The ID of the manufacturer. 
      
       Example: ``PumpID3!``


   * - registrations

       *required*

     - string
     - The array of RTU data that are going to be registered.

        .. code-block:: json

          {
             "registrationId": "2a3b4dddde3ddddd2233",
              "publicKey": "publicKey1",
              "status": "VALID",
              "rtuId": "2a3b4dddde3ddddd223347dfgerftuas"
          }
 

   * - registrationId

       *required*


     - string
     - The ID of the RTU registration that is associated with the physical device.

       The ID of the RTU registration is provided by manufacturer.

       Pattern: ``20 characters length`` ``alphanumeric``

       Example: ``2a3b4dddde3ddddd2233``

   * - publicKey

       *required*

     - string
     - The public key that represents and identifies the physical device.

       Example: ``ubl213licKey1``

   * - status

       *required*

     - enum
     - The activation status of the device in Xylem Cloud

       * ``VALID`` - Device is valid in Xylem Cloud
       * ``INVALID`` - Device is invalid in Xylem Cloud

       Example: ``VALID``
        
   * - rtuId

       *required* 

     - object
     - The ID of the RTU that generates from Xylem Cloud.
       
       Maximum Length: ``32``
        
       Example: ``2a3b4dddde3ddddd223347dfgerftuas``
       



Example Response
-----------------

.. code-block:: json

    {
       "status": "OK"
       "resultMessage": "Successful"
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
       
       *Successful*


    
Status code
-----------

.. list-table:: 
   :widths: 20 30 60
   :header-rows: 1

   * - Error Code
     - Description
     - Recovery
   * - 200
     - Successful 
     - The request was successful.
   * - 400
     - Bad Request
     - The input parameters in the request body are either incomplete or in the wrong format.

   * - 401
     - Unauthorized
     - You are not authorized to make this request. 
     
       Log in to Xylem Cloud and try again.

   * - 500
     - Internal server error
     - Service is currently unavailable. Your request could not be processed.
      
       Wait a few minutes and try again.


