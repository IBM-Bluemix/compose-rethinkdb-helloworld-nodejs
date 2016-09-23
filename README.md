# compose-rethinkdb-helloworld-nodejs overview

compose-rethinkdb-helloworld-nodejs is a sample Bluemix application that shows you how to connect to an IBM Compose for RethinkDB for Bluemix service using Node.js.

## Running the app on Bluemix

1. If you do not already have a Bluemix account, [sign up here][bluemix_signup_url]

2. Download and install the [Cloud Foundry CLI][cloud_foundry_url] tool

3. Clone the app to your local environment from your terminal using the following command:

  ```
  git clone https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs.git
  ```

4. `cd` into this newly created directory

5. Open the `manifest.yml` file and change the `host` value to something unique. The host you choose will determinate the subdomain of your application's URL:  `<host>.mybluemix.net`

6. Connect to Bluemix in the command line tool and follow the prompts to log in.

  ```
  $ cf api https://api.ng.bluemix.net
  $ cf login
  ```

7. Create the Compose for RethinkDB service in Bluemix if you haven't already done so.

  **Note :** The Compose for RethinkDB service does not offer a free plan. For details of pricing, see the _Pricing Plans_ section of the [Compose for RethinkDB service][compose_for_rethinkdb_url] in Bluemix.

  ```
  $ cf create-service compose-for-rethinkdb Standard my-compose-for-rethinkdb-service
  ```

8. Push the app to Bluemix.

  ```
  $ cf push
  ```

Your application is now running at `<host>.mybluemix.net`.

## Code Structure

| File | Description |
| ---- | ----------- |
|[**server.js**](server.js)|Establishes a connection to the RethinkDB database using credentials from VCAP_ENV and handles create and read operations on the database. |
|[**main.js**](public/javascripts/main.js)|Handles user input for a PUT command and parses the results of a GET command to output the contents of the RethinkDB database.|

The app uses a PUT and a GET operation:

- PUT
  - takes user input from [main.js](public/javascript/main.js)
  - uses the `r.db().table().insert()` method to add the user input to the database

- GET
  - uses `r.db().table().run()` method to retrieve the contents of the _words_ collection
  - returns the response from the database to [main.js](public/javascript/main.js)

## Privacy Notice
The sample web application includes code to track deployments to Bluemix and other Cloud Foundry platforms. The following information is sent to a [Deployment Tracker](https://github.com/cloudant-labs/deployment-tracker) service on each deployment:

* Application Name (application_name)
* Space ID (space_id)
* Application Version (application_version)
* Application URIs (application_uris)

This data is collected from the VCAP_APPLICATION environment variable in IBM Bluemix and other Cloud Foundry platforms. This data is used by IBM to track metrics around deployments of sample applications to IBM Bluemix. Only deployments of sample applications that include code to ping the Deployment Tracker service will be tracked.

### Disabling Deployment Tracking

Deployment tracking can be disabled by removing `require("cf-deployment-tracker-client").track();` from the beginning of the `server.js` file.

[compose_for_rethinkdb_url]: https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/
[bluemix_signup_url]: https://ibm.biz/compose-for-rethinkdb-signup
[cloud_foundry_url]: https://github.com/cloudfoundry/cli
