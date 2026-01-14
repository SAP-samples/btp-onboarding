# Global Account Security 


### SAP BTP User Account

A **user account** corresponds to a particular user in an identity provider. The user is always stored in an external identity provider, such as a custom tenant of SAP Cloud Identity Services or the default identity provider. 

A username alone doesn't determine a concrete user account, as you can have users with the same username in different identity providers. A specific user is identified by the combination of user name and identity provider. Different user accounts can have different assigned role collections and, therefore, different authorizations.

SAP BTP creates a copy of the user in the global account or subaccount, known as a shadow user. Global account or subaccount administrators of SAP BTP assign role collections to shadow users. 

SAP BTP distinguishes between platform users (account management, custom development, and operations) and business users (for the applications).


#### Platform Users

Users in the Global Account are referred to as **Platform Users**. They are the users who have full access and provide permissions at the global account, directory, or subaccount level.

As a Global Account Administrator, you can add additional users to your Global Account. 


#### Business Users

Business users use the applications that are deployed to a **SAP BTP Subaccount**. For example, the end users of services, such as SAP Build Work Zone, or end users of your custom applications, are business users.


For more information, see [SAP Help Portal - Working with Users](https://help.sap.com/docs/btp/sap-business-technology-platform/working-with-users?version=LATEST&q=shadow+user&locale=en-US).


### Role Collections

SAP BTP provides a set of role collections to establish administrator access to your global account and its subaccounts.

Role collections group authorizations for resources and services. Your administrators assign these role collections to other platform users to create new administrators. Role collections consist of individual roles. 

Role collections are account-specific. Role collections that exist in the global account don’t exist in the subaccounts. 

In a new Global Account with Subaccount, you just have 2 Role Collections:

- Global account administrator and
- Global account viewer

![Role Collections in Global Account](images_02/2_3_1_ga_rolecollections.png)


### Identity Provider

All users of SAP BTP are stored in an external identity provider, either in the "default identity provider" or in a custom identity provider, such as a custom tenant of "SAP Cloud Identity Services". 

When a user authenticates, SAP BTP forwards the request to the identity provider. SAP BTP holds a copy of this user (shadow user), and you can assign roles or role collections to this user. You can use the default and a custom identity provider in parallel.

>Note: SAP recommends that you configure your custom tenant of SAP Cloud Identity Services as a custom identity provider during the onboarding process. 


#### Default Identity Provider

The "SAP ID service" is the default identity provider for SAP BTP. You can start using it without further configuration. The default identity provider will work independently from your custom identity provider. 

Log in to [SAP ID service](https://account.sap.com/sam/landing) and check your user account and credentials in SAP ID Service.

![User Account in Default Identity Services](images_02/2_3_2_defaultidprovider.png)   


#### Custom Identity Provider

SAP Cloud Identity Services are a set of services within the SAP Business Technology Platform (SAP BTP) that enable you to integrate identity and access management across systems. The goal is to provide a seamless single sign-on experience across systems while ensuring that system and data access are secure. 

SAP Cloud Identity Services include Identity Authentication, Identity Provisioning, Identity Directory, and Authorization Management.

Find your Cloud Identity Services custom tenant in your System Landscape, or in the "Activation Information for SAP Cloud Identity Services" email if your user account was provided by an administrator. 

1. Click the link to access your user profile. The URL should be sth. like https://abcd0efgh.accounts.ondemand.com/.

   ![User Account in Cloud Identity Services](images_02/2_3_3_user_in_cis.png)   

2. If you are a tenant administrator, you can access the admin UI by adding /admin: https://abcd0efgh.accounts.ondemand.com/admin.

   ![User Account in Cloud Identity Services](images_02/2_3_4_cis_tenant.png)   

For more information, see [SAP Help Portal - Security](https://help.sap.com/docs/btp/sap-business-technology-platform/btp-security?locale=en-US&version=LATEST)

<br>





### Add additional Platform Users using Default Identity Provider

SAP ID service is the default identity provider for SAP BTP. You can start using it without further configuration. 


1. Choose your global account to which you want to add members.

2. In the navigation area, choose "Security" --> "Users".

3. Choose "Create".

   ![Add platform user in global account](images_02/2_3_5_create_platform_user.png)

4. Enter the e-mail address, choose the identity provider, and choose "Create".

   ![Add platform user in global account](images_02/2_3_6_add_user2.png)

5. Click on the new user. In the detail window, click on "Role Collections" and "Assign Role Collections".

6. Add the required role, "Global Account Administrator" or "Global Account Viewer". 

   ![Add platform user in global account](images_02/2_3_7_assign_rolec.png)

You can delete shadow users provided by the default identity provider, but you cannot delete the default identity provider itself. It will work independently of your custom identity provider.

For more information, see [SAP Help Portal - Add Members to Your Global Account](https://help.sap.com/docs/btp/sap-business-technology-platform/add-members-to-your-global-account).

<br>


### Establish Trust with your Cloud Identity Services

Before you can use Cloud Identity Services (CIS) in your Global Account, you must establish trust between your Global Account and your CIS.

1. Navigate to "Security" --> "Establish Trust".

   ![Establish Trust](images_02/2_3_10_establishtrust.png)

2. Select your cloud identity services tenant you want to use.

   ![Establish Trust](images_02/2_3_11_trust_1.png)

3. Configure the name for the Customer Identity Provider for Platform Users 

   ![Establish Trust](images_02/2_3_12_trust_2.png)
   
4. Select the domain you want to use. Default is "accounts.ondemand.com".

   ![Establish Trust](images_02/2_3_13_trust_3.png)

5. Review your configurations and click "Finish".
   
   ![Establish Trust](images_02/2_3_14_trust_4.png)
   
6. Check the results. You can now create user accounts with users from the customer identity provider.

   ![Establish Trust](images_02/2_3_15_trust_result.png)


<br>