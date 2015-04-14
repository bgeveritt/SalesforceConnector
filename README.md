Build Mendix apps on top of your Salesforce.com environment in minutes. Get the rapid development and deployment power of Mendix seamlessly integrated on top of your entire existing Salesforce.com architecture. This adapter quickly and easily allows you to communicate with standard or custom objects in your company's Salesforce.com instance.

The current version of this module supports the integrating with Salesforce via their strongly-typed Enterprise WSDL, and performs the following operations:

* Login
* Logout
* Query Account
* Query Accounts
* Query Account Contacts
* Query Account Opportunities
* Query Account Tasks (Activities)
* Create Account Tasks (Activities)
* Create Account Contacts

# Getting Started

* The *Salesforce Connector* module can be downloaded from within the Mendix Business Modeler via the Mendix App Store
* The module requires version 5.10.0+ of the Mendix Business Modeler

# Configuration

Populate the following constants:

* `Username` - The username to access your Salesforce instance
* `Password` - The password assigned to your Salesforce account
* `SecurityToken` - Provided by Salesforce to execute requests against their API
* `LoginUrl` - The endpoint for the Login request (e.g.: https://login.salesforce.com/services/Soap/c/31.0 or https://test.salesforce.com/services/Soap/c/31.0)

# Example Usage - Query Accounts

To obtain a list of your Accounts within Salesforce, you can simply source a Data grid from the existing `QueryAccounts` Microflow.

* Drop a Data grid on your page
* Set the following Data source properties:
  * `Type` - Microflow
  * `Microflow` - QueryAccounts

Note: The default QueryAccounts Microflow will only obtain the first 10 Accounts from Salesforce. Please refer to the Example Usage - Extending section to learn how to query other fields and additional records.

# Example Usage - Extending

The standard objects and fields retrieved via the default Salesforce Connector should be relevant to all Salesforce instances, however, there will be the need to retrieve additional fields (both standard and custom.) The following instructions explain how to query additional Account fields. Naturally, this concept can be applied to all objects.

* Within the Mendix Business Modeler, navigate to the `AccountResponse` XML-to-domain mapping, located in `Mappings\Responses`
* Click the `Select elements...` button at the top of the screen
* A pop-up will appear, displaying a graphical representation of your Salesforce WSDL. The `queryResponse` object should already be expanded, displaying a list of all the available fields that can be retrieved from your Salesforce instance. In this case, a number of fields will already be selected, relevant to the `Account` object. Select the additional fields you would like to query.
* Navigate to the `Domain Model` within your `SalesforceConnector` module
* Add the additional fields to the `Account` entity, with the relevant data types
* Navigate back to `AccountResponse` and map the new entity attributes to the additional fields
* Navigate to the `QueryAccounts` Microflow
* Double-click the `CreateQuery` Activity, and add the additional fields to your [SOQL Select command](http://www.salesforce.com/us/developer/docs/officetoolkit/Content/sforce_api_calls_soql_select.htm)
