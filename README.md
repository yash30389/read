# Default Infra Setup Guide

## Overview
This guide provides steps to set up the infrastructure for StackSet deployment across tenant and brand workload accounts using NX and AWS CDK. The setup includes generating projects, synthesizing infrastructure code, deploying StackSets, and adding parameters to Parameter Store for each account.

---

## Commands

### Deploy Default Infra
To deploy the default infrastructure, execute the following command:
```bash
npx nx deploy default-infra --configuration=unstable --require-approval never --profile AWSAdministratorAccess-149536462679
