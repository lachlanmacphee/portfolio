---
layout: ../../layouts/BlogPostLayout.astro
date: "2025-09-11"
title: "ERP for Everyone 02: Setup"
description: "Get your company information into the ERP and add users to help with the setup."
status: "published"
---

Assuming you gave the commands 5-10 minutes to run, and you didn't see any errors, you should now have ERPNext installed on your VPS and accessible via your domain.

Head to `erp.yourdomain.com` (replace `yourdomain.com` with your actual domain) in your web browser. You should see a login screen that looks like this:

![The login page of ERPNext](../../images/erpnext-setup-login.png)

Enter the username `Administrator` and the password `admin`. You will then see a welcome screen. Select the settings suited to your location and the currency that your business operates in:

![The welcome page of ERPNext](../../images/erpnext-setup-welcome.png)

You then need to setup an account. Enter your full name, email address (this is also used for notifications, so it should ideally be a dedicated account like `erp@yourcompany.com`), and a password (50+ characters ideally), then click "Next"

![The account setup page of ERPNext](../../images/erpnext-setup-account.png)

Next, input your organisation's details. This includes the name, abbreviation, chart of accounts, and financial year start date. Do **not** tick the `Generate Demo Data` box, we want to start with a clean slate.

![The organisation setup page of ERPNext](../../images/erpnext-setup-organisation.png)

Now, it will show you a loading screen while it sets up your organisation. This may take a few minutes, so be patient.

![The loading page of ERPNext](../../images/erpnext-setup-loading.png)

Once it's finished, you'll see the ERPNext dashboard. Congratulations, you've successfully installed and set up ERPNext for your organisation! The only thing left to do for this blog post is to add any other users that will help you with the setup.

![The ERPNext dashboard page](../../images/erpnext-setup-dashboard.png)

Head to `https://erp.yourcompany.com/app/user` and click the `Add User` button in the top right. Fill out the email and first name of the new user, and allocate them roles based on what they do in the business. In general, you should aim to allocate the minimum amount of roles for them to do what they need to do. If you're not sure which role to allocate, just take a guess, you can always allocate them more later!

![The ERPNext add user page](../../images/erpnext-setup-add-user.png)

That's all for this blog post! In the next one, we'll dive into setting up the items that your company buys and sells. Click [here](https://lachlanmacphee.com/blog/006-erpnext-items) to move to the next step.
