---
title: Domain-Driven Architecture Overview
icon: material/domain
hide:
  - toc
---

# Domain-Driven Architecture Overview

The central problem the application solves is the *optimization of energy usage* using excess energy production (especially from renewables) by integrating Bitcoin mining. This isn't just about mining; it's about using mining as *a tool* for energy management. The core domain revolves around the intelligent automation and control of mining based on energy availability and goals.

# Domains Breakdown

This outlines a strategic categorization of subdomains according to their importance within the system. Furthermore, it details the internal composition of each subdomain, breaking it down into entities, value objects, and aggregates to clarify responsibilities and structure.

- 🟢​ **Core:** The *automation/decision logic* is central. This is where the unique value proposition lies.
- 🟣 **Supporting:** These domains are necessary for the core domain to function but aren't the primary differentiator.
- ⚫ **Generic:** These are common problems solved elsewhere, not specific to this domain.

The identified domains are:

- 🟢 [Energy Optimization & Mining Automation](#energy-optimization--mining-automation)
- 🟣 [Energy System Monitoring](#energy-system-monitoring)
- 🟣 [Mining Device Management](#mining-device-management)
- 🟣 [Home Consumption Analytics](#home-consumption-analytics)
- 🟣 [Energy Forecast](#energy-forecast)
- 🟣 [Heat Utilization](#heat-utilization)
- 🟣 [Mining Performance Analysis](#mining-performance-analysis)
- ⚫ [User Settings](#user-settings)
- ⚫ [Notification System](#notification-system)

## Energy Optimization & Mining Automation

This is the **Core** domain that captures the intelligence, making smart decisions about *when* to mine based on energy conditions.

**Components**:

- `OptimizationPolicy`: A collection of rules and goals driving the automation decisions.
- `AutomationRule`: Represents a user-defined or system rule.
- `MiningDecision`: The output of the policy (e.g., `StartMining`, `StopMining`).

## Energy System Monitoring

A **Supporting** domain focused on acquiring and structuring data from the energy plant for the core domain.

**Components**:

- `EnergyPlant`, `EnergySource`, `EnergyStorage`, `EnergyLoad` (Entities)
- `EnergyReading`, `EnergyStateSnapshot` (Value Objects)

## Mining Device Management

A **Supporting** domain for controlling ASIC miners. Executes commands from the core domain and reports miner status.

**Components**:

- `Miner`, `MiningFarm` (Entities)
- `ControlCommand` (Value Object)

## Energy Forecast

A **Supporting** domain for gathering solar/energy forecasts for the core decision logic.

**Component**:

- `ForecastData` (Value Object)

## Home Consumption Analytics

A **Supporting** domain (potentially core) providing forecasts of household energy usage.

**Components**:

- `HomeLoadsProfile`, `LoadDevice` (Entities)
- `ConsumptionForecast` (Value Object)

## Heat Utilization

A **Supporting** domain using the heat byproduct from mining. Could gain importance if heating demand drives mining.

**Components**:

- `HeatOutput`, `HeatingZone`, `TemperatureSensor` (Potential entities/VOs)

## Mining Performance Analysis

A **Supporting** domain for analyzing mining output and performance, like rewards or hashrate.

**Components**:

- `MiningSession`, `MiningReward`, `HashRate`, `PoolConnectionDetails`

## User Settings

A **Generic** domain managing system/user preferences that influence core behavior.

**Components**:

- `User`, `SystemSettings`, `NotificationPreference`

## Notification System

A **Generic** domain responsible for informing users about events.

# Context Mapping: Subdomain Interactions

Shows how subdomains interact through information exchange and action triggering.

| From (Subdomain)                    | ➡️ | To (Subdomain)                          | Data/Action Provided                              |
| ----------------------------------- | --- | --------------------------------------- | ------------------------------------------------- |
| Energy System Monitoring            | ➡️ | Energy Optimization & Mining Automation | `EnergyStateSnapshot`                             |
| External Integrations (Forecast)    | ➡️ | Energy Optimization & Mining Automation | `ForecastData`                                    |
| User Configuration & Interaction    | ➡️ | Energy Optimization & Mining Automation | User parameters for `OptimizationPolicy`          |
| Energy Optimization & Mining Auto.  | ➡️ | Mining Device Management                | `ControlCommand` (e.g., TurnOn Miner X)           |
| Mining Device Management            | ➡️ | Energy Optimization & Mining Automation | Miner status reports                              |
| Mining Device Management            | ➡️ | Mining Performance Analysis             | Uptime, possibly hashrate                         |
| External Integrations (Mining Pool) | ➡️ | Mining Performance Analysis             | `MiningReward` data                               |
| Home Consumption Analytics          | ➡️ | Energy Optimization & Mining Automation | Aggregate `ConsumptionForecast`                   |
| Monitoring Subdomains               | ➡️ | User Configuration & Interaction        | Data for display (status, performance, heat, ...) |


