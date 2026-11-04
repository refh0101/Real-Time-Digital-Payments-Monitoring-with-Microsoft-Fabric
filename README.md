# Real-Time-Digital-Payments-Monitoring-with-Microsoft-Fabric
An end-to-end real-time digital payments monitoring solution built with Microsoft Fabric, using streaming transaction data to demonstrate PII protection, exception detection, Eventhouse analytics, and real-time operational insights.

## Project Overview

Digital payment platforms generate a continuous flow of transactions across channels such as mobile applications, online banking, card payments, ATMs, and transfers.

The challenge is not only collecting these transactions, but being able to see what is happening as it happens.

This project explores how Microsoft Fabric Real-Time Intelligence can be used to build a streaming payment-monitoring architecture. Historical banking transactions from a Kaggle dataset are replayed as live events, processed through Fabric Eventstream, stripped of selected PII fields, and sent to Eventhouse for real-time analysis.

The project focuses on three areas:

- Operational visibility: Monitor payment activity as transactions arrive.
- Data protection: Remove unnecessary PII before transactions are persisted for analytics.
- Exception detection: Create a foundation for identifying data-quality issues, failed transactions, and defined risk indicators in real time.

## Problem Statement

Digital payment systems generate a continuous stream of transactions, yet most organizations still analyze this data in delayed batches, often hours or days after the events occur. For digital payments, that delay matters. By the time an issue is detected, a failed payment may already have affected a customer, a suspicious transaction may have been completed, or a compliance gap may have gone unnoticed.

Operational teams need timely visibility into:

- Payment-channel issues
- Invalid or incomplete transaction records
- Failed or unusual transactions
- Changes in transaction volumes
- Transactions marked with elevated risk indicators
- AML or KYC exceptions
- Sensitive information flowing further than necessary

## Tech Stack

| Technology | Role |
|---|---|
| Microsoft Fabric | Core data and analytics platform |
| Fabric Real-Time Intelligence | Real-time processing environment |
| Fabric Notebook | Simulates the transaction source |
| Python | Generates and publishes transaction events |
| Pandas | Loads and processes the source dataset |
| Azure Event Hubs Python SDK | Publishes events from the notebook |
| Fabric Eventstream | Ingests and processes streaming transactions |
| Custom Endpoint | Connects the notebook producer to Eventstream |
| Manage Fields | Removes selected PII fields from the stream |
| Eventhouse | Stores transformed real-time transaction data |
| KQL | Queries and analyses real-time events |
| Fabric Activator | Planned alerting and event-driven actions |
| Real-Time Dashboard | Planned operational monitoring layer |

## Architecture Diagram

## PII Handling

The source dataset contains information that is not required for the planned operational analytics.

For the current implementation, two fields are treated as PII to be removed from the downstream transaction stream:

- customer_name
- ip_address

Rather than storing everything simply because it exists in the source, the project applies a data-minimization approach.

The event initially arrives with the full transaction structure:

**Raw payment event**

**Raw payment event** → `customer_name` · `ip_address` · `customer_id` · `account_id` · `transaction_id` · `amount` · `currency` · `risk_score` · `...`

The Eventstream processing layer removes:

- customer_name
- ip_address

The sanitized event continues with the fields needed for monitoring:

**Transformed payment event** → `customer_id` · `account_id` · `transaction_id` · `transaction_type` · `amount` · `currency` · `transaction_channel` · `risk_score` · `fraud_flag` · `AML/KYC attributes` · `event_timestamp` 

This is deliberately PII removal rather than visual masking.
