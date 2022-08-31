## [2.25.0] - 2022-08-17
##Added
**New country authorizations endpoints**

Country authorizations can now be viewed by using one of the following endpoints:

<a href="https://docs.mangopay.com/endpoints/v2.01/regulatory#e1061_the-country-authorizations-object">View a country's authorizations</a> <br>
<a href="https://docs.mangopay.com/endpoints/v2.01/regulatory#e1061_the-country-authorizations-object">View all countries' authorizations</a>

With these calls, it is possible to check which countries have:

- Blocked user creation
- Blocked bank account creation
- Blocked payout creation

Please refer to the <a href="https://docs.mangopay.com/guide/restrictions-by-country">Restrictions by country</a>
article for more information.

## [2.24.0] - 2022-06-29
##Added
**Recurring: €0 deadlines for CIT**

Setting free recurring payment deadlines is now possible for CIT (customer-initiated transactions) with the **FreeCycles** parameter.

The **FreeCycles** parameter allows platforms to define the number of consecutive deadlines that will be free. The following endpoints have been updated to take into account this new parameter:

<a href="https://docs.mangopay.com/endpoints/v2.01/payins#e1051_create-a-recurring-payin-registration">Create a Recurring PayIn Registration</a><br>
<a href="https://docs.mangopay.com/endpoints/v2.01/payins#e1056_view-a-recurring-payin-registration">View a Recurring PayIn Registration</a><br>

This feature provides new automation capabilities for platforms with offers such as “Get the first month free” or “free trial” subscriptions.

Please refer to the <a href="https://docs.mangopay.com/guide/recurring-payments-introduction">Recurring payments overview</a> documentation for more information.

## [2.23.0] - 2022.05.24
### Added

#### UserCategory management

Users can now be differentiated depending on their MANGOPAY usage.

This is possible with the new UserCategory parameter, whose value can be set to:

- Payer – For users who are only using MANGOPAY to give money to other users (i.e., only pay).
- Owner – For users who are using MANGOPAY to receive funds (and who are therefore required to accept MANGOPAY’s terms and conditions).

Please note that the following parameters become required as soon as the UserCategory is set to “Owner”:
- HeadquartersAddress
- CompanyNumber (if the LegalPersonType is “Business”)
- TermsAndConditionsAccepted.

The documentation of user-related endpoints has been updated and reorganised to take into account the new parameter:

