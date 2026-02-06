# Set Up SAP Mobile Start

SAP Mobile Start provides business information from SAP Start, SAP Build Work Zone, standard edition, and SAP Build Work Zone, advanced edition. It runs on iOS, iPadOS, and Android devices, as well as on watchOS and Wear OS devices, and on Apple Vision Pro.


#### Prerequisites

This mission requires that you have successfully set up **SAP Start** and Identity Provisioning for SAP Build Work Zone. It uses the "SAP Start" Site, which is already enabled for SAP Mobile Start.


### Download and Register SAP Mobile Start

For more information and alternative set-ups for the SAP Mobile Start app, see SAP Help Portal [SAP Mobile Start - User Guide](https://help.sap.com/docs/mobile-start/user-guide/installing?locale=en-US&version=LATEST).

#### Procedure for SAP Start Site

1. Open your SAP Start Site. Click your User, then select "Settings".

    <img src="imagesstart/6_5_1_sapstart.png" alt="Set up Mobile Start" width="600">

2. Scan the QR Code. You get forwarded to your App Store. Download the app.

    <img src="imagesstart/6_5_2_downloadapp.png" alt="Set up Mobile Start" width="400">

3. Once downloaded, you can scan the QR Code to register your app.

    <img src="imagesstart/6_5_3_register.png" alt="Set up Mobile Start" width="400">

4. The link opens your app. Depending on your setup, you may need to authenticate with the Custom IdP in your SAP Build Work Zone.

    <img src="imagesstart/6_5_4_authenticate.png" alt="Set up Mobile Start" width="250">

5. Create a Pass Code for your app. 

    <img src="imagesstart/6_5_5_passcode.png" alt="Set up Mobile Start" width="250">

6. Enter your Mobile Start App. Add your favorite apps to your Favorites.

    <img src="imagesstart/6_5_6_mobileapp.png" alt="Set up Mobile Start" width="300">


### Manage Mobile Settings

To configure SAP Mobile Start, first set up and configure roles for your mobile admins in your Subaccount.

For more information about SAP Mobile Start administration, see SAP Help Portal [SAP Mobile Start - Administration Guide](https://help.sap.com/docs/mobile-start/mobile-start-administration-guide/overview?version=LATEST&locale=en-US).




1. Enter your Subaccount. Navigate to "Security" --> "Role Collections". Create a new Role Collection "MobileTenantAdmin".

    <img src="imagesstart/6_5_11_createnewmobilerc.png" alt="Set up Mobile Start" width="500">

2. Click on the new Role Collection. In the details page, click "Edit".

    In the "Roles" section, select the role "MobileAdmin". Click "Add" and "Save".

    <img src="imagesstart/6_5_12_add_mobilerole.png" alt="Set up Mobile Start" width="500">

3. Go to "Users". Assign the new Role Collection to your User.

    <img src="imagesstart/6_5_13_userassignrc.png" alt="Set up Mobile Start" width="500">

4. Enter your SAP Build Work Zone Site Manager. Go to "Settings" --> "Mobile Settings". Enter the SAP Mobile Services admin cockpit.

    <img src="imagesstart/6_5_14_mobilesettings.png" alt="Set up Mobile Start" width="600">

5. Go to Registered Devices. You see, your device has been registered.

    Optional: send a notification to your device. 

     <img src="imagesstart/6_5_15_mobilesettings_2.png" alt="Set up Mobile Start" width="600">

6. Go to Settings and review your Settings. For more information about Mobile Services Admin Cockpit, see SAP Help Portal[SAP Mobile Start – Administration Guide](https://help.sap.com/docs/mobile-start/mobile-start-administration-guide/overview?version=LATEST&locale=en-US).


     <img src="imagesstart/6_5_16_settings.png" alt="Set up Mobile Start" width="600">


<br>

Congratulations, you finished the initial setup of SAP Mobile Start.
