---
title: "WebDAV Sharing"
description: "Instructions for users migrating from the deprecated built-in SCALE WebDAV sharing feature to the WebDAV (DAV) application."
weight: 30
aliases:
tags:
- scalewebdav
---

This article provides instructions on migrating configurations from the deprecated WebDAV feature to the WebDAV (DAV) application.
This application is a set of extensions to the HTTP protocol which allows users to collaboratively edit and manage files on remote web servers, and serves as the replacement for the built-in TrueNAS SCALE WebDAV feature.

You can run the WebDAV application as a non-root administration user. 
When installed and configured with at least one share, a container launches with root privileges.
This allows you to apply the correct permissions to the WebDAV shares and directories.
After this, the WebDAV container runs as a non-root user.

## Before You Begin

Before you configure the new WebDAV application:

* Disable the WebDAV service.
  Go to **System Settings > Services** and disable the service, then clear the **Start Automatically** checkbox to prevent the service from re-enabling after a system restart.

* Review your WebDAV service authentication settings and note all IP addresses, port numbers, URLs and credentials (username and password).

If you want to grant access to a specific user (and group) other than the defaults, add the new non-root administrative user and take note of the UID and GID for this user.

## Migrating from WebDAV Service

After disabling the WebDAV service, install the WebDAV application. 
Go to **Apps** click on **Available Applications** and locate the **WebDAV** application widget.

{{< trueimage src="/images/SCALE/22.12/WebDAVAppWidget.png" alt="WebDAV Application Widget" id="1 WebDAV Application Widget" >}}

Click **Install** to open the **webdav** configuration wizard.
Select the authentication from the **Authentication Type** dropdown. Selecting **Basic Authentication** displays credential settings.

{{< trueimage src="/images/SCALE/22.12/WebDAVConfigurationBasicAuth.png" alt="WebDAV Configuration Basic Authentication" id="2 WebDAV Configuration Basic Authentication" >}}

Enter the username and password information for your WebDAV share (from the WebDAV service settings).

Select **Enable HTTPS** to enable for WebDAV. 

{{< trueimage src="/images/SCALE/22.12/WebDAVNetworkConfigForHTTPS.png" alt="WebDAV Network Configuration for HTTPS" id="3 WebDAV Network Configuration for HTTPS" >}}

Select **truenas_default Certificate** from the **Certificate** dropdown list.

Add your existing WebDAV share to the application.
Click **Add** to the right of **Shares** in the **Storage Configuration** section. 

{{< trueimage src="/images/SCALE/22.12/WebDAVStorageConfigAddShare.png" alt="WebDAV Storage Configuration Add Share" id="4 WebDAV Storage Configuration Add Share" >}}

Enter the name for the share, which can be your existing WebDAV share. 
Enter a description if you want but this is only for internal use.
Enter or browse to the host path location for the WebDAV share dataset. 
Select **Read Only** to make the share read only and disable write access to the share. If selected, data mounts as read only. 

Select **Fix Permissions** to change the owner of the share to a different user other than the default user and group **568**. 
If you want to specify a different user, enter the user ID (UID) and group ID (GID) in the **User and Group Configuration** fields for these settings.

Click **Save** to complete the installation and configuration.

## Testing the Share

At the end of this migration process, test access to your WebDAV share.

{{< taglist tag="scalewebdav" limit="10" title="Related WebDAV Articles" >}}