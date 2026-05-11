---
title: SharePoint AirSync
devrev_id: ART-24213
parent_directory: AirSync
translation_group: RDmRHpg9
modified_date: "2026-02-23T06:29:03.695Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/RDmRHpg9"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
---

# SharePoint AirSync

The SharePoint AirSync simplifies import from SharePoint to DevRev, supporting both one-time imports and ongoing syncs.

# Supported Objects

The following is a list of SharePoint objects and their corresponding DevRev equivalents. Those marked as **Sync to DevRev** are eligible for import from SharePoint to DevRev.

|  |  |  |
| --- | --- | --- |
| **SharePoint Object** | **DevRev Object** | **Sync to DevRev** |
| Wiki pages | Article(as a Page) | ✅ |
| Site pages | Article(as a Link) | ✅ |
| Site URL | Article(as a Link) | ✅ |
| Web parts | Article(as an attachment) | ✅ |
| Files | Article(as an attachment) | ✅ |
| Drives | Collection | ✅ |
| Folders | Collection | ✅ |
| User | DevUser | ✅ |
| Group | Group | ✅ |
| Group Members | Object Members | ✅ |

# Supported Connection Types

SharePoint AirSync offers two connection types. Choose the one that fits your organization’s needs best.

## **User Flow (User-based OAuth connection)**

In this flow, each user creates their own OAuth connection to SharePoint. Here's how it works:

* Each user authenticates with their Microsoft account.
* Users can only import data from SharePoint sites they have access to.
* Each user selects the SharePoint sites they want to import.

## **App Flow (Admin-based client credential connection)**

In this flow, a Microsoft Entra ID Global Administrator sets up a single organization-wide connection using client credential authentication. Here's how it works:

* A Global Administrator creates an OAuth app with required scopes and grants admin consent in their Entra account.
* The connection can access any SharePoint site within the tenant.
* Data can be imported on behalf of any user in the organization.

# Installing the SharePoint AirSync to your org

To get started, navigate to **Settings > Integrations > Snap-ins**. Under the **All Snap-ins** tab, search for **Microsoft SharePoint**, open the snap-in, click **Add**, and then click the **Install Snap-in** button.

# Setting Up the SharePoint Connection

Depending on the connection type you choose, you will need to follow a different process to create the connection as mentioned below.

## **User Flow (User-based OAuth connection)**

1. The OAuth flow requires the following scopes. Admin consent is needed to proceed if it has not already been granted.

   |  |  |
   | --- | --- |
   | **Scope** | **Resource** |
   | GroupMember.Read.All | Microsoft Graph |
   | Organization.Read.All | Microsoft Graph |
   | RoleManagement.Read.Directory | Microsoft Graph |
   | Sites.Read.All | Microsoft Graph |
   | User.Read.All | Microsoft Graph |
   | AllSites.FullControl | SharePoint |
