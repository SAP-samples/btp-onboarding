## Account Administration Using the SAP BTP Command Line Interface

The SAP BTP command-line interface (BTP CLI) can be used for all account administration tasks, such as creating or updating subaccounts, authorization management, and working with service brokers and platforms. 
It is an alternative to the SAP BTP cockpit for all users who prefer to work in a terminal or want to automate operations using scripts.

>Note: btp CLI is the command line tool of the BTP Platform. It does not replace other CLIs, like [Cloud Foundry CLI](https://tools.hana.ondemand.com/#cloud-btpcli), which you need for the Cloud Foundry runtime, or the [Kyma CLI](https://kyma-project.io/docs/kyma/latest/04-operation-guides/operations/01-install-kyma-CLI) for Kyma runtime or Kubectl. 

### More information and Tutorials


* SAP Help Portal: [Account Administration Using the SAP BTP Command Line Interface](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-using-sap-btp-command-line-interface-btp-cli-feature-set-b?locale=en-US). 
* SAP Help Portal: [Setting Up an Enterprise Global Account via the Command Line](https://help.sap.com/docs/btp/sap-business-technology-platform/setting-up-global-account-via-command-line?locale=en-US)
* SAP Help Portal: [Setting Up a Trial Account via the Command Line](https://help.sap.com/docs/btp/sap-business-technology-platform/setting-up-trial-account-via-command-line?locale=en-US)
* SAP Tutorial [Get Started with the SAP BTP Command Line Interface (btp CLI)](https://developers.sap.com/tutorials/cp-sapcp-getstarted.html)
* SAP Tutorial [Enable SAP BTP, Kyma Runtime Using the Command Line](https://developers.sap.com/tutorials/btp-cli-setup-kyma-cluster.html)
* SAP Tutorial (only Linux) [Automate Account Operations with the Command Line Interface (CLI)](https://developers.sap.com/tutorials/cp-cli-automate-operations.html)

<br>

### How btp CLI works

You download the btp CLI client to your local desktop and access it through the shell of your operating system. The client then accesses all required platform services through its backend, the CLI server, where the command definitions are stored.

![How SAP BTP CLI works](images/6_1_cli_soldia.png)

Figure: btp CLI Solution diagram

<br>

You can download the btp CLI from the [SAP BTP Developer Tools page](https://tools.hana.ondemand.com/#cloud-btpcli).

<br>

### Automating the setup of your SAP BTP account with btp-setup-automator

SAP provides with the newly available GitHub repository for the [btp-setup-automator](https://github.com/SAP-samples/btp-setup-automator) the community a repository with **scripts to automate the setup of an SAP Business Technology Platform** (SAP BTP) account and to learn how this is done with the various command-line interfaces and tools.

The tooling for the btp-setup-automator is running within a Docker container and the repository provides all that you need. 

See also this [SAP blog](https://blogs.sap.com/2022/03/17/automating-the-setup-of-your-sap-btp-account-with-btp-setup-automator/) for further information.
