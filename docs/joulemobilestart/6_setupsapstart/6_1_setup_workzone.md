# Subscribe to SAP Build Work Zone, Standard Edition Service


### Prepare your Subaccount

1. Enter your Subaccount. Open "Entitlements" and search for "work zone".

   Check that your Subaccount is entitled to "SAP Build Workzone, standard edition" with the Service Plans:
   - standard (Application)
   - optional: free (Application)
   - optional: standard 

   <img src="imageswz/6_1_1_entitlements_wz.png" alt="Subscribe to Build Work Zone Service" width="600" />

2. If your Subaccount is not entitled, click "Edit" and "Add Service Plans".

    <img src="imageswz/6_1_2_addserviceplan.png" alt="Subscribe to Build Work Zone Service" width="600" />

3. Search for "SAP Build Work Zone, standard edition" and select the Service Plan(s) "standard (Application)", and optional "free (Application)" and "standard".

    Click "Add Service Plans," then save your settings.
   
    <img src="imageswz/6_1_3_addworkzone.png" alt="Subscribe to Build Work Zone Service" width="600" />

4. Navigate to "Security" --> "Trust Configuration". Ensure trust is established with your Custom Identity Provider.
   
    <img src="imageswz/6_3_2_trustconfigured.png" alt="Subscribe to Build Work Zone Service" width="600" />


5. If you do not have a Custom Identity Provider for Applications, create one. Click "Establish Trust" and choose your custom IdP tenant. Follow the steps from the previous chapter.

   If you have an S/4HANA Cloud Backend System, and you consider integrating it, use the same Custom Identity Provider. 
      
   <img src="imageswz/6_1_4_establishtrust.png" alt="Subscribe to Build Work Zone Service" width="600" />


### Subscribe to the Service.

1. In your Subaccount, go to "Services" --> "Instances and Subscriptions".

   Select "Create".

    <img src="imageswz/6_1_5_create_1.png" alt="Subscribe to Build Work Zone Service" width="600" />

2. Select the Service "SAP Build Work Zone, standard edition" and the Service Plan "Standard (Application"). 

   You can also use "free (Application)" for your first steps and update later to "standard" if your scenario requires it.

   Choose "Create".

   Mark the checkbox "I understand that enabling a service might result in costs, depending on the plan selected."

    <img src="imageswz/6_1_6_create_2.png" alt="Subscribe to Build Work Zone Service" width="600" />

3. The should be "Subscribes".

    <img src="imageswz/6_1_7_subscribed.png" alt="Subscribe to Build Work Zone Service" width="600" />

4. Go to "Security" --> "Users", click on your user to enter the detail screen. Assign the Role Collection "Launchpad Admin".

    <img src="imageswz/6_1_8_add_rc_admin.png" alt="Subscribe to Build Work Zone Service" width="600" />

5. Optional: You can also assign the Role Collections to a User Group from your Custom Identity Provider and assign this User Group to your Business User in your Custom IdP.

6. Go back to your Subscription and click on "SAP Build Work Zone, standard edition". Sign in using your Custom Identity Provider.

    <img src="imageswz/6_1_9_signin.png" alt="Subscribe to Build Work Zone Service" width="250" />

7. You entered your Work Zone Subscription. Check what's pre-configured.

    <img src="imageswz/6_1_10_enterworkzone.png" alt="Subscribe to Build Work Zone Service" width="500" />

<br>



### Create your First Business Site with Apps

This short guide follows the tutorial [Create a Business Site Using SAP Build Work Zone, standard edition](https://developers.sap.com/mission.launchpad-cf.html).

1. In the Site Directory, click on "Create Site" and provide a name, e.g., "my_first_site". Click "Create". After creation, the "Site Settings" opens.

   Click "Edit" and change the "View Mode" to the more modern "Spaces and Pages - New Experience". "Save" your changes.

    <img src="imageswz/6_1_11_changeviewmode.png" alt="Manage your Build Work Zone Site" width="600" />

2. In your Site Settings, navigate to "Roles Assignments". Make sure the Role "Everyone" is assigned.

    <img src="imageswz/6_1_12_roles.png" alt="Manage your Build Work Zone Site" width="600" />

3. Go back to your Site Directory.

4. Select the Content Manager and "Create" --> "App".

   Provide a name, e.g., "ShoppingCart", and provide the URL: "https://sapui5.hana.ondemand.com/test-resources/sap/m/demokit/cart/webapp/index.html".

   Keep the other values.

   <img src="imageswz/6_1_15_create_app.png" alt="Manage your Build Work Zone Site" width="600" />

5. Select the "Navigation" Tab and enter under "Intent":

    - Semantic Object: Order
    - Action: Display

    and "Save". 
    
6. The App is now available in the Content Manager. Enter the Content Manager, click the Role "Everyone," and select "Edit". You can now assign the new app to the Role Everyone. Don't forget to "Save".

   <img src="imageswz/6_1_16_assign_role.png" alt="Manage your Build Work Zone Site" width="600" />


7. Go back to your Content Manager and create a "Page". Name it, e.g., "Overview", and click "Add Section". Click "Add Widget".

   <img src="imageswz/6_1_17_add_widget.png" alt="Manage your Build Work Zone Site" width="600" />

8. Add your ShoppingCart app. Click "Add" and "Save".

   <img src="imageswz/6_1_18_add_app.png" alt="Manage your Build Work Zone Site" width="600" />

9. Go back to your Content Manager and create a "Space". Provide a name, e.g., "Space".

   Assign your page and "Save".

   <img src="imageswz/6_1_19_add_space.png" alt="Manage your Build Work Zone Site" width="600" />

10. Assign your space to the role "Everyone" and "Save".

    <img src="imageswz/6_1_20_add_spacetorole.png" alt="Manage your Build Work Zone Site" width="600" />

### Enter your Site

1. Go to "Site Directory" and launch your Site.

    <img src="imageswz/6_1_21_entersite.png" alt="Manage your Build Work Zone Site" width="600" />

2. Launch your Shopping Cart App. Click on the tile.

    <img src="imageswz/6_1_22_launchcart.png" alt="Manage your Build Work Zone Site" width="600" />

3. Enjoy your app.

    <img src="imageswz/6_1_23_cartsite.png" alt="Manage your Build Work Zone Site" width="600" />




   
