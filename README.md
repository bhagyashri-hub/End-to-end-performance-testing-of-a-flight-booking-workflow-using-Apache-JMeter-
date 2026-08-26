# End-to-End Performance Testing using Apache JMeter

## 📌 Project Overview

This project focuses on performance testing of the flight-booking web application using Apache JMeter.

The project simulates multiple concurrent users performing an end-to-end flight booking workflow and evaluates application performance using response time, throughput, percentile metrics, and error rate.

The test plan also uses CSV-based test data parameterization to simulate different source and destination cities.

---

## 🎯 Objectives

- Evaluate application performance under different user loads.
- Design and execute end-to-end performance test scenarios.
- Simulate concurrent users using Apache JMeter.
- Parameterize test data using CSV Data Set Config.
- Measure response time and throughput.
- Analyze P90, P95 and P99 response-time metrics.
- Identify and troubleshoot failed transactions.
- Document performance test results and observations.

---

## 🛠️ Tools & Technologies

- Apache JMeter 5.6.3
- Java 17
- CSV Data Set Config
- HTTP Request
- HTTP Header Manager
- HTTP Cookie Manager
- Transaction Controller
- Timers
- Assertions
- Aggregate Report
- View Results Tree
- Git & GitHub

---

## 🌐 Application Under Test

**Application:** Flight Booking Demo

The application provides a flight-search and booking workflow used for performance-testing practice.

---

## 🔄 End-to-End Test Flow

The performance test simulates the following user journey:

Home Page  
↓  
Search Flight  
↓  
Choose Flight  
↓  
Purchase Ticket  
↓  
Confirmation

---

## 📊 Test Data Parameterization

CSV-based test data is used to provide different flight source and destination combinations.

### CSV File

`CitiesCSV.csv`

### Variables

- `from`
- `to`

### JMeter Configuration

- CSV Data Set Config
- Sharing Mode: All Threads
- Recycle on EOF: True
- Stop Thread on EOF: False

Using external test data makes the performance test reusable and avoids hard-coding input values inside HTTP requests.

---

## ⚙️ Test Configuration

### Baseline Test

- Virtual Users: 5
- Ramp-up Period: 5 seconds
- Loop Count: 1

### Load Test

- Virtual Users: 25
- Ramp-up Period: 5 seconds
- Loop Count: 1

### Higher Load Test

- Virtual Users: 50
- Ramp-up Period: 10 seconds
- Loop Count: 2

A 2-second think time is configured between relevant user actions.

---

## 📈 Performance Metrics

The following metrics are collected and analyzed:

- Average Response Time
- Median Response Time
- P90 Response Time
- P95 Response Time
- P99 Response Time
- Minimum Response Time
- Maximum Response Time
- Error Percentage
- Throughput
- Data Received
- Data Sent

---

## 📋 Test Results

| Scenario | Users | Avg Response Time | P95 | Error % | Throughput |
|----------|------:|------------------:|----:|--------:|-----------:|
| Baseline | 5     | TBD               | TBD | TBD     | TBD        |
| Load     | 25    | TBD               | TBD | TBD     |  TBD       |
| Higher Load | 50 | TBD               | TBD | TBD     | TBD        |

> Replace `TBD` with the actual values obtained from JMeter Aggregate Report.

---

## 🐞 Defect / Test Script Investigation

During the initial execution, the `Purchase Ticket` transaction was reported as failed by JMeter.

### Initial Observation

- HTTP Response Code: `200`
- Application Response: Successful purchase confirmation
- JMeter Result: Failed
- Duration Assertion Threshold: `3000 ms`

Further investigation showed that the assertion was expecting a hard-coded historical date.

### Root Cause

The assertion depended on a fixed date value, while the application generated the purchase date dynamically.

This resulted in a false-negative test result.

### Resolution

The date-based validation was replaced with validation of a stable confirmation message:

`Thank you for your purchase today!`

This makes the assertion reusable across different test executions.

---

## 📊 Result Analysis

The performance results from the baseline, load, and higher-load scenarios are compared to understand how response time, throughput, and error rate change as concurrent users increase.

The analysis focuses particularly on:

- Changes in P95 response time
- Throughput behavior
- Error-rate changes
- Slowest transactions
- Transactions requiring further investigation



t.png
