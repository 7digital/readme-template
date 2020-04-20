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
* No client-facing SLAs

### Dependencies

### Owner

## System detail

### Data and processing flows

### Infrastructure and network design

### Resilience

### Scalability

### Expected traffic and load

## Monitoring and alerting

## CI/CD

## Known issues
