# Overview

This repository contains a set of Postman v2.1 collections that you can use to try out the functionality of the Mollie API. You can import the JSON files into any local Postman instance. The following collections are available:

* The **Mollie v2 API - API Key authentication** collection is based on API key authentication, and includes all endpoints that are available through that type of credentials. This collection is most applicable for a situation where there’s a one-to-one relation between a customer or merchant and Mollie, for example when one ecommerce platform instance connects to one Mollie account.

* The **Mollie v2 API - OAuth-access_token authentication** collection is based on `access_token` credentials, and includes the [Mollie Connect](https://docs.mollie.com/connect/overview) feature set to retrieve those access tokens. This collection is tailored for SaaS or marketplace setups and customers or merchants who want to operate on an account level, for example using Mollie's [Onboarding API](https://docs.mollie.com/reference/v2/onboarding-api/overview), Administration API, etc.

## Structure
The structure of the collections follows the structure of Mollie’s public API documentation. A request is sent to each endpoint, and each request contains at least one example. The example set aims to showcase the variety of options an endpoint offers, rather than showing every possibility.

## Collection variables
Most endpoint payloads contain variables instead of static values. All variables are initiated at the collection level, and contain dummy data that you can easily adjust. The saved examples display the actual values.

## Credentials
The JSON files contain variables instead of credentials. Postman supports authentication inheritance, so the variables are often called on higher-level objects (collection or folder). Best practice is to create a Postman Environment and initiate all credentials there to prevent credentials from appearing in the collection itself. Besides, you can easily create multiple environments and use them to switch between Mollie accounts or App credentials.

> **Warning**
Never include confidential information such as passwords, authentication keys, or oAuth tokens in publicly accessible Postman workspaces or collections.

## OAuth
To manually retrieve the access tokens of another account using OAuth, use the endpoints in the Connect folder of the collection that utilises OAuth, that is, access tokens:

1. Go to **Developers** > **Your apps** in your Mollie Dashboard and register an app in the “partner” account (the one that takes control).
2. Place the client ID and secret in the authorization settings ‘OAuth API’ folder or save them as environment variables.
3. Place the `redirect_url` in the ’Authorize’ request's payload and add the desired scopes, separated by spaces. See the [Authorize documentation](https://docs.mollie.com/reference/oauth2/authorize) for the other required parameters.
4. Send the ‘Authorise’ request. This constructs the OAuth URL that you can fetch from the Postman console. 
> **_NOTE:_** This is an easy way to construct the URL and change the variables (e.g. state, scope), 
you can also construct this URL manually without the need to send any API requests.
5. Log in to the “submerchant” Mollie account (the account will be controlled) and navigate to the URL in your preferred browser.
6. Connect the accounts, and retrieve the `code` parameter from the landing page URL. If you were not logged in to Mollie, you can do so here.
7. Paste the copied code in the `code` parameter in the payload of the ‘Generate access tokens’ request in the same collection folder, and send it. This should take no longer than 30 seconds. If the code expires, go back to step 4.
8. A Postman script reads the response body and assigns the tokens to environment variables for further use. You can now send requests to all other endpoints in the collection to create requests on behalf of the "submerchant" account.

After one hour, you need to refresh the `access_token` using the ‘Refresh tokens’ endpoint. Send a request to the endpoint and the variables holding the tokens will be overwritten with the new values.

## Test mode
For test mode, use **Mollie v2 API - API Key authentication** with a test API key. **Mollie v2 API - OAuth-access_token authentication** uses the test mode query parameter (`GET`) or payload-parameter (`POST`/`PATCH`/`DELETE`) by default.

## Feedback
Submit your feedback or additional examples as comments or as a pull request.