# Overview

This repository contains a set of Postman v2.1 collections that you can use to try out the functionality of the Mollie API. You can import the JSON files into any local Postman instance. The following collections are available:

* The **Mollie v2 API - API Key authentication** collection is based on API key authentication, and includes all endpoints that are available through that type of credentials. This collection is most applicable for a situation where there’s a one-to-one relation between a customer or merchant and Mollie, for example when one ecommerce platform instance connects to one Mollie account.

* The **Mollie v2 API - OAuth-access_token authentication** collection is based on `access_token` credentials, and includes the [Mollie Connect](https://docs.mollie.com/connect/overview) feature set to retrieve those access tokens. This collection is tailored for SaaS or marketplace setups and customers or merchants who want to operate on an account level, for example using Mollie's [Onboarding API](https://docs.mollie.com/reference/v2/onboarding-api/overview), Administration API, etc.

## Structure
The structure of the collections follows the structure of Mollie’s public API documentation. A request is sent to each endpoint, and each request contains at least one example. The example set aims for showcasing the variety of options an endpoint offers, rather than showing every possibility.

## Collection variables
Most endpoint payloads contain variables instead of static values. All variables are initiated at the collection level, and contain dummy data that you can easily adjust. The saved examples display the actual values.

## Credentials
The JSON files contain variables instead of credentials. Postman supports authentication inheritance, so the variables are often called on higher-level objects (collection or folder). Best practice is to create a Postman Environment and initiate all credentials there to prevent credentials from appearing in the collection itself. Besides, you can easily create multiple environments and use them to switch between Mollie accounts or App credentials.

## OAuth
To retrieve the access tokens of another account using OAuth, use the endpoints in the Connect folder of the collection that utilises OAuth, that is, access tokens:

1. Go to **Developers** > **Your apps** in your Mollie Dashboard and register an app in the “partner” account (the one that takes control).
2. Place the client ID and secret in the authorization settings ‘OAuth API’ folder or in the environment variables.
3. Send the ‘Authorise’ request. This constructs the OAuth URL that you can fetch from the Postman console.
4. Log in to the “submerchant” Mollie account (the account that is controlled) and navigate to the URL in your preferred browser.
5. Connect the accounts, and retrieve the `code` parameter from the landing page URL. If you were not logged in to Mollie, you can do so here.
6. Paste the copied code in the `code` parameter in the payload of the ‘Generate access tokens’ request in the same collection folder, and send it. This should take no longer than 30 seconds. If the code expires, go back to step 4.
7. The Postman tests read Mollie’s response and assign the tokens to global variables for further use. You can now send requests to all other endpoints in the collection and control the “submerchant” account.

After one hour, you need to refresh the `access_token` using the ‘Refresh tokens’ endpoint. Send a request to the endpoint and the variables holding the tokens will be overwritten with the new values.

## Test mode
Use the collections with an API key for test mode. **Mollie v2 API - OAuth-access_token authentication** uses the test mode query parameter (`GET`/`DELETE`) or payload-parameter (`PUT`/`PATCH`) by default.

## Feedback
Mollie strives to align the collection with the [public API documentation](https://docs.mollie.com/). Your feedback or additional examples are welcome in comments, or submit them as a pull request.
