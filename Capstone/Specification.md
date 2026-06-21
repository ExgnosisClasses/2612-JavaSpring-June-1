# Capstone Specification

#### Version 1.0  June 22

## Introduction and Background

The Bank had originally commissioned a React SPA client for the use of both account holders and front line bank staff. 

The original React SPA application implemented security using the native React libraries. The application was shelved because it failed the Bank's security review for regulatory compliance.

There is currently interest in reactivating the original project but using the OAuth recommendation for delegating the security to a BFF, backend for frontend, component.

Your project is a proof of concept project to confirm whether the BFF architecture is a viable approach solving the security issue.

---

## Environment 

Since this is a proof of concept project, your team will have to work in development environment with mocks of the main productions components that the SPA/BFF will have to interact with.

### Authentication Server

You will need to run a mock authentication server. You already have done most of this in the labs. There are only a few small changes necessary to make it usable in the project

### WireMock Server

You will need a wire mock server to emulate an external service. You have already written the code for it in one of the labs as part of the BankAPI. All that will be required is to extract the wiremock code into a stand alone Spring Boot project

### Kafka Broker and Oracle Database

You will be provided with a DDL for an Oracle database for persistent storage for transactions. You can use Docker to run the database. The work you will be required to do will be similar to what you did in the labs.

Similarly, you will be provided with a message schema for using a Kafka topic. You can also use Docker for Kafka. As with Oracle, the work you will be required to do will be similar to what you did in the labs.

### BankService

This will be a mockup of the actual bank service. This will be based on the BankAPI project you created in the labs.

Using the lab version, you will be required to integrate the database connectivity and the Kafka connectivity, as well as implementing all the required security constraints.

---

## Tasking

While there is work required get the mock components working, most of your work will take place in two components.

### React SPA

The main task will be to run the React functionality through the BFF in a provably secure manner.

### BFF

This the key component since it connects the SPA to the bank infrastructure, or at least the mocks you have created.

---

## SPA Overview

The SPA is designed to be deployed into a bank web application. There are two different types of users

### Functional Overview

There are two types of users

1. Customers
   - These are account holders. 
   - They can query their accounts, review transactions on their accounts and make transfers between accounts.
   - Customers can only see their own accounts and cannot do anything that would change the status or balance on their accounts.
   - The application supports two kinds of transfers.
     - Internal transfers between the customer accounts
     - External transfers between the customer and an external payment service (for utility payments for example).

2. Bank Staff
   - The bank staff can view any customer's accounts. 
   - The can also make transfers between a specific customer's accounts but not accounts that belong to different customers.
   - Bank staff can also record deposits and withdrawals on an account in order to record cash transactions done by a teller at the bank.

#### Business Rules
- There a set of business rules that have to be implemented by the capstone. 
- A full list will be provided but these cover the rules about when a transactions should be allowed and when it should be declined
  - For example, insufficient funds, etc.

---

## BankService

The BanksService needs to implement the following

### Audit

Every transaction, including failed transactions, must be recorded in an audit table in the database.

### Security

The security should be implemented at both the endpoints and in the service layer for enforcement of business rules

---

## Testing and Validation

Part of the deliverables is a full set of functional tests, both unit and integration tests, that validate the correctness of your work.

The presentation will require you to demonstrate the flow a transaction takes from end to end through your project



---

## Bonus

The following is not required but are additional pieces you can try


### Security Log

- The BFF records all logins successes and failure in a Kafka topic.

### Transaction report

- The BankService uses Kafka to output all transactions into a CVS file.

### Resilience

- Implement the retry resilience pattern and demonstrate that it works. 

---

This is just an overview, more detailed specification on each component will be provided during the week before the capstone


## End
