# Navigation

| Exercise | Link |
|---|---|
| Previous | [Exercise 1 - What is an Org and Space in CF](../Exercise-01-What-is-OrgandSpace-CF)
| Next | [Exercise 3 - Publish Wishlist](../Exercise-03-Publish-Wishlist)
| Start | [Overview](../README.md)



# Exercise 2 - Setup

<a name="1-web-ide-full-stack"></a>
## 1. SAP Web IDE Full-Stack

The primary development tool for these hands-on exercises is [SAP Web IDE Full Stack](https://help.sap.com/viewer/825270ffffe74d9f988a0f0066ad59f0/CF/en-US/c175c03da2534e4b9b3ea28687f6cb0a.html) - a browser-based IDE in which you can easily develop, test, build, deploy and extend role-based, consumer-grade applications for business users.

For the sake of simplicity in this document, we will refer to the 'SAP Web IDE Full-Stack' either as 'Web IDE Full-stack' or just 'Web IDE'.

In order to use Web IDE, you would normally need to configure the service and assign appropriate authorisations, etc.  However, for the purpose of this exercise, the user account provided to you by the instructor has been preconfigured with access to Web IDE.

Access Web IDE by [clicking here](https://webidecp-aevblwuamw.dispatcher.hana.ondemand.com/) and using the login information provided for you by the instructor.


<a name="2-configure-cloud-foundry"></a>
## 2. Configure Cloud Foundry

Before proceeding with development, we need to configure Web IDE to point to our allocated Space within our Cloud Foundry account.

Within this assigned space, we will then need to install a tool called the "Builder".  This tool performs all the actions needed when we want to build or deploy our applications into our Cloud Foundry Space.  For instance, if you wish to build a [Multi-tennant Application archive](https://help.sap.com/viewer/58746c584026430a890170ac4d87d03b/Cloud/en-US/ba7dd5a47b7a4858a652d15f9673c28d.html) from the artefacts described in your project’s MTA development descriptor (`mta.yaml`) file, then the Builder tool will perform this task for you.

1. Connect to Web IDE Full Stack

1. Select the  _Preferences_  
    ![Web IDE Preferences](./images/Icon_Preferences.png)  
    This is done either by clicking on the gear icon at the bottom of the vertical tool bar on the left-hand side of the screen, or by following the menu option _Tools -> Preferences_.  

1. Choose _Workspace Preferences - Cloud Foundry_

    ![CF Config](images/setup6_cf_config.JPG)

1. Select the API Endpoint `https://api.cf.eu10.hana.ondemand.com` 
1. Enter your User Name and password when prompted
1. Verify that the Organisation is set to `TechEd2018_OPP363` and the Space is set to `OPP363_SPACE_XXX` (where XXX is your assigned student number)
1. Click **_Save_** otherwise the API endpoint configuration will be lost!
1. Click _Install Builder_ (This will take several minutes to complete)


<a name="3-enable-web-ide-features"></a>
## 3. Enable Extra Features in Web IDE

In order to complete these exercises, we will need to use some extra features of Web IDE that are not enabled by default. The following steps describe how to enable these specific features.

1. In the _Preferences_ screen, select _Workspace Preferences - Features_

    ![Web IDE features](images/setup4_web_ide_features.JPG)

1. Search for two features, **SAP HANA Database Explorer** and **Tools for Node.js Development**

   ***IMPORTANT***  
   Each time SAP updates a Feature, the version number is incremented, and from a visual point of view, the background colour of the Feature's icon is changed.  Therefore the icon colours shown in the screenshot below are unlikely to match the icon colours you see on your screen.

    ![HANA DB](images/setup5_hana_db.JPG)


    ![node.js](images/setup5b_nodejs.JPG)

1. Switch both of these feature _ON_ and click _Save_ at the bottom of the screen

1. Since you have activated some new features, you must restart Web IDE by selecting _Refresh_ in the pop-up window

1. You can verify that the HANA Database Explorer feature has been enabled by looking for the icon shown below in the vertical toolbar on the left side of the screen

    ![SAP HANA Database Explorer](./images/Icon_Database_Explorer.png)



<a name="4-simplify-copy-paste"></a>
## 4. Simplify the Copying of Code Blocks from GitHub

During this session, you will often need to copy large blocks of code from the `README.md` documentation files. To make this easier and reduce the risk of copy-paste errors in your code, you can install a simple add-on for Chrome called _Tampermonkey_ and then a GitHub-specific user script to provide you with a _Copy to clipboard_ button for the code blocks in the exercises.

1. Open the Chrome browser.
1. Open the Tampermonkey extension URL <https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en-US>
1. Click _Add to Chrome_.
1. When the extension has been added, restart Chrome.
1. You should now see the TamperMonkey toolbar button in the top right of your browser.

    ![tampermonkey toolbar](images/setup7_tampermonkey.JPG)

1. Open the URL <https://raw.githubusercontent.com/Mottie/GitHub-userscripts/master/github-copy-code-snippet.user.js> to install the _Github copy code snippet_ user script.
1. Restart Chrome

During the exercises, the copy to clipboard icon will now appear whenever when you hover the mouse over a code block.

![tampermonkey toolbar](images/setup8_copy_code_block.JPG)



<a name="5-saving-web-ide-changes"></a>
## 5. Tips on Saving your Changes in SAP Web IDE Full-Stack

As in any development environment, it's important to save your work regularly to avoid losing your changes, this is particularly true in Web-based IDEs. As a general rule of thumb, try to follow the policy of: _"Save early, save often."_

1. Note that there are two _Save_ buttons in SAP Web IDE Full-Stack

    ***Save*** will only save the file currently being edited  
    ***Save All*** will save all currently open and unsaved files.

    ![save buttons](images/setup9_save_buttons.jpg)

1. Under _Preferences -> Code Editor -> Save Options_, there are some optional settings to:
    * "Automatically save changes in open documents every 30 sec", and
    * "Beautify the code of active documents on manual save"

    You can decide for yourself whether the Beautify option is of any use to you, but we recommend that the auto-save option is always enabled.

    ![autosave](images/setup10_save_prefs.JPG)


<a name="6-verify-cli-plugins"></a>
## 6. Verify installation of Cloud Foundry CLI

Open a _Command Prompt_ and run the command `cf plugins`.  You will see output similar to the following

```
$ cf plugins
Listing installed plugins...

plugin      version   command name                 command help
MtaPlugin   2.0.3     bg-deploy                    Deploy a multi-target app using blue-green deployment
MtaPlugin   2.0.3     deploy                       Deploy a new multi-target app or sync changes to an existing one
MtaPlugin   2.0.3     download-mta-op-logs, dmol   Download logs of multi-target app operation
MtaPlugin   2.0.3     mta                          Display health and status for a multi-target app
MtaPlugin   2.0.3     mta-ops                      List multi-target app operations
MtaPlugin   2.0.3     mtas                         List all multi-target apps
MtaPlugin   2.0.3     purge-mta-config             Purge no longer valid configuration entries
MtaPlugin   2.0.3     undeploy                     Undeploy a multi-target app

Use 'cf repo-plugins' to list plugins in registered repos available to install.
```

It is possible that plugins other than the ones shown above may be listed, but the **MtaPlugin** plugins you require are:

* `mta`
* `deploy`
* `bg-deploy`

This completes the system setup for your exercises.

<hr>
© 2018 SAP SE
<hr>

# Navigation

| Exercise | Link |
|---|---|
| Previous | [Exercise 1 - What is an Org and Space in CF](../Exercise-01-What-is-OrgandSpace-CF)
| Next | [Exercise 3 - Publish Wishlist](../Exercise-03-Publish-Wishlist)
| Start | [Overview](../README.md)


