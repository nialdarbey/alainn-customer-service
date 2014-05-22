# Customer Service

Business Entity Service responsible for storage and retrieval of Customer data. It abstracts away from the Systems that store this data, namely
* MySql Database
* SalesForce

# Operations
* getCustomer
  Retrieves Customer from MySql
* addLoyaltyPoints
  Increments loyalty points field in MySql
* saveCustomer
  Stores Customer in MySql and SalesForce
* addMobileToken
  Stores token for Mobile Push Notifications (iOS and Android)

# Technical Points of Note
## Transactional Scope
* This is used because we can't kick off the scope from the HTTP Inbound.
* Set the Action to ALWAYS BEGIN
## Database Connector
* No need to wrap connector in Enricher in order to hold on to original payload. Just use the target attribute instead.
* Particiapate in Scope based Transaction with Transactional Action: ALWAYS JOIN
* Bulk Mode set to through for when Payload is a list. The connector will iterate through the list and resolve the values for each item as Payload. Hence #[payload.preference] on the insert notification preference is for each item on the list. Several SQL statements are sent in bulk to MySql.
## SalesForce Connector
* I have yet to figure out how to get the new ID of the inserted Customer.

# Contact
nial.darbey@mulesoft.com
