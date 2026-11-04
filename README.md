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
