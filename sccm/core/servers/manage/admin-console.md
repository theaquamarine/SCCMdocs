---
title: Configuration Manager Console
titleSuffix: Configuration Manager
description: Learn about navigating through the Configuration Manager console.
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Using the Configuration Manager console

*Applies to: System Center Configuration Manager (Current Branch)*

Administrators use the Configuration Manager console to manage the Configuration Manager environment. This article covers the fundamentals of navigating the console.  



## Connect to a site server

The console connects to your central administration site server or to your primary site servers. You can't connect a Configuration Manager console to a secondary site. You can [install the Configuration Manager console](/sccm/core/servers/deploy/install/install-consoles). During installation, you specified the fully qualified domain name (FQDN) of the site server to which the console connects. 

To connect to a different site server, use the following steps: 

1. Select the arrow at the top of the [ribbon](#ribbon), and choose **Connect to a New Site**.  

    ![Connect the console to a new site](media/connect-to-a-new-site.png)  

2. Type in the FQDN of the site server. If you've previously connected to site server, select the server from the drop-down list.  

    ![Site Connection window, enter the FQDN of the site server](media/site-server-fqdn.png)  

3. Select **Connect**.  


Starting in version 1810, you can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level. For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## Navigation

Some areas of the console may not be visible depending on your assigned security role. For more information about roles, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration). 


### Workspaces

The Configuration Manager console has four **workspaces**:  

- **Assets and Compliance**  

- **Software Library**  

- **Monitoring**  

- **Administration**  

![Configuration Manager workspaces with context menu](media/configuration-manager-workspaces.png)  

Reorder workspace buttons by selecting the down arrow and choosing **Navigation Pane Options**. Select an item to **Move Up** or **Move Down**. Select **Reset** to restore the default button order.  

 ![Navigation Pane Options window to reorder workspaces](media/navigation-pane-options.png)  

Minimize a workspace button by selecting **Show Fewer Buttons**. The last workspace in the list is minimized first. Select a minimized button and choose **Show More Buttons** to restore the button to its original size.   

![Minimized workspaces in the Configuration Manager console](media/workspace-buttons.png)  


### Nodes

Workspaces are a collection of **nodes**. One example of a node is the **Software Update Groups** node in the **Software Library** workspace. 

Once you are in the node, you can select the arrow to minimize the navigation pane.  

![Example node and highlight minimize arrow](media/software-update-groups-node.png)  

Use the **navigation bar** to move around the console when you minimize the navigation pane.  

![Configuration Manager minimized navigation pane](media/minimized-navigation-pane.png)  

In the console, nodes are sometimes organized into folders. Clicking directly on the folder usually takes you to a **navigation index** or a **dashboard**.  

![Configuration Manager software updates navigation index](media/software-updates-navigation-index.png)  


### Ribbon 

The ribbon is at the top of the Configuration Manager console. The ribbon can have more than one tab and can be minimized using the arrow on the right. The buttons on the ribbon change based on the node. Most of the buttons in the ribbon are also available on context menus.  

![Example ribbon, highlighting multiple tabs and minimize arrow](media/ribbon.png)   


### Details pane

You can get additional information about items by reviewing the details pane. The details pane can have one or more tabs. The tabs vary depending on the node.  

![Configuration Manager example details pane](media/details-pane.png)   


### Columns 

You can add, remove, reorder, and resize columns. These actions allow you to display the data you prefer. Available columns vary depending on the node. To add or remove a column from your view, right-click on an existing column heading and select an item. Reorder columns by dragging the column heading where you would like it to be.  

![Configuration Managers add column](media/add-columns.png)  

At the bottom of the column context menu, you can sort or group by a column. Additionally, you can sort by a column by selecting its header.  

![Configuration Manager group by column](media/column-group-by.png)  

## <a name="bkmk_viewconnected"></a> View recently connected consoles
<!--3699367-->

Starting in version 1902, you can view the most recent connections for the Configuration Manager console. The view includes active connections and those that recently connected. You'll always see your current console connection in the list and you only see connections from the Configuration Manager console. You won't see PowerShell or other SDK-based connections to the SMS Provider. The site removes instances from the list that are older than 30 days.


### Prerequisites to view connected consoles

- Your account needs the **Read** permission on the **SMS_Site** object 
- IIS needs to be installed on the SMS Provider server <!---SCCMDocs-pr issue 1326--> 
- Enable the SMS Provider to use a certificate.<!--SCCMDocs-pr issue 3135--> Use one of the following options:  

  - Enable [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http) (recommended)
  - Manually bind a PKI-based certificate to port 443 in IIS on the server that hosts the SMS Provider role  

### View connected consoles

