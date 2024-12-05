

# Default Infra Setup Guide
## Overview
This guide provides steps to set up the infrastructure for StackSet deployment across tenant and brand workload accounts using NX and AWS CDK. The setup includes generating projects, synthesizing infrastructure code, deploying StackSets, and adding parameters to Parameter Store for each account.

## Commands

### Deploy Default Infra
To deploy the default infrastructure, execute the following command:
```bash
npx nx deploy default-infra --configuration=unstable --require-approval never --profile AWSAdministratorAccess-149536462679
```

---

# Steps for stackset deploy on tenant and brand account's

## Step 1: Generate StackSet Wrapper Projects
Generate the StackSet wrapper projects for deployment on each tenant and brand workload's.

Commands:
```bash
npx nx generate @ago-dev/nx-aws-cdk-v2:application --name genera-tenant-stackset-wrapper
npx nx generate @ago-dev/nx-aws-cdk-v2:application --name genera-brand-stackset-wrapper
```

## step-2:
-------
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

for synth tenant and brnad workloads

tenant command:
```bash
npx nx synth genera-tenant-workload-infra-assets
npx cdk-assets publish --path dist/packages/genera-tenant-workload-infra-assets/tenant-workload.assets.json --profile AWSAdministratorAccess-{devopsaccount's}
npx nx deploy genera-tenant-stackset-wrapper --require-approval never --profile AWSAdministratorAccess-149536462679
```

brand command:
```bash
npx nx synth genera-brand-workload-infra-assets
npx cdk-assets publish --path dist/packages/genera-brand-workload-infra-assets/brand-workload.assets.json --profile AWSAdministratorAccess-{devopsaccount's}
npx nx deploy genera-brand-stackset-wrapper --require-approval never --profile AWSAdministratorAccess-149536462679
```
