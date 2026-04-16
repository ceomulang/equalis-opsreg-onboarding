# Equalis OpsReg — Connect Your Azure Subscription

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fceomulang%2Fequalis-opsreg-onboarding%2Fmain%2Fazuredeploy.json)

## What this does

This ARM template grants **Equalis OpsReg** read-only access to your Azure subscription for compliance monitoring. Three built-in Azure roles are assigned:

| Role | Purpose |
|---|---|
| **Reader** | Scans your Azure resources via Resource Graph for compliance evaluation |
| **Security Reader** | Reads Microsoft Defender for Cloud security posture and findings |
| **Cost Management Reader** | Reads cost and billing data for FinOps spend analysis |

## What this does NOT do

- Does **not** create any resources in your subscription
- Does **not** modify any infrastructure or configuration
- Does **not** have write access to anything
- Does **not** store any credentials — uses Azure's built-in role-based access

## Compliance frameworks

Equalis OpsReg evaluates your Azure resources against:

- GDPR (General Data Protection Regulation)
- ISO 27001 (Information Security Management)
- NIS2 (Network and Information Security Directive)
- DORA (Digital Operational Resilience Act)
- PCI-DSS (Payment Card Industry Data Security Standard)

## How to deploy

1. Click the **Deploy to Azure** button above
2. Sign in to the Azure portal with your organizational account
3. Select the subscription you want to connect
4. Click **Review + create**, then **Create**
5. Return to [app.equalisopsreg.com](https://app.equalisopsreg.com) and click **Verify Connection**

Deployment takes approximately 30 seconds.

## How to revoke access

To disconnect Equalis OpsReg from your subscription:

1. Go to the Azure portal → **Subscriptions** → select your subscription
2. Click **Access control (IAM)** → **Role assignments**
3. Search for "Equalis OpsReg" in the description
4. Select the 3 role assignments and click **Remove**

## Support

- Website: [equalisopsreg.com](https://equalisopsreg.com)
- Email: support@equalisopsreg.com

## About Equalis OpsReg

Equalis OpsReg is an inform-only compliance platform. It detects violations and provides remediation guidance but **never modifies your environment**.

Equalis OpsReg Ltd | Dublin, Ireland