2. Since the scopes required by the OAuth app for SharePoint AirSync to function require admin consent, please share the [link](https://login.microsoftonline.com/common/adminconsent?client_id=ca450179-12cf-4625-b4f8-c89d60c037f9) below with your Global Administrators and request them to grant consent for the requested scopes, as shown in the screenshot below.  
     
   ***Note***: *The Global Administrator might see an error message after granting consent. Please ignore it for now and proceed to the next step.*  
   ![SharePointOAuthAppBAdmiinConsent.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11584994&key=3dac9a95598ac187cad50765d0f52a3f0937f1186f335b3d88dfb6669ad19dae)
3. Once admin consent has been granted for the requested scopes, click on the **AirSync** button, select **Microsoft SharePoint** from the list of snap-ins, click **Select connection**, and then click **Add connection**. You should then see a modal similar to the one shown below.  
   ![Screenshot 2026-02-11 at 4.40.44 PM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9314435&key=9ff5b80946c18313c32061a8e00b6d06b901c96e2d37cee5485ce6d31a8aa449)
4. Click **Sign in with Microsoft SharePoint** and follow the prompts to create the OAuth connection with SharePoint.
5. Once the connection is successfully established, you will see a list of all the sites you have access to. Select one or more sites from the list to import data from.

## App Flow (Client Credential Authentication)

The App Flow uses client credential-based authentication and certificate-based security. All steps must be performed by a Microsoft Entra ID Global Administrator.

### 1. Create an OAuth Application in Microsoft Entra ID

1. Go to **Microsoft Entra ID** > **App registrations**
2. Click on a **New registration**
3. Provide the application name as **DevRev SharePoint** for easy identification. However, you may choose a different name if preferred.
4. For the Supported account types select **Accounts in this organizational directory only (<ORG> Management only - Single tenant)**
5. Click on the Register button  
   ![image1.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316067&key=ea2d086641271d0080b09ff6cd47d9a5d23afd90a12b1d3726341ff012d5a1db)
6. Open the OAuth application and select the API permissions from the available options  
   ![image2.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316109&key=238511c3709d90a3fb5eff5c3768a5842d1a81472e16e76eca80fe9b0203be84)
7. Click on the Add a permission button and add the following listed scopes as Application permissions.

|  |  |
| --- | --- |
| Scope | Resource |
| Sites.FullControl.All | Microsoft Graph |
| User.Read.All | Microsoft Graph |
| GroupMember.Read.All | Microsoft Graph |
| RoleManagement.Read.Directory | Microsoft Graph |
| Sites.FullControl.All | SharePoint |

8. Grant admin consent for the tenant once all the scopes have been added.

Once the OAuth application is created, you will need to generate a private key and certificate that will be associated with this app.

---

### 2. Generate Private Key and Certificate

Follow the steps below based on your operating system to generate the private key and certificate required for client credential authentication.

**macOS**

macOS includes OpenSSL by default, so no additional setup is required.

**Windows (Command Prompt) Prerequisite (one-time setup)**  
Windows does not include OpenSSL out of the box and requires a one-time installation before proceeding.

1. Download Win64 OpenSSL Light from:  
   <https://slproweb.com/products/Win32OpenSSL.html>
2. During installation:

   * Select "Add OpenSSL to the system PATH"
   * Use the default install location: C:\Program Files\OpenSSL-Win64\

Verify installation - Open Command Prompt and run the following command:

```
openssl version
```

If this command works, you are ready to proceed.

**Run the following commands in the same sequence from the terminal/command line:**

```
openssl genrsa -out tempprivatekey.key 2048

openssl pkcs8 -topk8 -inform PEM -outform PEM -in tempprivatekey.key -out privatekey.key -nocrypt

awk 'BEGIN{printf "\""; first=1}
     { sub(/\r$/,""); if(!first) printf "\\n"; first=0; printf "%s",$0 }
     END{printf "\""}' privatekey.key > privatekey.jsonstring

openssl req -new -key privatekey.key -out request.csr

openssl x509 -req -days 1000 -in request.csr -signkey privatekey.key -out certificate.crt
```

|  |  |
| --- | --- |
| **File** | **Description** |
| privatekey.key | Private key used for JWT signing |
| privatekey.jsonstring | Private key in the required format |
| certificate.crt | Certificate uploaded to Entra ID |
| request.csr | Certificate Signing Request |
| tempprivatekey.key | Temporary key (can be deleted) |

---

### 3. Upload Certificate to Entra ID

1. Go to your App registration and open the DevRev SharePoint app
2. Navigate to Certificates & secrets
3. Upload the generated certificate.crt
4. Note down the Thumbprint shown after upload

---

### 4. Information Required to Create the Connection

Once the above steps are completed, please keep the following information handy, as it will be required during the **Create Connection** phase:

1. Client ID
2. Tenant ID
3. Certificate thumbprint
4. Private Key (privatekey.jsonstring)

Please note that all inputs provided during the connection setup are securely stored in an encrypted format. These inputs will be used to securely generate the access token.

---

### 5. Create connection

The App Flow requires two separate connections to be created using the information generated above.

**Create the REST Connection:**

1. Open the snap-in configuration.
2. Click the **Add connection** button (as shown in the screenshot below).  
   ![Screenshot 2026-02-23 at 10.43.10 AM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11731527&key=0db527fe64fb0540992d6422e5c0f1afde40527b2f603df90f404f26b295aed6)
3. A configuration modal will open.  
   ![Screenshot 2026-02-23 at 10.50.26 AM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11731551&key=1a57798b7cffd510dbeeaceb4874237f5e53f8e1b334cc08bf96156d63089860)
4. Enter a meaningful name for the connection.

   * We recommend adding **"REST"** at the end of the name for easier identification (optional).
5. Provide all the required information.
6. Click **Next** to complete the REST connection setup.

**Create the Graph Connection:**

1. Click the **AirSync** button.
2. Select the Microsoft SharePoint snap-in from the list of snap-ins.
3. Click on **Select connection > Add Connection.**  
   ![Screenshot 2026-02-23 at 11.16.30 AM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11731646&key=b85203ccb2783c773b278b55fd118a9a3bd54273c4f51d6883b0765bc1c5d4b3)
4. Select the **Microsoft SharePoint Graph** tab from the connection options.
5. Enter a meaningful name for the connection.

   * We recommend adding **"Graph"** at the end of the name for easier identification (optional).
6. Provide all the required information.
7. Click **Next** to complete the Graph connection setup.

![Screenshot 2026-02-23 at 11.12.35 AM.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/11731469&key=91e207997e8d87f064065e178b5cd154380d229ac3015b49ef19b4df9f955901)

### 6. Select Sites

Once the connection has been successfully created, you will see a list of all sites within the tenant across all users. Please select one or more sites from the list to import data from.

# Post import options

After a successful import, you have the following options available for the imported sites:

* **Sync to DevRev**

  This option allows you to synchronize any modifications made in SharePoint with the corresponding items previously imported into DevRev. It also creates new items in DevRev for any new content in SharePoint after the last sync or import.
* **View Report**

  This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import**

  If you want to remove the import and all data that were imported from SharePoint into DevRev, you can use this option.
* **Edit Connection**

  Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

## Sync to DevRev

After a successful import from SharePoint, you can choose to sync the imported data with DevRev. This feature imports any changes made to previously imported items from SharePoint.

To perform a one-time sync to DevRev, follow these steps:

1. Go to **Settings > Integrations > AirSyncs**.
2. Locate the previously imported site.
3. Select the **⋮** > **From SharePoint to DevRev** option.

> A one-time sync may overwrite fields in previously imported items, even if they were modified in DevRev.

## Historical imports

To view currently running and previous imports from various sources, do the following:

1. Go to **Settings > Integrations > AirSyncs**.
2. Select the import you want to view.
3. Click on the context menu (⋮) and select **View Report**.

## Periodic sync

After successfully importing to DevRev, you have the option to enable a periodic sync. This allows for automatic synchronization with DevRev on a regular basis. By default, the sync occurs once an hour.

To configure periodic sync, follow these steps:

1. Go to **Settings > Integrations > AirSync**.
2. Locate the previously imported site.
3. Select the **⋮** > **Set Periodic Sync** option.

The Enable automation for synced items setting is optional and can be activated during periodic sync configuration. When enabled, newly created or updated items trigger events, which can initiate webhooks, notifications, snap-ins, and other processes, as if the events originated directly in DevRev.

If this setting is turned off, updates do not trigger any event-driven processes. This behavior applies only to periodic syncs; no events are triggered during a first-time import or manual sync to or from DevRev.

## Delete import

> This deletes any content created by the import, including wiki pages, site pages, web parts, files, drive, folders, users, and attachments.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the configuration used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the site again after its deletion.

To delete an import and all the content it created, go to **Settings > Integrations > AirSyncs**, find the previously imported site, and select **⋮** > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support article [SharePoint AirSync](https://support.devrev.ai/en-US/devrev/article/RDmRHpg9) (ART-24213)
