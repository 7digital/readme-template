Based on [this template](https://docs.google.com/document/d/1h4y6cdCOkwr3tXHn5a_zd1j8nSPvqKWDxiM7r5sqrrs/edit?usp=sharing)

# Basket API Runbook (Example based on a fictional service)

## Overview

### Business overview

* Allows our customers to add tracks or releases to a basket to be later available for purchase via the [7digital web store](https://uk.7digital.com).
* Customers can pay for the contents of the basket, providing revenue for our D2C business.
* The service should be highly available and process calls in a timely fashion to ensure the user experience does not put of people purchasing items.

### Technical overview

* HTTP-based API

### Service Level Agreements (SLAs)

* Internal SLOs:
  * 99.5% of calls in a monthly window return successful HTTP status codes.
  * 99.5% of calls in a monthly window complete in less than 500 ms.
* No explcit client-facing or internal SLA

### Dependencies

* Purchasing API
* Catalogue API
* AWS DynamoDB

### Owner

Core Platform Team

## System detail

### Data and processing flows

TODO: Add diagram

### Infrastructure and network design

TODO: Add diagram

### Resilience

* Deployed into 2 AZs via auto-scaling groups managed by AWS Beanstalk
* Circuit breakers & timeouts implemented on calls to 7digital API
* Traffic is load balanced across multiple instances via an ELB.

### Scalability

* Auto scaling is triggered by excessive CPU usage.
* Manual scaling can be accomplished by configuring the auto-scaling group "min" property
* Limited by 7digital API in the DC
* Requests cannot be throttled.

## Monitoring and alerting

### Expected traffic and load


## CI/CD

## Known issues
