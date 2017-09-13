---
title: Recurring Payment
layout: tutorial

summary: Recurring Payment.

navigation:
    header: na.tocs.na_nav_header
    footer: na.tocs.na_nav_footer
    toc: na.tocs.recurring_payment_reference
    header_active: guides
---

# Modify a recurring payment

##  Request parameters

**URL:** https://api.na.bambora.com/scripts/recurring_billing.asp </br>
**Method:** POST

#### Authorisation
| Parameter | Format | Description |
|----------|--------|-------------|
| requestType | BACKEND | Always pass "BACKEND" (case sensitive). |
| merchant_id | 9 digits | Unique identifier for your Bambora merchant account (not "merchantId"). |
| passcode | 32 digits | Recurring Payment API Passcode (not the Payment API passcode) |


| Parameter | Format | Description |
|----------|--------|-------------|

| serviceVersion |  | Always "1.0". |
| operationType |  | "M" for modify or "C" for close |

#### Transaction
| Parameter | Format | Description |
|----------|--------|-------------|
| rbBillingPeriod | D, W, M, or Y | ...|
| rbBillingIncrement | ... | ... |
| rbBillingEndMonth | 1 or 0 | ... |
| rbNeverExpires | 1 or 0 | ... |

| processBackPayments | 1 or 0 | ... |

| rbAccountId | Up to 10 digits | The identifier of the recurring payment to be modified. |
| Amount | Max. 9-digits | The new amount. |
| rbBillingState | O, C, or A | "O" to pause payments by putting an account on hold. "C" to close the recurring account. "A" – to reactivate an account that was on hold or closed. |

#### Billing address
| Parameter | Format | Description |
|----------|--------|-------------|
| ordName | Max. 64 alphanumeric characters | Update the recurring billing account holder name (use trnCardOwner to change the name of a card owner). |
| ordAddress1 | Max. 64 alphanumeric characters | First line of the customer’s recurring billing profile address. |
| ordAddress2 | Max. 64 alphanumeric characters | Second line of the customer’s recurring billing profile address. |
| ordCity | Max. 32 alphanumeric characters | Customer’s city. |
| ordProvince | 2 characters | Must match a valid province code. |
| ordCountry | 2 characters | Must match a valid country code |
| ordPostalCode | Max. 16 alphanumeric characters | Postal code for the customer’s recurring billing profile address. |
| ordEmailAddress | Max. 64 characters | Customer email address. |
| ordPhoneNumber | Max. 32 alphanumeric characters | Customer phone number |

#### Card info
| Parameter | Format | Description |
|----------|--------|-------------|
| trnCardOwner | Max. 64 alphanumeric characters | Credit card owner's name. |
| trnCardNumber | Max. 20 digits | Customer credit card number. |
| trnExpMonth | 2 digits | Credit card expiry month. Format MM (January = 01). |
| trnExpYear | 2 digits | Credit card expiry year. Format YY. (2008 = 08) |

#### Schedule
| Parameter | Format | Description |
|----------|--------|-------------|
| rbFirstBilling | 8 digits | Date of the first charge against the customer’s recurring billing account. Passing a new value in this field overrides the data in the system even if the existing First Billing date has already passed. |
| rbSecondBilling | 8 digits | Date of the second charge against the customer’s recurring billing account. The second billing date is updated to reflect one full billing period after the First Billing date. Use this variable to process the second charge at a date outside the regular schedule and prorate the first payment. After the second billing date, all payments are scheduled at regular increments |
| rbExpiry | 8 digits | Expiry date for the recurring billing account. Format MMDDYYYY. |


##  Response codes

| Code | Message |
|------|---------|
| 1 | Request successful |
| 2 | Secure connection required |
| 3 | Service version not supported |
| 4 | Invalid login credentials |
| 5 | Invalid operation type |
| 6 | Invalid amount value |
| 7 | Invalid recurring billing account id |
| 8 | Merchant account is closed or disabled |
| 9 | Invalid XML message |
| 10 | Unexpected error |
| 11 | Login failure. Service Lockout |
| 12 | Invalid process back payments parameter |
| 13 | No fields to update in modification request |
| 14 | Customer address/payment information failed data validation |
| 15 | Invalid recurring billing account state |
