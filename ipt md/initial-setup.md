# Initial Setup

## Data directory

**📌 NOTE**\
This step is only shown if the data directory was not already configured during installation.

The first time the IPT is run, you will be presented with a few simple steps to prepare the IPT for use. First it requires a location where the data for the IPT installation can be stored. The format of the location entered on the page must conform with the standard for an absolute path to a directory on the operating system where the IPT is installed; relative paths are not supported. For example, use a path such as `C:\datadir` for Windows environments or `/srv/datadir` for Unix and Mac OS X environments. The IPT must have write permission to the selected location. If it does, the path can be entered in the text box provided and then click on the button labelled "Save" - the directory will be created if it doesn’t already exist. It is permissible to create the data directory first with the appropriate write permissions, then enter the absolute path to the directory in the text box and click on the "Save" button.

**🔥 CAUTION**\
Do not select a data directory that is vulnerable to inadvertent changes or removal. Do not use `/tmp`, for example, on systems where this folder may be emptied on a system restart. **The data directory should be backed up regularly in keeping with an appropriate disaster recovery plan.** Loss of the contents of the data directory will result in the loss of resource, user, and other configuration information and customizations to the IPT installation.

**📌 NOTE**\
If you have a data directory from a previously running IPT of the same version and want to use that previous configuration (including users and resources), you can enter the absolute path of that data directory in this first step of the IPT setup. Clicking on "Save" in this case will bypass the page titled IPT setup II and present the IPT Administration page.

**📌 NOTE**\
If you receive an error stating the location is not writable, see [the FAQ item on this](faq.adoc#file-permissions).

**💡 TIP**\
Click on the language name in the upper right hand corner to see whether your preferred language is available to use the IPT in.

![IPTSetup-1-dataDirectory](ipt2/setup/IPTSetup-1-dataDirectory.png)

## Administrator user

If the initial data directory assignment step was successful, the IPT will present a second setup page (see screen image, below) on which the information about the default administrator of the IPT must be entered.

The default administrator will have a distinct login and the authority to make changes to all aspects of the IPT installation. The default administrator will be able to make additional user accounts, including other administrators having the same authority to make changes. Though administrators can be added and removed, the IPT must always have at least one. Following are explanations of the fields encountered on the second setup page:

* **Email** - the full, active email address of the default administrator of the IPT installation.
* **First name** - the first name of the default administrator.
* **Last name** - the last name of the default administrator.
* **Password** - a password for the default administrator.

  <dl><dt><strong>📌 NOTE</strong></dt><dd>

  The password should be made secure and safe from loss, as it is not recoverable from the IPT application.
  </dd></dl>
* **Verify password** - an exact copy of the password as entered in the Password text box to confirm that it was entered as intended.

![IPTSetup-2-administrator](ipt2/setup/IPTSetup-2-administrator.png)

## IPT Mode

If the second step was successful, the IPT will present a third setup page (see screen image, below) on which the information about the IPT mode must be entered.

**⚠️ WARNING**\
for a given installation, this selection is final and cannot be changed later on.

The IPT mode decides whether the hosted resources will be indexed for public search access by GBIF. GBIF recommends IPT administrators try Test mode first in order to understand the registration process, and then reinstall in Production mode for formal data publishing. To switch from test to production mode or vice versa, you will have to reinstall your IPT and repeat any configurations you made.

* **IPT mode**

  Choose between Test mode and Production mode. Test mode is for evaluating the IPT or running it in a training scenario, and registrations will go into a test registry and resources will never be indexed. All DOIs minted for resources in test mode should use a test prefix (which can be requested from DataCite), meaning they are temporary. Production mode, on the other hand, is for publishing resources formally, and resources are registered into the GBIF Registry and will be indexed. DOIs minted for resources cannot be deleted, and require resources to remain publicly accessible.

![IPTSetup-3-mode](ipt2/setup/IPTSetup-3-mode.png)

## Public URL

If the third step was successful, the IPT will present a fourth setup page (see screen image, below) on which the information about the IPT mode must be entered.

The public, Internet-accessible URL that points to the root of this IPT installation. The URL is detected automatically if possible.  On production systems it needs to be accessible via the Internet in order for the IPT to function fully.  Configuring the IPT Public URL to use localhost, for example, will not allow the IPT to be registered with GBIF, will not allow the IPT to be associated with an organization, and will not allow resources to be publicly accessible.

* Institutional proxy URL (optional)

  If the server on which the IPT is installed does not have direct HTTP/HTTPS access to the Internet, but instead must route outbound HTTP/HTTPS requests through an institutional proxy server, enter the host address and port number here.  For example, `http://proxy.example.org:8080`.

![IPTSetup-4-url](ipt2/setup/IPTSetup-4-url.png)

When all the information on the page is complete and correct, click on the button labelled "Save" to complete the IPT setup process. If a problem occurs, an error message will appear at the top of the page with recommendations about how to resolve the issue. Provided the issue has been resolved, restarting the web server will make it disappear. If the setup is successful, a page confirming the success of the setup will appear.

![IPTSetup-5-complete](ipt2/setup/IPTSetup-5-complete.png)

Click on the button labelled "Continue" to open the IPT Administration page (see the screen image, below), from which further configuration of the IPT can be accomplished. Please review the explanations of all of the Administration functions before continuing. Details about the options presented on this screen are given in the [Administration Menu](administration.adoc) section. Before adding data resources to the IPT, the administrator must, at a minimum, verify the IPT settings, set the GBIF registration options, and associate the IPT with an organization.

![IPTAdminBeforeRegistration](ipt2/administration/IPTAdminBeforeRegistration.png)

Once you have completed the steps in this Getting Started Guide, your IPT is ready to add resources (data sets and metadata). You may want to complete one or more of the tutorials to understand how common IPT tasks are accomplished. For detailed explanations of any further aspects of the IPT, consult the following sections of this user manual.