1. In the Configuration Manager console, go to the **Administration** workspace.  

2. Expand **Security** and select the **Console Connections** node.  

3. View the recent connections, with the following properties:  

    - User name
    - Machine name
    - Connected site code
    - Console version
    - Last connected time: When the user last *opened* the console

![View Configuration Manager console connections](media/console-connections.png) 



## Command-line options

The Configuration Manager console has the following command-line options:

|Option|Description|  
|------------|-----------------|  
|`/sms:debugview=1`|A DebugView is included in all ResultViews that specify a view. DebugView shows raw properties (names and values).|  
|`/sms:NamespaceView=1`|Shows namespace view in the console.|  
|`/sms:ResetSettings`|The console ignores user-persisted connection and view states. The window size isn't reset.|  
|`/sms:IgnoreExtensions`|Disables any Configuration Manager extensions.|  
|`/sms:NoRestore`|The console ignores previous persisted node navigation.|  

## <a name="bkmk_notify"></a> Configuration Manager console notifications
<!--3556016, fka 1318035-->
Starting in Configuration Manager version 1902, the console notifies you for the following events:

- When an update is available for Configuration Manager itself
- When lifecycle and maintenance events occur in the environment

This notification is a bar at the top of the console window below the ribbon. It replaces the previous experience when Configuration Manager updates are available. These in-console notifications still display critical information, but don't interfere with your work in the console. You can't dismiss critical notifications. The console displays all notifications in a new notification area of the title bar.

![Notification bar and flag in console](./media/1318035-notify-eval-version-expired.png)

### Configure a site to show non-critical notifications

You can configure each site to show non-critical notifications in the properties of the site.

1.  In the **Administration** workspace, expand **Site Configuration**, then click on the **Sites** node.
1. Select the site you want to configure for non-critical notifications.
1. In the ribbon, click on **Properties**.
1. On the **Alerts** tab, select the option to **Enable console notifications for non-critical site health changes**.
   - If you enable this setting, all console users see critical, warning, and information notifications. This setting is enabled by default.  
   - If you disable this setting, console users only see critical notifications.  

Most console notifications are per session. The console evaluates queries when a user launches it. To see changes in the notifications, restart the console. If a user dismisses a non-critical notification, it notifies again when the console restarts if it's still applicable.

The following notifications reevaluate every five minutes:
- Site is in maintenance mode  
- Site is in recovery mode  
- Site is in upgrade mode  

Notifications follow the permissions of role-based administration. For example, if a user doesn't have permissions to see Configuration Manager updates, they won't see those notifications.

Some notifications have a related action. For example, if the console version doesn't match the site version, select **Install the new console version**. This action launches the console installer. 

The following notifications are most applicable to the technical preview branch:  

- Evaluation version is within 30 days of expiration (Warning): the current date is within 30 days of the expiration date of the evaluation version  
- Evaluation version is expired (Critical): the current date is past the expiration date of the evaluation version  
- Console version mismatch (Critical): the console version doesn't match the site version  
- Site upgrade is available (Warning): there's a new update package available  

For more information and troubleshooting assistance, see the **SmsAdminUI.log** file on the console computer. By default, this log file is at the following path: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.


## Tips

### Send feedback
<!--1357542-->

Starting in version 1806, submit product feedback from the console.  

- **Send a smile**: Send feedback on what you liked  

- **Send a frown**: Send feedback on what you didn't like  

- **Send a suggestion**: Takes you to UserVoice to share your idea  
 
For more information, see [Product Feedback](/sccm/core/understand/find-help#BKMK_1806Feedback).


### Assets and Compliance workspace

#### View users for a device
Starting in version 1806, the following columns are available in the **Devices** node:  

- **Primary user(s)** <!--1357280-->  

- **Currently logged on user** <!--1358202-->  
    > [!NOTE]  
    > Viewing the currently logged on user requires [user discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) and [user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

For more information on how to show a non-default column, see [Columns](#columns).

#### Improvement to device search performance
<!-- 3614690 -->
Starting in version 1806, when searching in a device collection, it doesn't search the keyword against all object properties. When you're not specific about what to search, it searches across the following four properties:
- Name
- Primary user(s)
- Currently logged on user
- Last logon user name

This behavior significantly improves the time it takes to search by name, especially in a large environment. Custom searches by specific criteria are unaffected by this change. 


### Monitoring workspace

#### Copy details in monitoring views
<!--1357856-->
Starting in version 1806, copy information from the **Asset Details** pane for the following monitoring nodes:  

- **Content Distribution Status**  

- **Deployment Status**  

![Deployment Status view, copy asset details](media/1810-deployment-status.PNG)



## Next steps

[Accessibility features](/sccm/core/understand/accessibility-features)

