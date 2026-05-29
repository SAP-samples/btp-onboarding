# Enhance SAP Joule for Consultants with Custom Knowledge Grounding

## 1. Introduction

### 1.1 Overview

#### 1.1 a) What Custom Knowledge Grounding Does

Custom Knowledge Grounding extends SAP Joule for Consultants with your organization's own documents. The documents are uploaded to a data repository, indexed by SAP AI Core Document Grounding, and retrieved at runtime to ground SAP Joule for Consultants' answers. Users get responses that combine the SAP-curated content SAP Joule for Consultants ships with and their firm's own methodologies, policies, and delivery standards.

![Solution diagram showing documents flowing from a data repository through SAP AI Core Document Grounding into SAP Joule for Consultants](1-introduction/images/solution-diagram.png)

#### 1.1 b) Prerequisites

- **SAP Joule for Consultants** — an existing instance. See [Onboarding Guide for SAP Joule for Consultants | SAP Help Portal](https://help.sap.com/docs/joule/serviceguide/provisioning-sap-joule-for-consultants).
- **SAP AI Core with the `extended` plan** — required by Document Grounding. See [SAP AI Core — SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/sap-ai-core).
- **Object Store** (recommended for the initial setup) — the simplest data repository to start with, and the example used throughout this guide. See [Object Store — SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/object-store).

#### 1.1 c) Pricing

Custom Knowledge Grounding relies on paid SAP services that are billed separately from SAP Joule for Consultants:

- **SAP AI Core (`extended` plan)** is mandatory. Charges accrue per document indexed and per token retrieved — see the [Generative AI Hub in SAP AI Core Calculator](https://ai-core-calculator.cfapps.eu10.hana.ondemand.com/uimodule/index.html) and [Pricing](https://discovery-center.cloud.sap/serviceCatalog/sap-ai-core?region=all&tab=service_plan).
- **Object Store (`standard` plan)** if you take the recommended setup path. See [Pricing](https://discovery-center.cloud.sap/serviceCatalog/object-store?service_plan=standard&region=all&commercialModel=btpea&tab=service_plan).
- **SAP AI Launchpad (`standard` plan)** is optional — needed only if you prefer the UI-driven setup over the REST API path. See [Pricing](https://discovery-center.cloud.sap/serviceCatalog/sap-ai-launchpad?region=all&tab=service_plan).

Review the pricing of each service before subscribing.

#### 1.1 d) What This Guide Covers

The remaining sections walk through the end-to-end setup:

- **[2. Data Repositories](#2-data-repositories)** — pick a supported data repository (e.g., Object Store, Microsoft SharePoint, or SAP Build Work Zone) and upload your documents to it.
- **[3. AI Core Document Grounding](#3-ai-core-document-grounding)** — provision SAP AI Core with the `extended` plan, then create a pipeline that ingests, chunks, embeds, and indexes the documents.
- **[4. Connection to SAP Joule for Consultants](#4-connection-to-sap-joule-for-consultants)** — configure a Destination Service instance, then enable Custom Knowledge Grounding in the SAP Joule for Consultants Console and connect it to the pipeline.
- **[5. Testing](#5-testing)** — verify the setup by asking SAP Joule for Consultants a question whose answer is only available in your uploaded documents.

> **Note:** Depending on what is already in place — an existing AI Core Document Grounding pipeline, ready-to-use data repository credentials, or neither — you may be able to skip directly to a later section. The next section, [1.2 Recommendations](#12-recommendations), opens with a decision tree for choosing the right entry point and then covers data repository choice and subaccount layout.

### 1.2 Recommendations

#### 1.2 a) Where to Start

Not every reader has to work through every section of this guide. Use the decision tree below to pick the entry point that matches what you already have in place:

- **An AI Core Document Grounding pipeline is already provisioned** (resource group, generic secret, and a pipeline reporting `FINISHED` against the data repository you intend to use) → skip ahead to the [4. Connection to SAP Joule for Consultants](#4-connection-to-sap-joule-for-consultants) section, starting with [4.1 Destination Service setup](#41-destination-service-setup). Configure the Destination Service against the existing pipeline and enable Custom Knowledge Grounding in the SAP Joule for Consultants Console.
- **The data repository credentials are already available** (e.g., a SharePoint site with the Entra app registered, an S3 bucket, or a Work Zone tenant with Document Grounding enabled) and you have run an AI Core Document Grounding setup before → skip the [2. Data Repositories](#2-data-repositories) section and start with the [3. AI Core Document Grounding](#3-ai-core-document-grounding) section.
- **Neither of the above applies** → start at the [2. Data Repositories](#2-data-repositories) section with [2.2 Object Store](#22-object-store), as described below. It is the fastest path to a working setup and the one the rest of this guide uses as the running example.

#### 1.2 b) Start with Object Store

Custom Knowledge Grounding can read from any of the [supported data repositories](https://help.sap.com/docs/sap-ai-core/generative-ai/grounding-035c455a5a424697b60f4a24b6d791fe#data-repositories). For the **initial setup**, Object Store is the recommended choice:

- **Fast activation** — the Object Store instance is provisioned by a booster and ready in minutes. SharePoint, customer-managed S3, and Work Zone setups often take longer than anticipated because of onboarding complications, approval, and security processes.
- **Very low cost** — Object Store charges are small. Even when run for a few months until the target data repository is ready, the extra cost is negligible — see [Pricing](https://discovery-center.cloud.sap/serviceCatalog/object-store?service_plan=standard&region=all&commercialModel=btpea&tab=service_plan).
- **Reversible** — once the target data repository is online and indexed, point Custom Knowledge Grounding at the new pipeline and decommission the Object Store instance.

The key advantage is that Custom Knowledge Grounding can be live in SAP Joule for Consultants while the longer-running setup of your target data repository runs in parallel — instead of blocking the entire rollout on it.

> **Note:** The Object Store instance must be provisioned in an AWS-based subaccount, since AI Core Document Grounding consumes it through the AWS S3 API.

> **Note:** Answers themselves are generated the same way regardless of the data repository. Source citations are clickable for SharePoint and Work Zone — they link back to the original file. For Object Store and the other repositories, citations show the document name and page reference but do not resolve to the file.

#### 1.2 c) Subaccount Layout and Existing Instances

The four moving parts — **Object Store** (or any other data repository), **SAP AI Core**, **Destination Service**, and **SAP Joule for Consultants** — communicate through service-key credentials, which allows for very flexible placement: they can all sit in the same subaccount, in different subaccounts, or even in different global accounts.

- **Reuse existing instances** where available. If your organization already runs SAP AI Core (with the `extended` plan) or SAP AI Launchpad in another subaccount, you can reuse them instead of provisioning new instances.
- The **Destination Service** can be deployed in the SAP Joule for Consultants subaccount or in the AI Core subaccount. In general, it is recommended to place it in the same subaccount as the consuming application—in this case, the SAP Joule for Consultants subaccount.
- The **Object Store** must live in an AWS-based subaccount (see above). The SAP Joule for Consultants subaccount is a convenient option, since it runs on AWS data centers.

## 2. Data Repositories

### 2.1 Data Repositories - Overview

#### 2.1 a) What a Data Repository Provides

AI Core Document Grounding does not host the source documents itself — it reads them from an external data repository and serves the resulting index to SAP Joule for Consultants. The data repository is the system of record where you upload and maintain the documents you want to ground SAP Joule for Consultants' answers on.

The starting point for the AI Core Document Grounding documentation is [Grounding | SAP Help Portal](https://help.sap.com/docs/sap-ai-core/generative-ai/grounding-035c455a5a424697b60f4a24b6d791fe).

#### 2.1 b) Supported Data Repositories

AI Core Document Grounding can read content from the following data repositories:

- Microsoft SharePoint
- AWS S3
- SFTP
- SAP Build Work Zone
- SAP Document Management service
- ServiceNow
- Google Drive

Setup steps for Google Drive, Microsoft SharePoint, SAP Build Work Zone, and ServiceNow (SNOW) are described on [Set Up Data Repository Integration | SAP Help Portal](https://help.sap.com/docs/joule/integrating-joule-with-sap/prepare-sharepoint-integration).

> **Note:** That help page is written for Document Grounding with **SAP Joule for Business**. Only the data repository setup instructions apply here — the remaining content on the page is specific to SAP Joule for Business and is not relevant for SAP Joule for Consultants.

The next subsections walk through the setup of three data repositories in more detail:

- [**2.2 Object Store**](#22-object-store)
- [**2.3 Microsoft SharePoint**](#23-microsoft-sharepoint)
- [**2.4 SAP Build Work Zone**](#24-sap-build-work-zone)

The three subsections are independent — pick the repository (or repositories) you want to use and skip the others. For any data repository not covered here, refer to the SAP Help pages linked above.

### 2.2 Object Store

#### 2.2 a) Provision the Object Store Service

The Object Store provides S3-compatible storage where documents are uploaded for AI Core Document Grounding to index. Begin by verifying the entitlement at the global account and adding the service plan to your subaccount.

> **Note:** Create the Object Store in an AWS-based subaccount; the steps below assume an AWS backend.

- At the global account level, open **Entitlements** → **Service Assignments**.
- Search for `Object Store` and confirm the `standard` plan is assigned.

![Service assignments screen with the Object Store standard plan highlighted](2-data-repositories/images/service-assignments.png)

- In your subaccount, open **Entitlements** and click **Edit**.
- Click **Add Service Plans**, select **Object Store**, check the `standard` plan, and click **Add 1 Service Plan**.
- Click **Save** to apply the changes.

![Object Store standard service plan added to the subaccount entitlements](2-data-repositories/images/object-store-service-plan.png)

#### 2.2 b) Set Up the Cloud Foundry Environment

The Object Store instance runs in the Cloud Foundry runtime, so the subaccount must have Cloud Foundry enabled and a space available to host the instance.

- In your subaccount, open **Overview** and click **Enable Cloud Foundry**.
- Keep the **Cloud Foundry Runtime** environment and `standard` plan, adjust the **Instance Name** and **Org Name** if needed, then click **Create**.

![Enable Cloud Foundry dialog with the standard plan selected](2-data-repositories/images/cloud-foundry.png)

- Once Cloud Foundry is enabled, click **Create Space** on the **Cloud Foundry Environment** tab.
- Enter a space name (for example, `j4c`), assign yourself the **Space Developer** and **Space Manager** roles, and click **Create**.

![Cloud Foundry space creation dialog with j4c entered as the space name and Space Developer and Space Manager roles assigned](2-data-repositories/images/cf-space.png)

#### 2.2 c) Create the Object Store Instance

- In your subaccount, open **Instances and Subscriptions** and click **Create**.
- Fill in the required fields:
  - **Service:** `Object Store`
  - **Plan:** `standard`
  - **Runtime Environment:** `Cloud Foundry`
  - **Space:** the space you created (e.g., `j4c`)
  - **Instance Name:** e.g., `j4c-object-store`
- Click **Create** to provision the instance.

![Object Store instance creation form with the standard plan and Cloud Foundry runtime selected](2-data-repositories/images/object-store-creation.png)

- Click on the instance row to open its details panel on the right.
- Under **Service Keys**, click **Create**.
- Enter a name (e.g., `j4c-object-store-sk`) and click **Create**.

![Service key creation dialog for the Object Store instance](2-data-repositories/images/object-store-service-key.png)

- Once the key's **Status** shows **Created**, click the **...** menu on the service key row and choose **Download** to save the credentials as a JSON file. You can also choose **View** to inspect them in the browser and copy individual values.

![Service key context menu showing the Download option](2-data-repositories/images/object-store-service-key-download.png)

> **Note:** The service key contains the `access_key_id`, `secret_access_key`, `region`, and `bucket` values needed to upload documents — you'll use them in the next step.

#### 2.2 d) Upload Documents with the AWS CLI

With the service key credentials, you can use the AWS CLI to upload documents to the Object Store bucket. AI Core Document Grounding will then index these documents for retrieval.

- Install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) if it isn't already on your machine.

> **Note:** If you prefer a graphical client, [Cyberduck](https://cyberduck.io/download/) supports S3 with the same service key credentials.

- Download the sample file [Test_document--Heliotrope_Fabricator.pdf](assets/Test_document--Heliotrope_Fabricator.pdf?raw=true). You can append `--Object-Store` to the filename (e.g., `Test_document--Heliotrope_Fabricator--Object-Store.pdf`) to mark which storage backend the copy belongs to.
- Run `aws configure` and paste in the credentials when prompted — the default output format can be left blank.
- Upload the document to the bucket and list its contents to verify:

  ```bash
  aws s3 cp <file> s3://<bucket>
  aws s3 ls s3://<bucket>
  ```

![AWS CLI terminal showing a successful s3 cp upload followed by an s3 ls listing](2-data-repositories/images/aws-cli-dark.png)

> **Note:** The bucket name in the service key is prefixed with `hcp-` followed by a unique identifier.

### 2.3 Microsoft SharePoint

> **Disclaimer:** The steps below are a reference. Coordinate with your SharePoint administrator and validate against the documentation below.
> - [Set Up Data Repository Integration | SAP Help Portal](https://help.sap.com/docs/joule/integrating-joule-with-sap/prepare-sharepoint-integration#microsoft-sharepoint) — the official SAP guidance for this setup. It is written for SAP Joule for Business, but the data repository setup steps apply here as well.
> - [Understanding Resource Specific Consent for Microsoft Graph and SharePoint Online | Microsoft Learn](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins-modernize/understanding-rsc-for-msgraph-and-sharepoint-online) — Microsoft's reference on the Resource Specific Consent permission model that the steps below rely on.

#### 2.3 a) Register the Microsoft Entra Application

AI Core Document Grounding connects to a SharePoint site through a Microsoft Entra application using the OAuth2ClientCredentials flow. Start by registering the application in Microsoft Entra.

- Sign in to [entra.microsoft.com](https://entra.microsoft.com/) with an account that can register applications.
- Open **App registrations** and click **New registration**.
- Enter a name (e.g., `j4c-sharepoint-grounding`), keep the default settings, and click **Register**.
- From the **Overview** tab, copy the **Application (client) ID** and the **Directory (tenant) ID** — you'll need both for the [3. AI Core Document Grounding](#3-ai-core-document-grounding) section.

![Microsoft Entra app registration Overview tab showing the Application (client) ID and Directory (tenant) ID](2-data-repositories/images/sharepoint-app-registration-overview.jpeg)

#### 2.3 b) Grant the Sites.Selected Permission

The application needs the `Sites.Selected` Microsoft Graph permission. On its own, this permission grants access to **zero** SharePoint sites — it only makes the application eligible to be granted access to specific sites in a later step. This is intentional and enforces least-privilege.

- In the registered application, open **API permissions** and click **Add a permission**.
- Select **Microsoft Graph** → **Application permissions**.
- Search for `Sites.Selected`, check it, and click **Add permissions**.

> **Note:** Use the `Sites.Selected` permission listed under **Microsoft Graph** — not the one with the same name listed under **SharePoint**. They are different resources, and AI Core Document Grounding consumes Microsoft Graph.

- Click **Grant admin consent for [Your Org]**. A tenant Global Administrator or Privileged Role Administrator must perform this step.
- Verify that the **Status** column for `Sites.Selected` shows a green check mark.

![API permissions tab showing Sites.Selected granted with a green check mark in the Status column](2-data-repositories/images/sharepoint-api-permissions.jpeg)

#### 2.3 c) Create a Client Secret

The OAuth2ClientCredentials flow authenticates with a client secret instead of a user sign-in.

- In the registered application, open **Certificates & secrets** and click **New client secret**.
- Enter a description, pick an expiry, and click **Add**.
- Copy the secret **Value** immediately — it is only displayed once. Store it together with the tenant ID and application ID.

![Certificates & secrets tab showing a newly created client secret with the Value column highlighted](2-data-repositories/images/sharepoint-client-secret.jpeg)

#### 2.3 d) Link the Application to the SharePoint Site

After admin consent, the application still cannot read any site. You now have to bind it explicitly to the SharePoint site that hosts your grounding documents. The easiest path is the [PnP.PowerShell](https://pnp.github.io/powershell/) module.

> **Note:** The account running the grant command must have the **Site Collection Administrator** role on the target SharePoint site (a tenant Global Administrator works as well). Owners of the Microsoft 365 Group or Teams team that backs a SharePoint site automatically have this role. If you don't have it, ask a SharePoint administrator to grant it temporarily. `Sites.Selected` on its own is not enough to perform the grant.

- Install **PowerShell 7.2 or later** — see [Install PowerShell on Windows, Linux, and macOS | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell).
- Install the PnP.PowerShell module — see [Installing PnP PowerShell | PnP PowerShell](https://pnp.github.io/powershell/articles/installation.html).
- On first use in the tenant, register PnP's own Entra application by running `Register-PnPEntraIDApp` and following the prompts. The resulting **Client ID** is the helper-app ID used to sign in with `Connect-PnPOnline` — it is **not** the ID of the application you registered in the previous sections.

> **Note:** `Register-PnPEntraIDApp` is a one-time setup per tenant. Skip it if PnP.PowerShell has already been initialized.

- Sign in to the target SharePoint site and grant the Sites.Selected application read access:

  ```powershell
  Connect-PnPOnline -Url "<site-url>" -Interactive -ClientId "<pnp-helper-app-client-id>"
  Grant-PnPAzureADAppSitePermission `
      -AppId "<sites-selected-app-client-id>" `
      -DisplayName "<display-name>" `
      -Site "<site-url>" `
      -Permissions Read
  ```

  Replace `<site-url>` with the full SharePoint site URL (e.g., `https://contoso.sharepoint.com/sites/KnowledgeBase`), `<pnp-helper-app-client-id>` with the helper-app client ID from `Register-PnPEntraIDApp`, and `<sites-selected-app-client-id>` with the **Application (client) ID** of the application you registered for AI Core Document Grounding.

- A successful response prints the permission ID, the granted role (`read`), and the application identity.

> **Note:** `Read` is sufficient for AI Core Document Grounding. The same grant can also be issued through a Microsoft Graph `POST /sites/{site-id}/permissions` call — see [Understanding Resource Specific Consent for Microsoft Graph and SharePoint Online | Microsoft Learn](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins-modernize/understanding-rsc-for-msgraph-and-sharepoint-online) for the REST equivalent.

#### 2.3 e) Upload Documents to the SharePoint Site

- Open the SharePoint site in a browser and upload your documents to a document library.
- Download the sample file [Test_document--Heliotrope_Fabricator.pdf](assets/Test_document--Heliotrope_Fabricator.pdf?raw=true). You can append `--SharePoint` to the filename (e.g., `Test_document--Heliotrope_Fabricator--SharePoint.pdf`) to mark which storage backend the copy belongs to.

The Bruno and AI Launchpad subsections in the [3. AI Core Document Grounding](#3-ai-core-document-grounding) section consume the following SharePoint credentials, which you have now collected:

- `MS_Entra_Tenant_ID` — **Directory (tenant) ID** from the Overview tab.
- `MS_Entra_Application_ID` — **Application (client) ID** from the Overview tab.
- `MS_Entra_Application_Client_Secret` — the secret value copied from **Certificates & secrets**.
- `SharePoint_URL` — the full URL of the SharePoint site you granted permission on.

#### 2.3 f) Troubleshooting

The [Troubleshooting Document Grounding Pipelines | SAP Community](https://community.sap.com/t5/technology-blog-posts-by-sap/troubleshooting-document-grounding-pipelines/ba-p/14227725) blog walks setup failures down in three steps:

- Step 1 — Validate access to the Document Grounding API.
- Step 2 — Validate SharePoint credentials.
- Step 3 — Validate pipeline configuration.

Especially noteworthy are the checks for step 3:

- **SharePoint site identifier.** Use the **identifier** from the site URL (e.g., `HR%20Team` for `https://contoso.sharepoint.com/sites/HR%20Team`), not the human-readable site title. Mind the URL encoding.
- **Include paths.** Match the URL path of the folder you want to ground on, relative to the document library — `/teched`, not `/Shared%20Documents/teched`.
- **Pipeline created but no documents.** Almost always means the include path is too narrow. Test with no include path first; once replication works, narrow it down.

### 2.4 SAP Build Work Zone

#### 2.4 a) Provision SAP Build Work Zone, Advanced Edition

Document Grounding is available in SAP Build Work Zone, advanced edition across all plans. Provision the tenant if you don't already have one.

- Follow the [Onboarding to SAP Build Work Zone, advanced edition | SAP Help Portal](https://help.sap.com/docs/build-work-zone-advanced-edition/sap-build-work-zone-advanced-edition/onboarding-to-sap-build-work-zone-advanced-edition) guide.
- The community post [SAP Build Work Zone: advanced edition — step-by-step configuration | SAP Community](https://community.sap.com/t5/technology-blog-posts-by-members/sap-build-workzone-advanced-edition-step-by-step-configuration/ba-p/13548498) covers the same ground with screenshots and may be easier to follow on a first pass.

#### 2.4 b) Enable Document Grounding on the Work Zone Tenant

Once the Work Zone tenant is up, enable Document Grounding so AI Core can ingest its content, and collect the OAuth credentials AI Core will use to read it.

- Follow [Integration With Document Grounding | SAP Help Portal](https://help.sap.com/docs/build-work-zone-advanced-edition/sap-build-work-zone-advanced-edition/integration-with-document-grounding).
- The community blog [Joule — Document Grounding with SAP Build Work Zone, advanced edition | SAP Community](https://community.sap.com/t5/technology-blog-posts-by-sap/joule-document-grounding-with-sap-build-work-zone-advanced-edition-rag/ba-p/14260070) walks through the same enablement end-to-end.

> **Note:** Stop after **Step 3** of the community blog. **Step 4: Use an Existing Joule Subaccount or Create a New One to Set Up Document Grounding** is replaced by the AI Core Document Grounding setup in the [3. AI Core Document Grounding](#3-ai-core-document-grounding) section of this guide — the Destination Service and SAP Joule for Consultants Console steps later on perform the equivalent integration for SAP Joule for Consultants.

#### 2.4 c) Upload Documents to Work Zone

- In the Work Zone workspace configured for Document Grounding, upload your documents to the workspace folder.
- Download the sample file [Test_document--Heliotrope_Fabricator.pdf](assets/Test_document--Heliotrope_Fabricator.pdf?raw=true). You can append `--Work-Zone` to the filename (e.g., `Test_document--Heliotrope_Fabricator--Work-Zone.pdf`) to mark which storage backend the copy belongs to.

The Bruno and AI Launchpad subsections in the [3. AI Core Document Grounding](#3-ai-core-document-grounding) section consume the following Work Zone credentials, which you collected during the Document Grounding enablement above:

- `DWS_URL` — the URL of the Work Zone tenant.
- `OAuthClient_Key` — the OAuth client key.
- `OAuthClient_Secret` — the OAuth client secret.

#### 2.4 d) Support

Issues specific to the Work Zone side of this setup — Document Grounding capability, OAuth configuration, content not appearing in the workspace folder — belong to support component `EP-WZ-STA`. Issues with the AI Core pipeline that reads from Work Zone (indexing, embeddings, pipeline status) belong under `CA-ML-RAGE`. The [3.5 Support](#35-support) subsection later in the next section has the full breakdown.

## 3. AI Core Document Grounding

### 3.1 AI Core Document Grounding - Overview

#### 3.1 a) What AI Core Document Grounding Does

SAP AI Core Document Grounding reads documents from a data repository, chunks them, generates embeddings, and stores them in a vector index. SAP Joule for Consultants queries that index at runtime to ground its answers in your organization's own content.

> **Note:** For a conceptual introduction to what happens inside that pipeline — vector embeddings, the SAP HANA Cloud vector engine, and how data ingestion, orchestration, and retrieval fit together in the Generative AI Hub — see the [Analyzing Document Grounding in Generative AI Hub | SAP Learning](https://learning.sap.com/courses/using-advance-ai-techniques-with-sap-s-generative-ai-hub/analyzing-document-grounding-in-generative-ai-hub) lesson. It is theoretical background, not setup instructions, and complements the hands-on subsections that follow.

#### 3.1 b) What the Rest of This Section Covers

The next subsections walk through the setup of SAP AI Core Document Grounding. The instructions in both the Bruno and AI Launchpad subsections use the Object Store as the example data repository:

- **[3.2 AI Core instance creation](#32-ai-core-instance-creation)** — provision SAP AI Core with the `extended` plan via the AI Core booster, and download the service key.
- **[3.3 AI Core Document Grounding with Bruno](#33-ai-core-document-grounding-with-bruno)** — create the resource group, generic secret, and pipeline through the REST API using an importable Bruno collection.
- **[3.4 AI Core Document Grounding with AI Launchpad](#34-ai-core-document-grounding-with-ai-launchpad)** — an alternative path that performs the same setup through a UI instead of the REST API.
- **[3.5 Support](#35-support)** — where to open tickets when something goes wrong.

> **Note:** The Bruno and AI Launchpad subsections are two interchangeable paths to the same outcome. Bruno is a free, open-source API client; SAP AI Launchpad is an alternative UI-driven route that requires a paid subscription.

#### 3.1 c) Pricing

SAP AI Core offers a free plan, but Document Grounding requires the `extended` plan, which is a paid subscription. Charges accrue per document indexed and per token retrieved, and are billed separately from SAP Joule for Consultants. Review the pricing before subscribing:

- [SAP AI Core — SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/sap-ai-core)
- [Generative AI Hub in SAP AI Core Calculator](https://ai-core-calculator.cfapps.eu10.hana.ondemand.com/uimodule/index.html)

If you take the AI Launchpad path, note that SAP AI Launchpad with the `standard` plan is also a paid subscription: [SAP AI Launchpad — SAP Discovery Center](https://discovery-center.cloud.sap/serviceCatalog/sap-ai-launchpad).

#### 3.1 d) Supported Data Repositories

AI Core Document Grounding can index content from the following data repositories:

- Microsoft SharePoint
- AWS S3
- SFTP
- SAP Build Work Zone
- SAP Document Management service
- ServiceNow
- Google Drive

Bruno collections are provided for AWS S3, Microsoft SharePoint, and SAP Build Work Zone (see the next subsection). For the other data repositories, refer to the SAP documentation:

- [Orchestration (V2) with Grounding Capabilities in SAP AI Core | SAP Tutorials](https://developers.sap.com/tutorials/ai-core-orchestration-grounding-v2.html)
- [Generic Secrets for Grounding | SAP Help Portal](https://help.sap.com/docs/sap-ai-core/generative-ai/generic-secrets-for-grounding-e1a201c1fc2e4eb3a570efd81a3b3616)
- [Create a Document Grounding Pipeline Using the Pipelines API | SAP Help Portal](https://help.sap.com/docs/sap-ai-core/generative-ai/create-document-grounding-pipeline-using-pipelines-api-d32b1465461149749b00129c02e05142)

#### 3.1 e) Credentials Required for the Next Steps

Every Bruno collection expects the **AI Core service key** values. In addition, each data repository needs its own credentials and ships with its own collection.

##### AWS S3

Bruno collection: [aicore-dg-s3.yml](assets/aicore-dg-s3.yml?raw=true)

- `S3_Region`, `S3_Host`, `S3_Bucket`, `S3_Username`, `S3_Access_Key_ID`, `S3_Secret_Access_Key`

> **Note:** This collection works with any AWS S3 source. When using SAP BTP Object Store (as in the Bruno and AI Launchpad subsections), the values are taken from the Object Store service key.

##### Microsoft SharePoint

Bruno collection: [aicore-dg-sharepoint.yml](assets/aicore-dg-sharepoint.yml?raw=true)

- Microsoft Entra application: `MS_Entra_Tenant_ID`, `MS_Entra_Application_ID`, `MS_Entra_Application_Client_Secret`
- SharePoint site: `SharePoint_URL`

##### SAP Build Work Zone

Bruno collection: [aicore-dg-workzone.yml](assets/aicore-dg-workzone.yml?raw=true)

- Advanced Work Zone: `DWS_URL`, `OAuthClient_Key`, `OAuthClient_Secret`

#### 3.1 f) Test Documents

Sample documents are provided to verify the end-to-end setup. Each file contains fictional content written with unique terminology, and the matching **test prompt is included on the first page** of the document so you can copy it straight into SAP Joule for Consultants. Upload at least one to your data repository:

- [Test_document--Aurora_Phase_Conductor.pdf](assets/Test_document--Aurora_Phase_Conductor.pdf?raw=true)
- [Test_document--Heliotrope_Fabricator.pdf](assets/Test_document--Heliotrope_Fabricator.pdf?raw=true)
- [Test_document--Obsidian_Flux_Harmonizer.pdf](assets/Test_document--Obsidian_Flux_Harmonizer.pdf?raw=true)
- [Test_document--Verdant_Chronoweaver.pdf](assets/Test_document--Verdant_Chronoweaver.pdf?raw=true)

### 3.2 AI Core instance creation

#### 3.2 a) Verify the AI Core Entitlement

Before running the booster, confirm that the `extended` plan of SAP AI Core is assigned to your global account and added to the target subaccount. The booster will fail if the entitlement is missing at the global account level.

- At the global account level, open **Entitlements** → **Service Assignments**.
- Search for `SAP AI Core` and confirm the `extended` plan is assigned.

![Service assignments screen with the SAP AI Core extended plan highlighted](3-ai-core-document-grounding/images/ai-core-entitlement.png)

#### 3.2 b) Launch the AI Core Booster

We shall now execute the AI Core Booster to provision SAP AI Core in your subaccount. The booster automates the entitlement assignment, instance creation, and service key generation for the `extended` plan required by AI Core Document Grounding.

- In your global account, click on **Boosters**, look for **Set Up Account for SAP AI Core**, and then click on **Start** to launch the booster.

![Boosters page with the Set Up Account for SAP AI Core booster ready to launch](3-ai-core-document-grounding/images/ai-core-booster.png)

- The booster checks that your user has the required authorizations and that the global account holds the necessary entitlements. Wait for both checks to show **DONE**, then click on **Next Step**.

![AI Core booster step 1 showing the prerequisite checks marked DONE](3-ai-core-document-grounding/images/ai-core-booster-step-1.png)

- Select **Select Subaccount** to reuse an existing Cloud Foundry subaccount and click on **Next Step**.

> **Note:** Choose **Create Subaccount** instead if you do not already have a target subaccount.

![AI Core booster step 2 with Select Subaccount chosen](3-ai-core-document-grounding/images/ai-core-booster-step-2.png)

- Select your target **Subaccount** and **Space**. The **Org** is filled in automatically. Click on **Next Step**.

![AI Core booster step 3 with the target subaccount and space selected and the Org filled in automatically](3-ai-core-document-grounding/images/ai-core-booster-step-3.png)

- Validate your selections and click on **Finish**.

![AI Core booster step 4 review screen before the Finish click](3-ai-core-document-grounding/images/ai-core-booster-step-4.png)

- The booster assigns the `extended` plan, creates the `default_aicore` instance, and generates a default service key. Once completed, a **Success** message appears. Click on **Navigate to Subaccount**.

![AI Core booster success screen with the Navigate to Subaccount button](3-ai-core-document-grounding/images/ai-core-booster-success.png)

#### 3.2 c) Download the AI Core Service Key

The booster creates the SAP AI Core instance and a service key automatically. Download the service key — you'll need its credentials when configuring the Destination Service later.

- In the subaccount, open **Instances and Subscriptions** and click the `default_aicore` row to open its details panel on the right.
- Under **Service Keys**, click the **...** menu next to the default key and select **Download**.

![Subaccount Instances and Subscriptions view with the default_aicore service key Download option open](3-ai-core-document-grounding/images/ai-core-subaccount.png)

### 3.3 AI Core Document Grounding with Bruno

The next two subsections — [3.3 AI Core Document Grounding with Bruno](#33-ai-core-document-grounding-with-bruno) and [3.4 AI Core Document Grounding with AI Launchpad](#34-ai-core-document-grounding-with-ai-launchpad) — describe two interchangeable paths to the same outcome. Pick one. Bruno is free and open-source; AI Launchpad is a UI-driven alternative that requires a paid subscription.

#### 3.3 a) Install Bruno and Import the Collection

Bruno is an open-source API client for exploring and testing APIs. Use it to create the resource group, register the Object Store credentials as a generic secret, and provision the document grounding pipeline with the AI Core Document Grounding REST API.

- Download and install the latest version of [Bruno](https://www.usebruno.com/downloads).

> **Note:** The templates collections are stored as `.yml` files. Older Bruno versions do not support the YAML import format, so make sure to install the latest release.

- Open Bruno and click the **+** icon next to **Collections** in the left navigation, then select **Import collection**.
- Pick the `aicore-dg-s3.yml` collection file when prompted.

![Bruno UI showing the Import collection menu open in the Collections sidebar](3-ai-core-document-grounding/images/bruno-import.png)

#### 3.3 b) Configure the Environment

The collection ships with an `aicore-dg-s3` environment containing placeholders for the AI Core and Object Store credentials. Fill them in before running any request.

- With the `aicore-dg-s3` collection open, click the environment selector in the top-right corner and select `aicore-dg-s3`, then click **Configure**.
- Replace each `<placeholder>` with the corresponding value:
  - `AICore_AI_API_URL`, `AICore_clientid`, `AICore_clientsecret`, `AICore_url` — from the AI Core service key.
  - `S3_Region`, `S3_Host`, `S3_Bucket`, `S3_Username`, `S3_Access_Key_ID`, `S3_Secret_Access_Key` — from the Object Store service key.
- Leave `resource_group` and `generic_secret` at their defaults (or adjust to your naming convention). For the Object Store setup, you can use `object-store` as the name for the generic secret. Leave `pipeline_id` empty for now.
- Click **Save**.

![Bruno environment configuration screen with the AI Core and S3 placeholders ready to be filled in](3-ai-core-document-grounding/images/bruno-environments.png)

#### 3.3 c) Fetch an Access Token

Every request to the AI Core API requires an OAuth2 bearer token. The collection retrieves it once and reuses it across the other requests via a collection-level script.

- Open the `01_get_token` folder and select the `get_token` request.
- Click **Send**. A `200 OK` response with an `access_token` confirms the credentials are correct.

![Bruno response panel showing a 200 OK reply with an access_token field for the get_token request](3-ai-core-document-grounding/images/bruno-token.png)

> **Note:** Occasionally, the token expires. Resend the request above to retrieve a new token.

#### 3.3 d) Create the Resource Group

The resource group isolates document grounding artifacts inside the AI Core tenant. It must carry the `ext.ai.sap.com/document-grounding: true` label so that AI Core enables the grounding capability for it.

- Open the `02_resource_group` folder and select `create_resource_group`.
- Click **Send**. A `202 Accepted` response with the `resourceGroupId` confirms the request was queued.

![Bruno response panel showing a 202 Accepted reply with a resourceGroupId for create_resource_group](3-ai-core-document-grounding/images/bruno-resource-group.png)

- Select `get_resource_group` and click **Send** to poll the provisioning status. Initially the `status` field reads `PROVISIONING`.
- Wait a few minutes and resend the request until `status` reads `PROVISIONED`.

![Bruno response panel showing the resource group status as PROVISIONED](3-ai-core-document-grounding/images/bruno-resource-group-provisioned.png)

> **Note:** Do not continue to the next step until the resource group is fully `PROVISIONED` — the generic secret cannot be created against a resource group that is still onboarding.

#### 3.3 e) Create the Generic Secret

The generic secret stores the S3 credentials inside AI Core so that the document grounding pipeline can read from the Object Store bucket. The `ext.ai.sap.com/documentRepositoryType: S3` label tells AI Core how to interpret the credentials.

- Open the `03_generic_secret` folder and select `create_generic_secret`.
- Click **Send**. A `200 OK` response with `"message": "secret has been created"` confirms the secret is registered.

![Bruno response panel showing a 200 OK reply with the secret has been created message](3-ai-core-document-grounding/images/bruno-generic-secret.png)

#### 3.3 f) Create the Pipeline

The pipeline binds the generic secret to a document grounding job. Once created, AI Core ingests, chunks, embeds, and indexes every document in the bucket.

> **Note:** The full pipeline API is documented in [Create a Document Grounding Pipeline Using the Pipelines API | SAP Help Portal](https://help.sap.com/docs/sap-ai-core/generative-ai/create-document-grounding-pipeline-using-pipelines-api-d32b1465461149749b00129c02e05142). There you can find information on how to restrict processing to specific folders, include metadata, and configure the update schedule.

A request body that limits indexing to a folder inside the bucket looks like this (S3 only — for the other data repositories, see the SAP Help link above):

```json
{
  "type": "S3",
  "configuration": {
    "destination": "{{generic_secret}}",
    "s3": {
      "includePaths": [
        "/j4c-custom-knowledge"
      ]
    }
  }
}
```

To run the example above, replace the body in the `create_pipeline` request with the snippet.

- Open the `04_pipeline` folder and select `create_pipeline`.
- Click **Send**. A `201 Created` response returns the `pipelineId`.

![Bruno response panel showing a 201 Created reply with a pipelineId for create_pipeline](3-ai-core-document-grounding/images/bruno-pipeline-creation.png)

- Note down the returned `pipelineId` for later use.
- Select `get_pipeline_status` and click **Send** to monitor progress. The pipeline takes a few minutes to finish — longer if more documents are in the bucket. Resend until `status` reads `FINISHED`.

![Bruno response panel showing the pipeline status as FINISHED](3-ai-core-document-grounding/images/bruno-pipeline-finished.png)

- Select `get_documents` and click **Send** to list the documents picked up by the pipeline. Each document should report `"status": "INDEXED"`.

![Bruno response panel listing pipeline documents each with status INDEXED](3-ai-core-document-grounding/images/bruno-pipeline-documents.png)

> **Note:** If you upload new documents to the Object Store bucket after the pipeline has finished, run the `restart_pipeline` request to trigger a fresh sync. The pipeline picks up additions and changes, then transitions back to `FINISHED` once the new documents are indexed.

### 3.4 AI Core Document Grounding with AI Launchpad

This subsection is an alternative to [3.3 AI Core Document Grounding with Bruno](#33-ai-core-document-grounding-with-bruno) — pick one. The two paths produce the same resource group, generic secret, and pipeline. AI Launchpad is the UI-driven option.

#### 3.4 a) Provision SAP AI Launchpad

SAP AI Launchpad is a web-based UI that lets you set up AI Core Document Grounding through a graphical interface — without writing API requests. Using it is **optional**: the same setup can be completed with Bruno (see [3.3 AI Core Document Grounding with Bruno](#33-ai-core-document-grounding-with-bruno)). Choose AI Launchpad if you prefer a UI-driven workflow.

SAP AI Launchpad is a paid subscription service. The `standard` plan is required. Review the pricing on [SAP Discovery Center Service - SAP AI Launchpad](https://discovery-center.cloud.sap/serviceCatalog/sap-ai-launchpad?region=all&tab=service_plan) before subscribing.

SAP AI Launchpad can be set up using the **Set Up Account for SAP AI Launchpad** booster. Follow steps similar to the AI Core booster execution described in [3.2 AI Core instance creation](#32-ai-core-instance-creation).

Access to SAP AI Launchpad and its administrative features requires specific role collections to be assigned to your user. For more information, see [SAP AI Launchpad > Roles and Authorizations | SAP Help Portal](https://help.sap.com/docs/ai-launchpad/sap-ai-launchpad/security#loio4ef8499d7a4945ec854e3b4590830bcc).

#### 3.4 b) Create the AI API Connection

Before SAP AI Launchpad can manage the AI Core tenant, register the AI Core service key as an AI API connection.

- In SAP AI Launchpad, open **Workspaces** in the left navigation and click **Add** in the top-right corner.
- Enter a **Connection Name** (e.g., `j4c-ai-core`).
- Next to **Service Key**, click the upload icon and select the AI Core service key file you downloaded earlier. The **AI API URL**, **XSUAA URL**, **Client ID**, and **Client Secret** fields are populated automatically.
- Click **Create**.

![SAP AI Launchpad Add Connection dialog with the AI Core service key uploaded and the credential fields populated](3-ai-core-document-grounding/images/ai-launchpad-connection.png)

#### 3.4 c) Create the Resource Group

The resource group isolates document grounding artifacts inside the AI Core tenant.

- Go to **SAP AI Core Administration** > **Resource Groups** and click **Create** in the top-right corner.
- Enter a **Resource Group ID** (e.g., `j4c-custom-knowledge`).
- Ensure that the `ext.ai.sap.com/document-grounding` label is enabled.
- Click **Create**.

![SAP AI Launchpad Create Resource Group dialog with the document-grounding label enabled](3-ai-core-document-grounding/images/ai-launchpad-resource-group.png)

> **Note:** The resource group takes a few minutes to transition from `PROVISIONING` to `PROVISIONED`. Do not continue to the next step until the resource group is fully provisioned — the generic secret cannot be created against a resource group that is still onboarding.

- In the left navigation, click **Workspaces**.
- Under **Resource Groups**, click the card for the resource group you created (e.g., `j4c-custom-knowledge`). The card should show **Document Grounding: Enabled**.
- The header at the top of the launchpad now displays the active workspace as `<connection> (<resource-group>)` — for example, `j4c-ai-core (j4c-custom-knowledge)`.

![SAP AI Launchpad Workspaces page with the j4c-custom-knowledge resource group selected and Document Grounding marked Enabled](3-ai-core-document-grounding/images/ai-launchpad-select-resource-group.png)

#### 3.4 d) Create the Generic Secret

The generic secret stores the S3 credentials inside AI Core so that the document grounding pipeline can read from the Object Store bucket.

- Go to **SAP AI Core Administration** > **Generic Secrets** and click **Add**.
- Select **Amazon S3** as the **Document Repository Type** and ensure that **Document Grounding** is toggled on.
- Fill in the **Secret** key/value pairs using the Object Store service key.
- Click **Add**.

![SAP AI Launchpad Add Generic Secret dialog with Amazon S3 selected and Document Grounding toggled on](3-ai-core-document-grounding/images/ai-launchpad-generic-secret.png)

#### 3.4 e) Create the Document Grounding Pipeline

Create a pipeline so AI Core ingests, chunks, embeds, and indexes every document in the data repository.

- Go to **Generative AI Hub** > **Grounding Management** and click **Create** in the top-right corner.
- Choose `S3` as the **Document Store Type**.
- Choose the generic secret you created in the previous step (e.g., `object-store`)
- Click **Create**.

![SAP AI Launchpad Grounding Management Create Pipeline dialog with the S3 document store type and the object-store generic secret selected](3-ai-core-document-grounding/images/ai-launchpad-pipeline-creation.png)

The pipeline will now start ingesting the documents from the data repository. This process will take a few minutes. Open the pipeline to confirm that it finished successfully and that the test document was indexed.

- On the **Grounding Management** page, click the new pipeline (named `pipeline-<id>-collection`) to open its details.
- Wait until the **Status** in the header switches to **Completed**.
- Under **Data Repository Content**, the **Documents** list shows every indexed file.

![SAP AI Launchpad pipeline details page with Status Completed and the indexed Documents list under Data Repository Content](3-ai-core-document-grounding/images/ai-launchpad-pipeline-collection.png)

> **Note:** If you upload new documents to the Object Store bucket after the pipeline has finished, you can click the **Synchronize** icon in the top-right corner of the pipeline page to trigger a resync.

### 3.5 Support

#### 3.5 a) Where to Open Support Tickets

Custom Knowledge Grounding spans multiple SAP services, and each layer is owned by a different team. When something goes wrong, route the ticket to the component that owns the layer where the issue occurs.

#### 3.5 b) AI Core Document Grounding

The resource group, generic secret, and pipeline are part of AI Core Document Grounding. Open a ticket under component `CA-ML-RAGE` for issues such as:

- Resource group stuck in `PROVISIONING` or failing to provision.
- Generic secret creation rejected.
- Pipeline not starting, hanging, or finishing with errors.
- Documents in the data repository not indexed properly.

> **Note:** When the SAP Joule for Consultants Console shows a pipeline as **Completed With Errors**, only the successfully indexed documents are used in answers. Inspect the per-document status in Bruno (via `get_documents`) or in SAP AI Launchpad before opening the ticket.

#### 3.5 c) Work Zone as a Data Repository

If you use SAP Build Work Zone instead of Object Store as the data repository for document grounding, issues that are specific to the Work Zone source belong to component `EP-WZ-STA`.

> **Note:** Issues with the AI Core pipeline that reads from Work Zone (indexing, embeddings, pipeline status) still belong under `CA-ML-RAGE`. Use `EP-WZ-STA` only when the problem is on the Work Zone side of the integration.

#### 3.5 d) Destination Service and SAP Joule for Consultants Console

Once the pipeline reports **FINISHED** (Bruno) or **Completed** (AI Launchpad), the remaining steps described in the following sections — the setup of the Destination Service instance and the configuration in the SAP Joule for Consultants Console — is owned by the SAP Joule for Consultants team. Open a ticket under component `CA-GAIF-SCC` in this case.

> **Note:** Before opening a `CA-GAIF-SCC` ticket, confirm that the pipeline itself is healthy. A failing pipeline surfaces in the console as a downstream symptom, but the root cause belongs to AI Core Document Grounding.

## 4. Connection to SAP Joule for Consultants

### 4.1 Destination Service setup

#### 4.1 a) Configure the Destination Service

A Destination Service connects AI Core Document Grounding to SAP Joule for Consultants. Configure it as follows.

- In your subaccount, open **Instances and Subscriptions** and click **Create**.
- Select **Destination Service** with the `lite` plan, fill in the required fields, and click **Create** to provision the instance.

![Destination Service instance creation form with the lite plan selected](4-connection-to-j4c/images/destination-service-creation.png)

- Click the instance row (not the blue instance name) to open its details panel on the right.
- Under **Service Keys**, click **Create**.
- Enter a name and click **Create**.

![Destination Service details panel with the Create Service Key dialog open](4-connection-to-j4c/images/destination-service-service-key.png)

- Download the service key — you'll need it later to connect SAP Joule for Consultants.
- Then open the instance to configure its destinations — either click the blue instance name in the **Instances** list, or click **Manage Instance** at the top of the details panel on the right. Both navigate to the same instance page.

> **Note:** Destinations can be configured either at the instance level or at the subaccount level. This setup uses the instance level. Do not configure the destination at the subaccount level.

> **Note:** Editing or deleting destinations requires the BTP role collection `Destination Administrator`.

![Destination Service service key download menu](4-connection-to-j4c/images/destination-service-download.png)

#### 4.1 b) Create the Destination

- In the Destination Service instance, open the **Destinations** section and click **Create**.
- Select **From Scratch** and click **Create**.

![Destinations page with the New Destination From Scratch option selected](4-connection-to-j4c/images/destination-service-create-scratch.png)

- Open the service key of the AI Core instance — you'll copy several values from it.
- Set **Authentication** to **OAuth2ClientCredentials**, then paste in the **Client ID** and **Client Secret** from the AI Core service key.
- Fill in the following fields, replacing the placeholders with the values from the service key:
  - **Token Service URL:** `<url>/oauth/token`
  - **URL:** `<AI_API_URL>/v2/lm/document-grounding`
- Add the following **Additional Properties**:
  - `HTML5.ForwardAuthToken`: `true`
  - `HTML5.DynamicDestination`: `true`
  - `AI-Resource-Group`: name of your resource group

> **Note:** `AI-Resource-Group` is not available as a predefined value in the value help — enter the key name manually.

![Destination configuration form with OAuth2ClientCredentials authentication, Token Service URL, URL, and the three additional properties filled in](4-connection-to-j4c/images/destination-service-create-destination.png)

- Check the connection to verify the destination is configured correctly.

![Destination configuration showing a successful Check Connection result](4-connection-to-j4c/images/destination-service-check-connection.png)

### 4.2 Admin Console configuration

#### 4.2 a) Enable Custom Knowledge Grounding

With the Destination Service configured, enable Custom Knowledge Grounding in the SAP Joule for Consultants Console and connect to AI Core Document Grounding through the destination.

> **Note:** You need to have admin access to the SAP Joule for Consultants Console, see [SAP Joule for Consultants Console](https://help.sap.com/docs/joule/joule-tools-12ace5a963e147ffa6f5aab8a4cf15f4/sap-joule-for-consultants-console).

- In the SAP Joule for Consultants Console, open the **Settings** menu from the left navigation and select **Custom Knowledge Grounding**.
- Toggle the switch to enable the feature.

![SAP Joule for Consultants Console Settings page with the Custom Knowledge Grounding feature toggled on](4-connection-to-j4c/images/console-enable-custom-knowledge.png)

#### 4.2 b) Connect to the SAP Destination Service

- In the left navigation, open the **Custom Knowledge Grounding** page.
- Click **Connect** to open the connection dialog.
- Select **JSON** as the credentials type. Alternatively, choose **Credentials** to enter each field individually.
- Paste the contents of the Destination Service service key downloaded earlier into the **JSON Credentials** field.
- Click **Next**.

> **Note:** Use the service key from the Destination Service instance — not the AI Core service key.

![Connect dialog with the JSON credentials option selected and the Destination Service service key pasted in](4-connection-to-j4c/images/console-connect-json.png)

Once connected, the console retrieves the document grounding instances available through the destination.

- In the **Select Sources** dialog, check the instance(s) you want to use. Only sources with a green checkmark can be selected.
- Use **Recheck Health** if you recently updated a source and want to refresh its validation status.
- Click **Save**.

![Select Sources dialog showing available document grounding instances with green checkmarks](4-connection-to-j4c/images/console-select-sources.png)

#### 4.2 c) Manage Sources & Pipelines

The selected sources appear under **Sources & Pipelines**. Expand a source to inspect its pipelines.

![Sources & Pipelines view with a source expanded to show its pipelines](4-connection-to-j4c/images/console-sources-pipelines.png)

The pipeline table shows the following columns:

| **Column** | **Description** |
| --- | --- |
| Pipeline ID | Unique identifier — click the link to open detailed processing logs |
| Indexed Documents | Total number of documents submitted for processing |
| Data Source | Type of connected data source (e.g., S3) |
| Last Sync | Timestamp of the most recent sync run |
| Status | `Completed`, `Completed With Errors`, or `Processing` |

The three action icons in the top-right corner of the page are:

- **Pencil** — configure document grounding instances (connect or disconnect sources).
- **Bin** — delete the selected source.
- **Refresh** — re-read the pipeline metadata from AI Core Document Grounding and update what the console shows (status, last sync timestamp, document count).

> **Note:** Once the pipeline **Status** shows **Completed**, SAP Joule for Consultants references the grounded knowledge starting with the next new conversation.

> **Note:** If the status shows **Completed With Errors**, some documents were not ingested successfully by the document grounding pipeline. Only successfully processed documents are used in answers. For details, check the documents in Bruno or in the SAP AI Launchpad. For support, please open a ticket under component `CA-ML-RAGE` — troubleshooting the AI Core Document Grounding pipeline is out of scope for SAP Joule for Consultants.

> **Note:** The **Refresh** icon in the console only refreshes the **view** — it does **not** re-index your data repository. Whether newly uploaded documents become available to SAP Joule for Consultants is decided by re-running the AI Core Document Grounding pipeline itself: the `restart_pipeline` request in [3.3 AI Core Document Grounding with Bruno](#33-ai-core-document-grounding-with-bruno), or the **Synchronize** icon on the pipeline page in [3.4 AI Core Document Grounding with AI Launchpad](#34-ai-core-document-grounding-with-ai-launchpad). Until that pipeline run reaches `FINISHED` / `Completed`, the new documents are not indexed.

#### 4.2 d) Troubleshooting

**Destination shows "not a valid DGS destination":** The destination is missing one or more of the required additional properties (`HTML5.DynamicDestination`, `HTML5.ForwardAuthToken`, `AI-Resource-Group`), or its URL does not point to a valid document grounding endpoint. Edit the destination in the BTP Cockpit, add the missing properties, save it, then click **Recheck Health** in the console.

**Source not appearing in the Select Sources dialog:** Verify that the Destination Service instance whose service key you connected is the same instance where you created the destination. The console only discovers destinations from its own bound Destination Service instance.

**No pipelines appear after saving:** Allow a few minutes for the pipeline to initialize and the first sync to complete. Use the **Refresh** icon on the **Sources & Pipelines** page to update the view.

## 5. Testing

### 5.1 Testing Custom Knowledge Grounding

#### 5.1 a) Start a New Conversation

SAP Joule for Consultants references the grounded documents in any new conversation. Start a fresh conversation and ask a question whose answer is only available in the uploaded test document.

- In SAP Joule for Consultants, click **New Conversation** in the left navigation.
- Enter a prompt that targets content from the test document, here: `Explain the Heliotrope Fabricator`.

![SAP Joule for Consultants new conversation with the prompt Explain the Heliotrope Fabricator entered](5-testing/images/j4c-new-conversation.png)

> **Note:** The Heliotrope Fabricator is fictional content contained only in `Test_document--Heliotrope_Fabricator.pdf`. If SAP Joule for Consultants returns a meaningful explanation, the document grounding is working as expected.

#### 5.1 b) Verify the Source Citation

SAP Joule for Consultants cites the documents it used to ground its answer. Open the sources panel to confirm that the test document was retrieved.

- Once SAP Joule for Consultants has answered, click **Sources** below the response.
- A panel opens on the right listing the cited documents.

![Sources panel listing Test_document--Heliotrope_Fabricator.pdf as a Customer Document with a citation index and page reference](5-testing/images/j4c-test-document.png)

The panel header reads **Sources** and lists every document the answer was grounded on. Entries provided through Custom Knowledge Grounding are grouped under the **Customer** category, with each entry labeled **Customer Document** to distinguish it from SAP-managed content. The cited file is shown with the citation index from the answer (e.g., `[1]`) and a page reference (e.g., `(pg 1)`).

> **Note:** Source entries are clickable, but for S3-backed sources the link does not resolve to the original file. Because the Object Store uses S3, this applies to all documents uploaded through it.
