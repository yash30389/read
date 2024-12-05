# Default Infra Setup Guide

## Overview
This guide provides steps to set up the infrastructure for StackSet deployment across tenant and brand workload account's. The setup includes generating project's, synthesizing infrastructure code, deploying StackSet's and adding parameters to ParameterStore for each account.


### Deploy Default Infra
To deploy the default infrastructure, execute the following command:
```bash
npx nx deploy default-infra --configuration=unstable --require-approval never --profile devopsaccount
```

---------

# Steps for stackset deploy on tenant and brand account's

## Step 1: Generate StackSet Wrapper
Generate the StackSet wrapper's for deployment of stackset.

```bash
npx nx generate @ago-dev/nx-aws-cdk-v2:application --name genera-tenant-stackset-wrapper
npx nx generate @ago-dev/nx-aws-cdk-v2:application --name genera-brand-stackset-wrapper
```

## step 2: Generate Workload Infra Assets
Generate "genera-tenant-workload-infra-assets","genera-brand-workload-infra-assets" for synth and deploy.

Install required pacjages:

```bahs
npm install @stellarlibs/nx-cdk
```

Projects generation command:
```bash
npx nx generate @stellarlibs/nx-cdk:app --name genera-tenant-workload-infra-assets
npx nx generate @stellarlibs/nx-cdk:app --name genera-brand-workload-infra-assets
```

# Prerequisites

We need to pass the required parameters while creating the tenant and brand account's.

| **Parameter Path**                  |**Parameterstore values in code** |  **Description**                                 |
|-------------------------------------|----------------------------------|--------------------------------------------------|
| `/genera/tenant/tenantId`           | `companyid`                      | Unique identifier for the tenant                 |
| `/genera/tenant/tenantName`         | `companyname`                    | Name of the tenant                               |
| `/genera/tenant/tenantaccountid`    | `accounttenantid`                | AWS Tenant account ID                            |
| `manageraccountid`                  | `accounttenantid`                | AWS Manager account ID                           |
| `/genera/brand/ClientName`          | `clientname`                     | Name of the client                               |
| `/genera/brand/ClientId`            | `clientid`                       | Unique identifier for the client                 |
| `/genera/brand/BrandName`           | `brandname`                      | Name of the brand                                |
| `/genera/brand/BrandId`             | `brandid`                        | Unique identifier for the brand                  |
| `/genera/brand/brandaccountid`      | `accountbrandid`                 | Brand account ID                                 |


----
## Step 3: Synthesize and Deploy Workloads

# Tenant Workload
## Synthesize the infrastructure:
```bash
npx nx synth genera-tenant-workload-infra-assets
```

## Publish the assets on devops accounts:
```bash
npx cdk-assets publish --path dist/packages/genera-tenant-workload-infra-assets/tenant-workload.assets.json --profile devopsaccount
```

## Deploy the StackSet wrapper:
```bash
npx nx deploy genera-tenant-stackset-wrapper --require-approval never --profile devopsaccount
```

# Brand Workload
## Synthesize the infrastructure:
```bash
npx nx synth genera-brand-workload-infra-assets
```

## Publish the assets:
```bash
npx cdk-assets publish --path dist/packages/genera-brand-workload-infra-assets/brand-workload.assets.json --profile devopsaccount
```

## Deploy the StackSet wrapper:
```bash
npx nx deploy genera-brand-stackset-wrapper --require-approval never --profile devopsaccount
```

