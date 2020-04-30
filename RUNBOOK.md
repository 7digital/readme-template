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

* Events are logged to the `app-error` SumoLogic source category.
* Metrics logged to [DataDog](https://app.datadoghq.com/dashboard/hwj-6qq-rqi/downloading-api)
* Application reports health via `/status` endpoint which ELB uses to determine if it should receive traffic.
* Pingdom checks that a specific basket can be retrieved every minute. Will trigger SRE on-call if it fails twice in a row.

### Expected traffic and load

* ~5 RPS UK evenings
* ~2 RPS UK daytime

## CI/CD

* Deployed via [TeamCity]
* Rollback is accomplished by un-pinning the deployed "Build" and starting the "Deploy" build configuration.

## Known issues

### Pingdom check fails/flaps

* Sometimes the application can deadlock. You can tell that it has deadlocked by finding the EC2 instance that has no CPU usage. It can be fixed by restarting the EC2 instance via the AWS EC2 console. Core Platform have a [ticket](https://example.com) open to investigate. 