[Create a Natural User (Payer)](https://docs.mangopay.com/endpoints/v2.01/users#e255_create-a-natural-user)
[Create a Natural User (Owner)](https://docs.mangopay.com/endpoints/v2.01/users#e1059_create-natural-user-owner)
[Update a Natural User](https://docs.mangopay.com/endpoints/v2.01/users#e260_update-a-natural-user)
[Create a Legal User (Payer)](https://docs.mangopay.com/endpoints/v2.01/users#e259_create-a-legal-user)
[Create a Legal User (Owner)](https://docs.mangopay.com/endpoints/v2.01/users#e1060_create-a-legal-user-owner)
[Update a Legal User](https://docs.mangopay.com/endpoints/v2.01/users#e261_update-a-legal-user)
[View a User](https://docs.mangopay.com/endpoints/v2.01/users#e256_view-a-user)
[List all Users](https://docs.mangopay.com/endpoints/v2.01/users#e257_list-all-users)

Differentiating the platform users results in a smoother user experience for “Payers” as they will have less declarative data to provide.

## [2.22.0] - 2022.05.12
### Added

#### Terms and conditions acceptance parameter

The acceptance of the MANGOPAY terms and conditions by the end user can now be registered via the SDK.

This information can be managed by using the new `TermsAndConditionsAccepted` parameter added to the `User` object.

The following API endpoints have been updated to take into account the new TermsAndConditionsAccepted parameter:

[Create a Natural User](https://docs.mangopay.com/endpoints/v2.01/users#e255_create-a-natural-user)
[Update a Natural User](https://docs.mangopay.com/endpoints/v2.01/users#e260_update-a-natural-user)
[Create a Legal User](https://docs.mangopay.com/endpoints/v2.01/users#e259_create-a-legal-user)
[Update a Legal User](https://docs.mangopay.com/endpoints/v2.01/users#e261_update-a-legal-user)
[View a User](https://docs.mangopay.com/endpoints/v2.01/users#e256_view-a-user)

Please note that:

- Existing users have to be updated to include the terms and conditions acceptance information.
- Once accepted, the terms and conditions cannot be revoked.

## [2.21.0] - 2022.03.31
### Added

#### Instant payment eligibility check

With the function
`PayOutEligibilityResult checkInstantPayoutEligibility(String idempotencyKey, PayOutEligibility payOutEligibility);`
the destination bank reachability can now be verified prior to making an instant payout. This results in a better user experience, as this preliminary check will allow the platform to propose the instant payout option only to end users whose bank is eligible.

#### Instant payment mode only

Instant Payment requests can now be automatically cancelled when an issue is encountered (rather than falling back to the standard payout mode).

This is possible by using the new `INSTANT_PAYMENT_ONLY` option that has been added to the `PayoutModeRequested` parameter.

#### Tag on KYC Document creation

You can now add a tag while creating a KYC Document

### Fixed

- Issues with the BankAccount deserializer and IBAN and US account number
- missing debitedFunds and fees on class RecurringPayInMIT


## [2.20.0] - 2021-11-17
## Added

### Instant payouts hooks

We are now providing new hooks for our new feature [Instant payouts](https://docs.mangopay.com/guide/instant-payment-payout) :

- INSTANT_PAYOUT_SUCCEEDED
- INSTANT_PAYOUT_FALLBACKED

It will allow you to trigger an action depends on the Instant Payout treatment.

### GET a RecurringPayIn ID

You can now request the RecurringPayIn ID to check if the status is valid using
`this.api.getPayInApi().get(createdCit.getId())`

## [2.19.0] - 2021-10-20
## Added

You can now change the status to "ENDED" for a recurring payment.

## Fixed

- "Status" is now available in the response when you request a recurring payment registration.

## [2.18.0] - 2021-10-14
## Fixed

- Card deactivation
- UBO Declaration creation
- User-Agent in headers

## Added

### Payconiq

As requested by numerous clients, we are now providing [Payconiq](https://www.payconiq.be) as a new mean-of-payment. To request access, please contact MANGOPAY.

### Flags for KYC documents

**We provide more information regarding refused KYC documents.** Therefore it will be easier for you to adapt your app behavior and help your end user.

You are now able to see the exact explanation thanks to a new parameter called “Flags”.

It has been added to

` this.api.getKycDocumentApi().getKycDocument(kycDocument.getId());`

It will display one or several error codes that provide the reason(s) why your document validation has failed. These error codes description are available [here](https://docs.mangopay.com/guide/kyc-document).

## [2.17.0] - 2021-08-10
## Fixed

- Better error parsing (issue #244)
- Change `FallbackReason` parameter's type to object in PayOutPaymentDetailsBankWire

## Added

- You can now update and view a Recurring PayIn Registration object. To know more about this feature, please consult the documentation [here](https://docs.mangopay.com/guide/recurring-payments-introduction).
- To improve recurring payments, we have added new parameters for CIT : DebitedFunds & Fees. To know more about this feature, please consult the documentation [here](https://docs.mangopay.com/endpoints/v2.01/payins#e1053_create-a-recurring-payin-cit)

## [2.16.0] - 2021-06-10
## Added

We have added a new feature **[recurring payments](https://docs.mangopay.com/guide/recurring-payments)** dedicated to clients needing to charge a card repeatedly, such as subscriptions or payments installments.

You can start testing in sandbox, to help you define your workflow. This release provides the first elements of the full feature.

- [Create a Recurring PayIn Registration object](https://docs.mangopay.com/endpoints/v2.01/payins#e1051_create-a-recurring-payin-registration), containing all the information to define the recurring payment
- [Initiate your recurring payment flow](https://docs.mangopay.com/endpoints/v2.01/payins#e1053_create-a-recurring-payin-cit) with an authenticated transaction (CIT) using the Card Recurring PayIn endpoint
- [Continue your recurring payment flow](https://docs.mangopay.com/endpoints/v2.01/payins#e1054_create-a-recurring-payin-mit) with an non-authenticated transaction (MIT) using the Card Recurring PayIn endpoint

This feature is not yet available in production and you need to contact the Support team to request access.

## Fixed

- Missing "Culture" parameter in PreAuthorization

## [2.15.0] - 2021-05-27
## Added

### Instant payment

Mangopay introduces the instant payment mode. It allows payouts (transfer from wallet to user bank account) to be processed within 25 seconds, rather than the 48 hours for a standard payout.

You can now use this new type of payout with the Java SDK.

Example :

```java
PayOut getPayOut = this.api.getPayOutApi().getBankwire(payOut.getId());
// where payOut.getId() is the id of an existing payout
```

Please note that this feature must be authorized and activated by MANGOPAY. More information [here](https://docs.mangopay.com/guide/instant-payment-payout).

### List transactions for a mandate

The [endpoint](https://docs.mangopay.com/endpoints/v2.01/transactions#e993_list-transactions-for-a-mandate) to list all transactions linked to mandate has been added to the SDK.

## [2.14.0] - 2021-05-11
## Fixed

### IBAN for testing purposes

⚠️ **IBAN provided for testing purpose should never be used outside of a testing environement!**

More information about how to test payments, click [here](https://docs.mangopay.com/guide/testing-payments).

### Others

- LegalRepresentativeBirthday primitive Long fixed. Thanks @LeComptoirDesPharmacies

## Added

Some of you use a lot the [PreAuthorization](https://docs.mangopay.com/endpoints/v2.01/preauthorizations#e183_the-preauthorization-object) feature of our API. To make your life easier, we have added three new events :

- PREAUTHORIZATION_CREATED
- PREAUTHORIZATION_SUCCEEDED
- PREAUTHORIZATION_FAILED

The goal is to help you monitor a PreAuthorization with a [webhook](https://docs.mangopay.com/endpoints/v2.01/hooks#e246_the-hook-object).

*Example: If a PreAuthorization is desynchronized, when the status is updated, you will be able to know it.*

## [2.13.0] - 2021-03-25
## Added

### On demand feature for 3DSv2

> **This on-demand feature is for testing purposes only and will not be available in production**

#### Request

We've added a new parameter `Requested3DSVersion` (not mandatory) that allows you to choose between versions of 3DS protocols (managed by the parameter `SecureMode`). Two values are available:
* `V1`
* `V2_1`

If nothing is sent, the flow will be 3DS V1.

The `Requested3DSVersion` may be included on all calls to the following endpoints:
* `/preauthorizations/card/direct`
* `/payins/card/direct`

#### Response

In the API response, the `Requested3DSVersion` will show the value you requested:
* `V1`
* `V2_1`
* `null` – indicates that nothing was requested

The parameter `Applied3DSVersion` shows you the version of the 3DS protocol used. Two values are possible:
* `V1`
* `V2_1`

## [2.12.0] - 2021-02-19
- 3DS2 integration with Shipping and Billing objects, including FirstName and LastName fields
  The objects Billing and Shipping may be included on all calls to the following endpoints:
  - /preauthorizations/card/direct
  - /payins/card/direct
  - /payins/card/web
- Enable Instant Payment for payouts by adding a new parameter PayoutModeRequested on the following endpoint /payouts/bankwire
  - The new parameter PayoutModeRequested can take two differents values : "INSTANT_PAYMENT" or "STANDARD" (STANDARD = the way we procede normaly a payout request)
  - This new parameter is not mandatory and if empty or not present, the payout will be "STANDARD" by default
    Instant Payment is in beta all over Europe - SEPA region
## [2.11.6] - 2020-12-09
- Added 'Regulatory' endpoint to allow checks of User Block Status
- Added support for Regulatory -> Blocked Status Hooks

## [2.11.5] - 2020-09-25
- added test to cover issue
- added new method for PreAuthorization Transactions
- added methods for creating client bank accounts and client payouts

## [2.11.4] - 2020-09-25
- Missing UserID added in UboDeclaration process
- New endpoint to support changes to Card Validation process (please listen out for product announcements)
- Testing added for added for RemainingFunds feature
- Improved gson support and minor fixes

## [2.11.3] - 2020-08-24
- As part of KYC improvements, we are adding OUT_OF_DATE as a enum for KYC documents
- Due to changes to the API we are no longer accepting connections with a TLS certificate of 1.1 or lower, this concerns in particular .NET frameworks 4.5 and earlier. This update applies a fix which forced the application to use TLS 1.2. (edited)
- Fixed port settings in setBaseUrl() for use of Mock API - #206
- ProcessedDate is now a long #170
- Modified function to reflect payinExecutionDetailsDirect #157
- Added binaryData as a parameter to resolve DisputeApi defect #195
- Enabled TLS v1.2 for Java 7

## [2.11.2] - 2020-08-11
- Fixed PayInDeserializer not setting the WireReference from the JSON response.

## [2.11.1] - 2020-08-10
- New MultiCapture and RemainingFunds Parameters in Preauthorization object
- BankingAlias Object returned now fixed, returns complete info
- Fixed JsonNull In PayInDeserializer, thank you https://github.com/ptroc
- "User-agent" format in the headers changed, aligned to other assets

## [2.11.0] - 2020-07-10
- USER_KYC_REGULAR has been added as a new Event. Thanks to it, you are now able to know when all the needed KYCs for a user have been validated and its KYCLevel is updated.
- Release adds typing for EventType values KYC_OUTDATED USER_KYC_REGULAR and USER_KYC_LIGHT
- Bug Fix -> Serializing certain address fields, filtering bank accounts

## [2.10.1] - 2020-03-23
### Fixed
- Serialization issue has been fixed. `ExecutionDetails` property was wrongly sent on JSON request, `TemplateURLOptions` was not taken in account for Payin Web.

## [2.10.0] - 2020-03-19
### Added
- `AccountNumber` property added for Payins `EXTERNAL_INSTRUCTION` (BankingAliases)
- GooglePay `Payin` methods are now available. More info about activation to come in the following weeks...
- `EXPIRED` Mandate Status and linked `MANDATE_EXPIRED` Event Type has been added, as this feature will be shortly supported for DirectDebit Payins. More info on our [docs](https://docs.mangopay.com/endpoints/v2.01/mandates#e230_the-mandate-object)
### Changed
- `PAYLINE`parameter for PayInTemplateURLOptions will be deprecated in the following weeks for Payin Web (especiallay for Payin Cards). `PAYLINEV2` parameter has been added to be used instead.

## [2.9.0]
### Added
- ApplePay `Payin` methods are now available. More info about activation to come in the following weeks...
- New `Dispute` reason type `COUNTERFEIT_PRODUCT` has been added.

## [2.8.1] - 2019-09-09
### Added
- `GetEmoney` method now supports year and month parameters. More info on our [docs](https://docs.mangopay.com/endpoints/v2.01/user-emoney#e895_view-a-users-emoney)
### Fixed
- Fix content-length issue on UBODeclaration submission
- Migration to GSON

## [2.8.0] - 2019-08-29
### Added
- new [`UBODelaration`](https://docs.mangopay.com/endpoints/v2.01/ubo-declarations#e1024_the-ubo-declaration-object) submission system
- `CompanyNumber` support for [Legal `Users`](https://docs.mangopay.com/endpoints/v2.01/users#e259_create-a-legal-user)
### Fixed
Travis CI integration has ben fixed and ensure fast & secure package publishing on maven.org again.

 