# devops-database

## Overview
This repository contains the database component for the DevOps final project e-commerce platform.

## Responsibilities
- Store persistent application data
- Provide the database initialization script
- Support backend services with structured data storage

## Tech Stack
- PostgreSQL
- SQL

## Branching Strategy
This repository follows the Git Flow model:
- `main`: production-ready code
- `develop`: integration branch for ongoing development
- `feature/*`: new features
- `release/*`: release preparation
- `hotfix/*`: urgent production fixes

## Getting Started
### Prerequisites
- PostgreSQL

### Initialize database
Use the provided SQL script to initialize the database:

```bash
psql -U postgres -d ecommerce -f init.sql
