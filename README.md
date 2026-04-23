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

## Parameters

This template takes a single parameter:

| Parameter | Description |
|---|---|
| `equalisOpsRegPrincipalId` | Service Principal Object ID of the Equalis OpsReg connector **in your tenant** (GUID). This is *not* the Application ID — it is the per-tenant Object ID that Azure creates when you grant admin consent to the Equalis OpsReg connector app. |

**How this gets filled in:**

- **From the Equalis onboarding wizard** (recommended): the wizard launches this template and supplies the `equalisOpsRegPrincipalId` value automatically. You don't need to look it up.
- **Manual deployment**: if you're deploying this template outside the wizard, find your tenant's Object ID in the Azure Portal → **Microsoft Entra ID** → **Enterprise applications** → search for "Equalis OpsReg" → copy the **Object ID** field on the Overview page.

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
4. Review the `equalisOpsRegPrincipalId` value shown in the portal. If deploying from the Equalis wizard, this is pre-filled — proceed. If deploying manually, paste the Object ID you retrieved from Enterprise applications → Equalis OpsReg → Object ID. Do not paste the Application ID (a common mistake — the Application ID is the same across all tenants; the Object ID is unique to yours).
5. Click **Review + create**, then **Create**
6. Return to [app.equalisopsreg.com](https://app.equalisopsreg.com) and click **Verify Connection**

Deployment takes approximately 30 seconds.

## Upgrading from an earlier deployment

If you previously deployed an earlier version of this template, the role assignments it created were bound to an invalid principal and never functioned. Deploying the current template creates new, correctly-bound role assignments with different names — the old ones are harmless but should be removed for cleanliness:

1. Azure Portal → **Subscriptions** → select your subscription → **Access control (IAM)** → **Role assignments**
2. Filter by role: **Reader**, **Security Reader**, **Cost Management Reader**
3. Any assignment where the principal shows as "Identity not found" or an unresolved GUID is an old broken assignment — remove it
4. The assignments from the current template will show "Equalis OpsReg" as the resolved principal — keep those

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
