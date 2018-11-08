# Flutterwave Rave FirebirdCloud Domain and Hosting Reseller PHP Payment Integration Kit
Flutterwave's Rave PHP payment gateway integration kit for FirebirdCloud's white label web host reseller platform. Become the "Domain and Hosting Reseller" with Nigeria's leading domain and web hosting resseller. Get your web hosting business started instantly at no cost and accept payment using this Flutterwave Rave PHP payment gateway integration kit.

## Prerequisite
- Before you can use this script, you will need to have an FirebirdCloud Domain and Hosting reseller account. Create a free account now if you haven't already done so: https://firebirdcloud/reseller.php?action=partnersite
- Before you can start integrating Rave by Flutterwave, you will need a Rave account. Create a free account now if you haven't already done so: https://rave.flutterwave.com/signup

## Introduction

The system has the built-in ability to allow you to integrate Paystack to allow your Customers / Sub-Resellers to pay you. What we have done is, built a module that can pass parameters to an intermediate bridge on your server, that you can then integrate with any Payment Gateway of your choice.

The logic of the flow in this integration is quite simple:
1. Any Customer / Sub-Reseller of yours needs to pay you money and selects a Payment Gateway to do so.
2. We simply create a collection of messages that you will need to charge this Customer / Sub-Reseller. This set of messages would contain things like Order Information, Amount etc. We then redirect the Customer to your Server with this set of messages.
3. You then charge the Customer / Sub-Reseller using these messages, and your Payment Gateway(in this case Paystack).
4. You then redirect the Customer back to our Server with a status of the transaction as to whether you have successfully charged the Customer / Sub-Reseller.
5. Once this is done we Add these funds to the Customer / Sub-Reseller account, and/or process any associated Orders.

# Setup

## STEP 1: Integrate this kit with your website (eg. using cPanel)
Unarchive the content of the repo into your server

## STEP 2: Select the correct Checksum Algorithm within your Reseller Control Panel:
1. Login to your Reseller Control Panel.
2. In the Menu, point to Settings -> Finance and Billing -> Payment Gateway and click List / Add.
3. Click the Manage button next to the Custom Payment Gateway that you are upgrading.
4. Select the Checksum Algorithm as MD5 and save your changes by clicking Submit.

## STEP 3: Adding the Paystack Custom Payment Gateway
Next, you need to Add the Paystack Payment Gateway to our system.
You can Add or Modify your current/preferred Payment Gateway within your Reseller account by following the steps given below:
1. Login to your Reseller Control Panel.
2. In the Menu, point to Settings -> Finance and Billing -> Payment Gateway and click List / Add.
3. Click the Add a Gateway link.
4. Click the Add any other Payment Gateway link.
5. Enter the following details and save your changes by clicking Submit:
- Gateway Name: This is the heading for your Payment Gateway and it will be displayed to your Customers / Sub-Resellers on the Payment page within a dropdown of options. A typical heading could be Debit card/Mastercard/Visacard/Bank in order to signify that your Customer / Sub-Reseller can pay using those modes if they select this particular option.
- Gateway URL: This is the URL on your server to which we will redirect the Customer / Sub-Reseller. This is explained in detail further ahead. Currently, simply fill in some URL. We will change this later to the correct URL.
- Payment Gateway Access Level for Customers / Sub-Resellers: Select appropriate Access Levels for your Customers / Sub-Resellers.
- Send me a Reminder if a transaction is pending for more than x days: In case you have not yet accepted a payment sent to you via this Payment Gateway, you can get e-mail reminders sent to you daily after x number of days from the payment date, until you either Approve or Decline these payments.
- Display Position: If you plan on adding multiple Payment Gateways you can select the position in which you wish to display this Gateway on your Payment Page.
- Checksum Algorithm: Select MD5 if you have downloaded the latest Integration Kit (version 2 or above) or have followed the upgrade instructions listed in Step 1. Select Addler 32 only if you are still using an older kit and haven't yet upgraded.

## STEP 4: Preparation on your Server
On your own server, upload all the files from this integration kit. Some of the files included are:

paymentpage.php: This is the page that we will redirect your Customer / Sub-Reseller to. From this page, you need to collect the data we send and use the data to charge your Customer / Sub-Reseller. After you have charged the Customer / Sub-Reseller you will then redirect the Customer / Sub-Reseller to postpayment.php.

postpayment.php: This page simply redirects your Customer back to our Server after you have charged him, with appropriate variables required by our Server.

functions.php: This is just a functions file used by the other pages for certain calculations.

- Both the paymentpage.php and the postpayment.php pages contain a variable called KEY. For instance, in the above two files you will find a line as follows:

    $key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"; //replace ur 32 bit secure key , Get your secure key from your Reseller Control panel
You need to replace this value in both the files with the KEY we generated for you at the time of adding the Gateway. You can check it from the Settings -> Finance and Billing -> Payment Gateway -> List / Add section by clicking the Payment Gateway that you added.

If at anytime you feel that you may have compromised the security of this Key, you can regenerate a new one from this section by clicking the Generate Key button. You will then have to replace the New Key in your code.

- Edit the Rave specific parameters on paymentpage.php and postpayment.php

## STEP 5: Set the Gateway URL
You will now need to set the Gateway URL which we skipped earlier while adding the Gateway. The Gateway URL is the full http:// URL that will be used to access the paymentpage.php on your server. So a typical Gateway URL would look like "http://www.yourserver.com/paymentpage.php".

Visit the Settings -> Finance and Billing -> Payment Gateway -> List / Add section within your Reseller Control Panel and click the Manage button next to the Payment Gateway you added. Click the Modify button and enter the Gateway URL as described above. Make sure the URL is entered complete with the "http://" or "https://" all the way up to the name of the page. DO NOT pass any Parameters to the URL.

CORRECT GATEWAY URL: http://www.yourserver.com/paymentpage.php
WRONG GATEWAY URLS: www.yourserver.com/paymentpage.php http://www.yourserver.com/paymentpage.php?someparam=something

## STEP 6: Testing the Integration so far
You are now ready to test your integration and verify that it works. Follow the steps below to Test your Integration:
1. Login to your Reseller Control Panel.
2. In the Menu, point to Settings -> Finance and Billing -> Payment Gateway and click List / Add.
3. Click the Manage button next to the Payment Gateway you added.
4. Click Test for Add Funds or Test for Payment, depending upon the type of transaction you wish to test.

This will popup a new window to redirect you to the Gateway URL you had specified
