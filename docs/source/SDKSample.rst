.. Siddhartha Blog documentation master file, created by
   sphinx-quickstart on Thu Jun  2 22:47:12 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Getting started
---------------


This guide describes how to integrate the SDK and build an application client that uses the SDK APIs.

#. Create an application client.

    See the sample application client that uses command line arguments, or the SDK demo examples that are provided in the artifact package.

#. Install the SDK in the application client.

#. Configure the SDK environment.

#. Use one of the following methods to get the device data:

    - :ref:`Sync method`
    - :ref:`Async method`

Installing the SDK
------------------

The following steps describe how to prepare your application client that uses the SDK as library.

1.	Download the Java SDK package from the given link.

2.	Run JAR sign verification tool to verify authenticity and integrity of the Java SDK achieve artifact.

3. Install the SDK to a local or remote Maven repository.

   - Use Maven install plugin to install the SDK to a local repository.
      
      .. code-block:: XML

          mvn org.apache.maven.plugins:maven-install-plugin:2.5.2:install-file -Dfile=<path-to-sdk-file>

   - Use Maven deploy plugin to deploy the SDK to a remote repository.

      .. code-block:: XML

         mvn org.apache.maven.plugins:maven-install-plugin:2.5.2:install-file -Dfile=<path-to-sdk-file>

         mvn deploy:deploy-file -DgroupId=com.xylem.cloud 
            -DartifactId=xylem-cloud-sdk-java 
            -Dversion=<sdk-version> 
            -Dfile=<path-to-sdk-file> 
            -Dpackaging=jar 
            -DrepositoryId=<id-to-map-on-server-section-of-settings.xml> 
            -Durl=<url-of-the-repository-to-deploy>

4. Add the Java SDK artifact as a dependency to your application client.

   **Maven**

   .. code-block:: XML

       <dependency>
       <groupId>com.xylem.cloud</groupId>
       <artifactId>xylem-cloud-sdk-java</artifactId>
       <version>{LatestVersion}</version>
       </dependency>

   **Gradle**

   .. code-block:: XML

       repositories {
       mavenCentral()
       }
       dependencies {
       compile 'com.xylem.cloud:xylem-cloud-sdk-java:{LatestVersion}'
       }

Configuring the SDK environment
-------------------------------

The SDK environment must be configured before creating any API clients by using the SDK. These steps describe how to create an API context with all the secret keys and environmental details. The configured SDK environment allows the API clients to operate.

1.	Use the methods described in this topic to configure the SDK environment inside the application client. 

2.	Point your application client to the PRODUCTION API environment.

3.	Create Xylem Cloud API clients. 

Method 1: SDK configuration as Java object
*******************************************

Only ``CLIENTCREDENTIAL`` is supported as ``AuthenticationScheme``.

 .. code-block:: Java
    
    import java.util.Properties;
    import com.xylem.cloud.ApiContext;
    import com.xylem.cloud.clients.OgcApiClient;
    // Code omitted for clarity
    ...
    // Create Properties object
    // Replace the property parameters with your application service ID, API secret, OIDC secret key, and auth domain
    Properties properties = new Properties();
    properties.put("gc.domain","{The domain of the Xylem application}");
    properties.put("app.serviceid","{The service ID of your application}");
    properties.put("app.apikey.secret","{The API secret key}");
    properties.put("app.openid.client.secret","{The OIDC secret key}");
    ApiContext adminContext = ApiContext.of(
       ApiEnvironment.PRODUCTION,
       AuthenticationScheme.CLIENTCREDENTIAL,
       new Configurations(properties));
    ClientFactory adminClientFactory = new ClientFactory();
    OgcApiClient ogcApiClient = adminClientFactory.getOgcClient(adminContext);


Method 2: SDK configuration as properties file
***********************************************

   .. code-block:: Java

         import com.xylem.cloud.ApiContext;
         import com.xylem.cloud.clients.OgcApiClient;
         // Code omitted for clarity
         ...
         ApiContext adminContext = ApiContext.of(
            ApiEnvironment.PRODUCTION,
            AuthenticationScheme.CLIENTCREDENTIAL,
            new Configurations({Path of your property file location});
         ClientFactory adminClientFactory = new ClientFactory();
         adminOgcApiClient = adminClientFactory.getOgcClient(adminContext);

The ``sdkconfig.properties`` file must include the following details:

  .. code-block:: Java

         gc.domain={The domain of the Xylem application}
         app.serviceid={The service ID of your application}
         app.apikey.secret={The API secret key}
         app.openid.client.secret={The OIDC secret key}


.. _Sync method:

Sync method
-------------------------------------

This method returns the observed data of a specific device for less than two weeks. Use Xylem Cloud API clients that are created to request data.

**Define the criteria**

To specify the search criteria, create a criteria object to set the following fields:
 
   .. code-block:: Java

       import com.xylem.cloud.clients.query.ObsFetchCriteria;
       import com.xylem.cloud.clients.query.ObservationFields;
       // Code omitted for clarity
        ...
       ObsFetchCriteria criteria = ObsFetchCriteria.builder()
       .deviceId("{DeviceId}")
       .startDateTimeStamp(1577780044L)
       .endDateTimeStamp(1578903244L)
       .fields(Arrays.asList(ObservationFields.customerId,ObservationFields.resultTime))
       .observedProperties("Arrays.asList("deviceRuntime", "relativeEngineLoad")
       .build();


.. list-table:: 
   :widths: 20 30 60
   :header-rows: 1

   * - Field
     - Datatype
     - Description

   * - deviceId
     - long
     - The ID of the device to get the observed data

   * - startDateTimeStamp
     - string
     - The start timestamp and end timestamp for the data extraction

   * - endDateTimeStamp
     - long
     - The date range must be for less than two weeks.

       The timestamp must be in the Epoch format.

   * - ObservationFields
     - enum
     - The following observation fields of your device:

       - resultTime
       - featureOfInterestId
       - thingName
       - customerId
       - instanceId

   * - ObservationFields   
     - string
     - The observation properties of your device

.. _ASync method:

Async method
--------------------------------------

These methods return the observed data of a specific device for more than two weeks but less than six months. Use Xylem Cloud API clients to request data.
The data is returned in the Array data format only.

**Define the search criteria**

To specify the search criteria, create a criteria object to set the following fields:


.. code-block:: Java

       import com.xylem.cloud.clients.query.ObsFetchCriteriaAsync;
       import com.xylem.cloud.clients.query.ObservationFields;
       // Code omitted for clarity
       ...
       ObsFetchCriteriaAsync criteria = ObsFetchCriteriaAsync.builder()
       .deviceId("{DeviceId}")
       .startDateTimeStamp(1577780044L)
       .endDateTimeStamp(1584276193L)
       .fields(Arrays.asList(ObservationFields.customerId,ObservationFields.resultTime))
       .observedProperties(Arrays.asList("deviceRuntime", "relativeEngineLoad"))
       .pageSize(2000)
       .build();


.. list-table:: 
   :widths: 20 30 60
   :header-rows: 1

   * - Field
     - Datatype
     - Description

   * - deviceId
     - long
     - The ID of the device to get the observed data

   * - startDateTimeStamp
     - string
     - The start timestamp and end timestamp for the data extraction

   * - endDateTimeStamp
     - long
     - The date range must be for less than two weeks.

       The timestamp must be in the Epoch format.

   * - ObservationFields
     - enum
     - The following observation fields of your device:

       - resultTime
       - featureOfInterestId
       - thingName
       - customerId
       - instanceId

   * - ObservationFields   
     - string
     - The observation properties of your device
   * - pageSize
     - integrate
     - The number of records to include in a page  





























