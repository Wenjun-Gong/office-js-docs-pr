---
title: Deploy and publish Office Add-ins
description: Methods and options to deploy your Office Add-in for testing or distribution to users.
ms.date: 02/12/2025
ms.localizationpriority: high
---

# Deploy and publish Office Add-ins

You can use one of several methods to deploy your Office Add-in for testing or distribution to users. The deployment method can also affect which platforms surface your add-in.

|Method|Use|
|:---------|:------------|
|[Sideloading](../testing/test-debug-office-add-ins.md#sideload-an-office-add-in-for-testing)|As part of your development process, to test your add-in running on Windows, iPad, Mac, or in a browser. (Not for production add-ins.) |
|[Network share](../testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins.md)|As part of your development process, to test your add-in running on Windows after you have published the add-in to a server other than localhost. (Not for production add-ins, for testing on iPad, Mac, or the web, or for add-ins that use the [unified manifest for Microsoft 365](../develop/unified-manifest-overview.md).)|
|[AppSource](#appsource)|To distribute your add-in publicly to users.|
|[Microsoft 365 admin center](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps)|In a cloud deployment, to distribute your add-in to users in your organization by using the Microsoft 365 admin center. This is done through [Integrated Apps](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) or [Centralized Deployment](/microsoft-365/admin/manage/centralized-deployment-of-add-ins). |
|[SharePoint catalog](publish-task-pane-and-content-add-ins-to-an-add-in-catalog.md)|In an on-premises environment, to distribute your add-in to users in your organization. Doesn't support add-ins that use the [unified manifest for Microsoft 365](../develop/unified-manifest-overview.md) or any feature that requires a **\<VersionOverrides\>** element in the add-in only manifest.|
|[Exchange server](#outlook-add-in-exchange-server-deployment)|In an on-premises or online environment, to distribute Outlook add-ins to users.|

[!INCLUDE [publish policies note](../includes/note-publish-policies.md)]

## Deployment options by Office application and add-in type

The deployment options that are available depend on the Office application that you're targeting and the type of add-in you create.

| Extension point | Sideloading | Network share                                 | AppSource | Microsoft 365 admin center | SharePoint catalog\* | Exchange server |
|:----------------|:-----------:|:---------------------------------------------:|:---------:|:--------------------------:|:--------------------:|:---------------:|
| Content         | Supported   | Supported                                     | Supported | Supported                  | Supported            | Not supported   |
| Task pane       | Supported   | Supported                                     | Supported | Supported                  | Supported            | Not supported   |
| Command         | Supported   | Support for Excel, PowerPoint, and Word only  | Supported | Supported                  | Not supported        | Not supported   |
| Mail app        | Supported   | Not supported                                 | Supported | Supported                  | Not supported        | Supported       |

\* SharePoint catalogs don't support Office on Mac.

## Production deployment methods

The following sections provide additional information about the deployment methods that are most commonly used to distribute production Office Add-ins to users within an organization.

### Deploy updates

[!INCLUDE [deploy-updates-that-require-admin-consent](../includes/deploy-updates-that-require-admin-consent.md)]

For information about how end users acquire, insert, and run add-ins, see [Start using your Office Add-in](https://support.microsoft.com/office/82e665c4-6700-4b56-a3f3-ef5441996862).

### AppSource

You can make your add-in available through [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office), Microsoft's online app store which is accessible through a browser and through the UI of Office applications. Distribution through AppSource gives you the option of including installation of your add-in with the installation of your Windows app or a COM or VSTO add-in. For more information, see [Publish to your Office Add-in to AppSource](publish-office-add-ins-to-appsource.md).

### Integrated Apps via the Microsoft 365 admin center

The Microsoft 365 admin center makes it easy for an administrator to deploy Office Add-ins to users and groups in their organization. Add-ins deployed via the admin center are available to users in their Office applications right away, with no client configuration required. You can use Integrated Apps to deploy internal add-ins as well as add-ins provided by ISVs. Integrated Apps also shows admins add-ins and other apps bundled together by same ISV, giving them exposure to the entire experience across the Microsoft 365 platform.

When you link your Office Add-ins, Teams apps, SPFx apps, and [other apps](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps#what-apps-can-i-deploy-from-integrated-apps) together, you create a single software as a service (SaaS) offering for your customers. For general information about this process, see [How to plan a SaaS offer for the commercial marketplace](/azure/marketplace/plan-saas-offer). For specifics on how to create Integrated Apps, see [Configure Microsoft 365 App integration](/azure/marketplace/create-new-saas-offer#configure-microsoft-365-app-integration).

For more information on the Integrated Apps deployment process, see [Test and deploy Microsoft 365 Apps by partners in the Integrated apps portal](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

> [!IMPORTANT]
> Customers in sovereign or government clouds don't have access to Integrated Apps. They will use Centralized Deployment instead. Centralized Deployment is a similar deployment method, but doesn't expose connected add-ins and apps to the admin. For more information, see [Determine if Centralized Deployment of add-ins works for your organization](/microsoft-365/admin/manage/centralized-deployment-of-add-ins).

### SharePoint app catalog deployment

A SharePoint app catalog is a special site collection that you can create to host the manifests (add-in only manifest type) of a Word, Excel, or PowerPoint add-in. Because SharePoint catalogs don't support new add-in features implemented in the `VersionOverrides` node of the manifest, including add-in commands, we recommend that you use Centralized Deployment via the admin center if possible. Add-in commands deployed via a SharePoint catalog open in a task pane by default.

If you are deploying add-ins in an on-premises environment, use a SharePoint catalog. For details, see [Publish task pane and content add-ins to a SharePoint catalog](publish-task-pane-and-content-add-ins-to-an-add-in-catalog.md).

> [!NOTE]
> - SharePoint catalogs don't support Outlook add-ins.
> - SharePoint catalogs don't support add-ins that use the [unified manifest for Microsoft 365](../develop/unified-manifest-overview.md).
> - SharePoint catalogs don't support Office on Mac. To deploy Office Add-ins to Mac clients, you must submit them to [AppSource](/partner-center/marketplace-offers/submit-to-appsource-via-partner-center).

### Outlook add-in Exchange server deployment

For on-premises and online environments that don't use the Azure AD identity service, you can deploy Outlook add-ins via the Exchange server.

Outlook add-in deployment requires:

- Microsoft 365, Exchange Online, or Exchange Server 2016 or later
- Outlook 2016 or later

To assign add-ins to tenants, use the Exchange admin center to upload a manifest directly, either from a file or a URL, or add an add-in from AppSource. To assign add-ins to individual users, you must use Exchange PowerShell. For details, see [Add-ins for Outlook in Exchange Server](/exchange/add-ins-for-outlook-2013-help).

It's important to note that some versions of Outlook clients and Exchange servers may only support certain Mailbox requirement sets. For details about supported requirement sets, see [Requirement sets supported by Exchange servers and Outlook clients](/javascript/api/requirement-sets/outlook/outlook-api-requirement-sets#requirement-sets-supported-by-exchange-servers-and-outlook-clients).

## GoDaddy Microsoft 365 SKUs

[Microsoft 365 subscriptions provided by GoDaddy](https://www.godaddy.com/business/office-365) have limited support for add-ins. The following options are **not** supported.

- Deployment through the Microsoft Admin Center.
- Deployment through Exchange servers.
- Acquiring add-ins from AppSource.

## See also

- [Sideload Outlook add-ins for testing](../outlook/sideload-outlook-add-ins-for-testing.md)
- [Publish to your Office Add-in to AppSource](publish-office-add-ins-to-appsource.md)
- [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office)
- [Design guidelines for Office Add-ins](../design/add-in-design.md)
- [Create effective AppSource listings](/partner-center/marketplace-offers/create-effective-office-store-listings)
- [Troubleshoot user errors with Office Add-ins](../testing/testing-and-troubleshooting.md)
- [What is the Microsoft commercial marketplace?](/azure/marketplace/overview)
- [Microsoft Dev Center app publishing page](https://developer.microsoft.com/microsoft-teams/app-publishing)

