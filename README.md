## THE 2 COLLECTIONS
This repository contains 2 Postman v2.1 collections shipped in JSON files that are ready to be imported into any local Postman instance. Collection ‘Mollie v2 API - API Key authentication’ is based on API Key authentication at Mollie and contains all endpoints that are available through that type of credentials. They are most applicable for a situation where there’s a one-to-one relation between a customer/merchant and Mollie, for instance one ecommerce platform instance that connects to one Mollie account. 

The other collection, ‘Mollie v2 API - OAuth/access_token authentication’, is based on access_token credentials and includes the Mollie Connect feature set to retrieve those. Thus, this collection is tailored for SaaS / marketplace setups and customers/merchants that want to operate on account-level (Onboarding API, Administration API, etc.)

## STRUCTURE
The collection is structured like Mollie’s public API documentation. Every endpoint is represented in a call and every call contains one or more examples. The example set will be extended and aims at showcasing the variety of options the endpoint offers, rather than showing every possibility.

## COLLECTION VARIABLES
Most endpoint payloads contain variables instead of static values. All these variables are initiated at the Collection level and contain dummy data that can easily be adjusted. For the saved examples it was decided to display the actual values used.

## CREDENTIALS
No credentials are present in the JSON files. Instead, everywhere credentials are required, variables are used instead. Postman supports authentication inheritance, so these variables are often called on higher-level objects (collection or folder). It is advised to create a Postman Environment and initiate all credentials in there. This prevents credentials from appearing in the collection itself. Besides, you can easily create multiple environments and use this to switch between Mollie accounts or App credentials.

## OAUTH
If you want to retrieve the access_tokens of another account using OAuth, you can use the endpoints in the Connect folder of the collection that utilises OAuth/access_tokens. Follow these steps:
1. Start with registering an app in the “partner” account (the one that takes control) in your Mollie Dashboard (‘Developers’ --> ‘Your apps’). 
2. Place the client id and secret in the authorization settings ‘OAuth API’ folder or the environment variables.
3. Send the ‘Authorize’ call. This will construct the OAuth URL, which you can fetch from the Postman console.
4. Make sure you are logged in to the “submerchant” Mollie account (the account that is controlled) and navigate to the URL in your preferred browser.
5. Connect the accounts and retrieve the ‘code’ parameter from the landing page URL. If you were not logged into Mollie, you can do that here.
6. Place the copied code in the ‘code’ parameter in the payload of the ‘Generate access tokens’ call in the same collection folder and send it (this may take no longer than 30 seconds. If the code expires, go back to step 4).
7. The Postman tests will read Mollie’s response and assign the tokens to global variables for further use. You can know use all other endpoints this collection and control the “submerchant” account.
After one hour, the access_token needs to be refreshed by the ‘Refresh tokens’ endpoint. Simply send it and the variables holding the tokens will be overwritten with the new tokens.

## TESTMODE
Keep in mind to use the collections with an API key for test mode. The collection based on OAuth/access_tokens uses the test mode query-parameter (GET/DELETE) or payload-parameter (PUT/PATCH) by default.

## FEEDBACK
Mollie will keep the collection aligned with the public API documentation. Feedback or additional examples are welcomed and can be submitted as a comment or PR.
