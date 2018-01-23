---
title: Device Based Authentication Type
keywords: homepage
sidebar: overview_sidebar
permalink: AuthType_DeviceBased.html
toc: true
summary: A brief introduction to Device Based Authentication type within NHS Digital's Care Access Service.
---

The Device ID (Match) module provides device fingerprinting functionality for risk-based authentication. 

The Device ID (Match) module collects the unique characteristics of a remote user's computing device and compares them to characteristics on a saved device profile. 

The module computes any variances between the collected characteristics to those stored on the saved device profile and assigns penalty points for each difference.

In general, you can configure and gather the following device characteristics:

> * User agents associated with the configuration of a web browser
> * Installed fonts
> * Plugins installed for the web browser
> * Resolution and color depth associated with a display
> * Timezone or geolocation of a device

For example, when a user who typically authenticates to AM using Firefox and then logs on using Chrome, the Device ID (Match) module notes the difference and assigns penalty points to this change in behavior. 

If the module detects additional differences in behavior, such as browser fonts, geolocation, and so forth, then additional points are assessed and calculated.

If the total number of penalty points exceeds a pre-configured threshold value, the Device ID (Match) module fails
