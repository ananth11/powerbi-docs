---
title: Distribute content to external guest users with Azure AD B2B
description: Power BI enables sharing content with external guest users through Azure Active Directory Business-to-business (Azure AD B2B).
author: kfollis
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: conceptual
ms.date: 09/09/2019
ms.author: kfollis
LocalizationGroup: Administration
---

# Distribute Power BI content to external guest users with Azure AD B2B

Power BI enables sharing content with external guest users through Azure Active Directory Business-to-business (Azure AD B2B).
By using Azure AD B2B, your organization enables and governs sharing with external users in a central place. By default, external guests have a consumption only experience. Additionally, you can allow guest users outside your organization to edit and manage content within your organization.

This article provides a basic introduction to Azure AD B2B in Power BI. For more information, see [Distribute Power BI content to external guest users using Azure Active Directory B2B](guidance/whitepaper-azure-b2b-power-bi.md).

## Enable access

Make sure to enable the [Share content with external users](service-admin-portal.md#export-and-sharing-settings) feature in the Power BI admin portal before inviting guest users. Even when this option is enabled, the user must have permission in Azure Active directory to invite guest users, which is granted through the Guest Inviter role. 

The option to [allow external guest users to edit and manage content in the organization](service-admin-portal.md#allow-external-guest-users-to-edit-and-manage-content-in-the-organization) lets you give guest users the ability to see and create content in workspaces, including browsing your organization's Power BI.

> [!NOTE]
> The [Share content with external users](service-admin-portal.md#export-and-sharing-settings) setting controls whether Power BI allows inviting external users to your organization. Once an external user accepts the invite, they become an Azure AD B2B guest user in your organization. They appear in people pickers through-out the Power BI experience. When the setting is disabled, existing guest users in your organization continue to have access to any items they had access to and continue to be listed in people picker experiences. Additionally, if guests are added through the [planned invite](#planned-invites) approach they will also appear in people pickers. To prevent guest users from accessing Power BI, use an Azure AD conditional access policy.

## Who can you invite?

Guest users with most email addresses can be invited to your organization, including personal accounts like gmail.com, outlook.com, and hotmail.com. Azure AD B2B calls these addresses *social identities*.

You cannot invite users that are associated with a government cloud, like [Power BI for US Government](service-govus-overview.md).

## Invite guest users

Guest users only require invitations the first time you invite them to your organization. To invite users, use planned or ad hoc invites.

To use ad hoc invites, use the following capabilities:
* Report and Dashboard sharing
* App access list

Ad hoc invites are not supported in the workspace access list. Use the [planned invites approach](#planned-invites) to add these users to your organization. Once the external user is a guest in your organization, add them to the workspace access list.

### Planned invites

Use a planned invite if you know which users to invite. The Azure portal or PowerShell enables you to send the invites. You must be a tenant admin to invite people.

Follow these steps to send an invite in the Azure portal.

1. In the [Azure portal](https://portal.azure.com), select **Azure Active Directory**.

1. Under **Manage**, select **Users** > **All users** > **New guest user**.

    ![Screenshot of the Azure portal with the New guest user option called out.](media/service-admin-azure-ad-b2b/azure-ad-portal-new-guest-user.png)

1. Enter an **email address** and **personal message**.

    ![Screenshot of the Azure AD Portal New Guest User dialog.](media/service-admin-azure-ad-b2b/azure-ad-portal-invite-message.png)

1. Select **Invite**.

To invite more than one guest user, use PowerShell. For more information, see [Azure AD B2B collaboration code and PowerShell samples](/azure/active-directory/b2b/code-samples/).

The guest user needs to select **Get Started** in the email invitation they receive. The guest user is then added to the tenant.

![Screenshot of Guest user email invitation.](media/service-admin-azure-ad-b2b/guest-user-invite-email.png)

### Ad hoc invites

To invite an external user at any time, add them to your dashboard or report through the share UI, or your app through the access page. Here is an example of what to do when inviting an external user to use an app.

![Screenshot of External user added to App access list in Power BI.](media/service-admin-azure-ad-b2b/power-bi-app-access.png)

The guest user will receive an email indicating that you shared the app with them.

![Screenshot of Email for app shared with guest user](media/service-admin-azure-ad-b2b/guest-user-invite-email-2.png)

The guest user must sign in with their organization email address. They'll receive a prompt to accept the invitation after signing in. After signing in, the app opens for the guest user. To return to the app, they should bookmark the link or save the email.


## Licensing

The guest user must have the proper licensing in place to view the content that you shared. There are three ways to make sure the user has a proper license: use Power BI Premium, assign a Power BI Pro license, or use the guest's Power BI Pro license.

[Guest users who can edit and manage content in the organization](service-admin-portal.md#allow-external-guest-users-to-edit-and-manage-content-in-the-organization) need a Power BI Pro license to contribute content to workspaces or sharing content with others.

### Use Power BI Premium

Assigning the workspace to [Power BI Premium capacity](service-premium-what-is.md) lets the guest user use the app without requiring a Power BI Pro license. Power BI Premium also lets apps take advantage of other capabilities like increased refresh rates, dedicated capacity, and large model sizes.

![Diagram of guest user experience with Power BI Premium.](media/service-admin-azure-ad-b2b/license-approach-1.png)

### Assign a Power BI Pro license to guest user

Assigning a Power BI Pro license to a guest user within your tenant lets that guest user view content in the tenant. For more information about assigning licenses, see [Assign licenses to users on the Licenses page](/office365/admin/manage/assign-licenses-to-users#assign-licenses-to-users-on-the-licenses-page). Before assigning Pro licenses to guest users, contact your Microsoft account representative to ensure you're in compliance with the terms of your agreement with Microsoft.

![Diagram of guest user experience with Assign Pro license from your tenant.](media/service-admin-azure-ad-b2b/license-approach-2.png)

### Guest user brings their own Power BI Pro license

The guest user already has a Power BI Pro license assigned within their tenant.

![Diagram of guest user experience when they bring their own license.](media/service-admin-azure-ad-b2b/license-approach-3.png)

## Guest users who can edit and manage content

When using the [allow external guest users to edit and manage content in the organization](service-admin-portal.md#allow-external-guest-users-to-edit-and-manage-content-in-the-organization) feature, the specified guest users get additional access to your organization's Power BI. Allowed guests can see any content to which they have permission, access Home, browse workspaces, install apps, see where they are on the access list, and contribute content to workspaces. They can create or be an Admin of workspaces that use the new workspace experience. Some limitations apply. The Considerations and Limitations section list those restrictions.
 
To help allowed guests sign in to Power BI, provide them with the Tenant URL. To find the tenant URL, follow these steps.

1. In the Power BI service, in the top menu, select help (**?**) then **About Power BI**.

2. Look for the value next to **Tenant URL**. Share the tenant URL with your allowed guest users.

    ![Screenshot of About Power BI dialog with guest user tenant URL called out.](media/service-admin-azure-ad-b2b/power-bi-about-dialog.png)

## Considerations and Limitations

* By default, external Azure AD B2B limits guests to consumption of content only. External Azure AD B2B guests can view apps, dashboards, reports, export data and create email subscriptions for dashboards and reports. They can't access workspaces or publish their own content. To remove these restrictions, you can use the [Allow external guest users to edit and manage content in the organization](service-admin-portal.md#allow-external-guest-users-to-edit-and-manage-content-in-the-organization) feature.

* To invite guest users a Power BI Pro license is needed. Pro Trial users can't invite guest users in Power BI.

* Some experiences are not available to [guest users who can edit and manage content in the organization](service-admin-portal.md#allow-external-guest-users-to-edit-and-manage-content-in-the-organization). To update or publish reports, they need to use the Power BI service web UI, including Get Data to upload Power BI Desktop files.  The following experiences aren't supported:
    * Direct publishing from Power BI desktop to the Power BI service
    * Guest users can't use Power BI desktop to connect to service datasets in the Power BI service
    * Classic workspaces tied to Office 365 Groups:
        * Guest user can't create or be Admins of these workspaces
        * Guest users can be members
    * Sending ad hoc invites isn't supported for workspace access lists
    * Power BI Publisher for Excel isn't supported for guest users
    * Guest users can't install a Power BI Gateway and connect it to your organization
    * Guest users can't install apps publish to the entire organization
    * Guest users can't use, create, update, or install organizational content packs
    * Guest users can't use Analyze in Excel
    * Guest users can't be @mentioned in commenting
    * Guest users can't use subscriptions
    * Guest users who use this capability should have a work or school account. 
    
* Guest users using Personal accounts will experience more limitations because of sign-in restrictions.
    * They can use consumption experiences in the Power BI service through a web browser
    * They can't use the Power BI Mobile apps.
    * They won't be able to sign-in to provide credentials where a work or school account is required.

* This feature isn't currently available with the Power BI SharePoint Online report web part.

* There are Active Directory Settings that can limit what external guest users can do within your overall organization. That also applies to your Power BI environment. The following documentation discusses the settings:
    * [Manage External Collaboration Settings](/azure/active-directory/b2b/delegate-invitations#configure-b2b-external-collaboration-settings)
    * [Allow or block invitations to B2B users from specific organizations](https://docs.microsoft.com/azure/active-directory/b2b/allow-deny-list)
    * [Allow or block guest users from accessing the Power BI service](/azure/active-directory/conditional-access/overview)
    
* Sharing outside your organization isn't supported national clouds. Instead, create user accounts in your organization that external users can use to access the content. 

* If you share directly to a guest user, Power BI will send them an email with the link. To avoid sending an email, add the guest user to a security group and share to the security group.  

## Next steps

For more detailed info, including how row-level security works, check out the whitepaper: [Distribute Power BI content to external guest users using Azure AD B2B](https://aka.ms/powerbi-b2b-whitepaper).

For information about Azure AD B2B, see [What is Azure AD B2B collaboration?](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b/).
