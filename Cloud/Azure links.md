https://azure.microsoft.com/mediahandler/files/resourcefiles/azure-skills-navigator-for-network-engineers-/Azure%20Skills%20Navigator-%20Network%20EngineerOct10(learn.microsoft).pdf

Here is the list of FREE Udemy tutorials for mastering Azure cloud  
computing.  

✅ Microsoft Azure for Absolute Beginners  
https://lnkd.in/eHm2raD8  

✅ Zero to Hero in Cloud computing Essentials With Azure  
https://lnkd.in/eBQeSV67  

✅ AZ-900 Microsoft Azure Fundamentals https://lnkd.in/dtf_NPA4

✅ AZ-204 Developing Solutions for Microsoft Azure  
https://lnkd.in/eGGfHEyk  

✅ Azure Real World Hand-on Training For Beginners.  
https://lnkd.in/ewZCsnfZ  

✅ Migrate Windows service to Azure https://lnkd.in/eV-3aFpd

✅ Azure Security real world-hands-on for beginners  
https://lnkd.in/eEnR7KE3  

✅ Microsoft Azure Databricks for Data Engineering  
https://lnkd.in/eeGksC_6  

✅ Deploy Azure Virtual Desktop for beginners  
https://lnkd.in/e45q2aTW  

✅ Azure Basics Part 1 (Azure AD, Subscription, Resource Group)  
https://lnkd.in/eNzYJ-fw  

✅ Azure Basics Part2 (Network , Compute and Load Balancers)  
https://lnkd.in/eAcGj4Nc  

✅ Azure Basics Part3 (Storage Account) https://lnkd.in/e9zqNWFD

✅ Azure Basics Part4 (App Service ) https://lnkd.in/ezBy9Nfe

✅ Azure Basics Part 5 Azure with docker Containers  
https://lnkd.in/enc2fMSM  

✅ Azure Serverless Functions https://lnkd.in/eg5h-XfR

✅ Modern Data Architecture using Microsoft Azure  
https://lnkd.in/eiQ7UFh5  

✅ Terraform on Azure - Basic Tutorial https://lnkd.in/ef9bQdf5

✅ Create a 3-Tier Application Using Azure Virtual Machines  
https://lnkd.in/ezUvVNMM  

=======================================

🚨 Did you know about the FREE demo workspace that’s fully loaded  
with events and tables for you to query and practice your \#kql ⁉ 🚨  

👇 👇 👇 ❗❗❗Check it out ❗❗❗ 👇 👇 👇  
https://lnkd.in/ewJAQtZ4  

👉 For KQL breakdowns and pre-built queries you can copy n’ paste,  
check out my KQL repo on GitHub at https://lnkd.in/e-3C8m-g  

👉 For practical use cases (like \#costoptimization ) and exercises in  
KQL, visit my blog at www.hanley.cloud  

💡 Keep up with the latest and follow me on Twitter @IanDHanley  
https://lnkd.in/e3x74inZ  

\#microsoftsecurity🛡 #microsoftsentinel⚔ \#devsecops🛠 \#cybersecuritytips💪  
 \#learn 📚  \#cloudsecurity ☁  \#azure⚡  

=======================================

🤔 🔎 Which Accounts are Firing this Alert in your  
Environment❓❓❓  

https://lnkd.in/ee3Y7hhP

👇This \#kql query shows you exactly that.👇

```Plain
SecurityEvent                                  // <--Define the table to query

| where EventID == "4662"          // <--Declare which EventID you're looking for

| summarize count() by Account  // <--Show how many times that EventID was thrown per account

| render columnchart                     // <--Optional, but helps quickly visualize potential outliers
```

👉 You can swap out ‘SecurityEvent’ for another table/log source  
etc.  

👉 Try changing out the EventID ‘4662’ for another EventID in your  
environment (to track down the ‘noisiest’ EventIDs in a month and figure  
out which EventIDs to plug in, try this query: https://lnkd.in/eaDXNqZW  
)  

👉 You can swap out ‘Account’ for ‘Computer’ or other variable  
associated with the table/log source you’re querying.  

## 👉Rendering the results to a column chart is a great way to quickly visualize and identify outliers.

💡 For more KQL breakdowns, use cases, Sentinel & Log Analytics  
Cost Optimization exercises, check out my blog  
at www.devsecopsdad.com 💡  

👨‍💻 👩‍💻 For more useful queries you can copy n’ paste, visit my KQL  
repo at https://lnkd.in/e5e7z_aR follow me on Twitter @IanDHanley  
https://lnkd.in/e3x74inZ 😎  

⚔ \#microsoftsentinel ⚡\#azurecloud ☁ \#devsecops 🔐  
🔑 \#learningeveryday 📚 \#azuresecurity 🛡 \#cybersecuritytips💪  

=======================================

⚡ \#microsoftsentinel 🛡 Blog Update ⚡ Ever try to connect ARM based  
architecture to a Log Analytics Workspace?  

Use-Case: 👉 You’re a industrial manufacturing plant manager, you  
need to prototype, deploy, secure, and remotely manage connected  
electronic devices at scale. You need to be practical and most  
importantly, cost-effective.  

🔥 Thankfully, you’ve made good decisions up to this point and have  
invested in a SIEM such as Azure Sentinel (good job!). This means that  
most of your sensor and PLC equipment can connect through an API or is  
compatible with the Azure Monitoring Agent.  

🚨 What do you do for unsupported but critical IoT architecture  
❓❓❓ ❓  

💡 Answer: https://lnkd.in/enTNj9v3

In this post we will: ✅ - Call out and solve for use-case  
pre-requisites ✅ - Configure our ‘unsupported’ equipment accordingly  
(Ruby & FluentD) ✅ - Create a Log Analytics Workspace ✅ - Retrieve  
WorkspaceID and Primary Key ✅ - Program the config file for log  
aggregation (FluentD) ✅ - Log auth and syslog tables to a Log Analytics  
Workspace  

🛠 For additional use-cases and exercises, check out my blog at  
https://hanley.cloud  

👨‍💻 👩‍💻 For more useful queries you can copy n’ paste, visit my KQL  
repo at https://lnkd.in/e-3C8m-g or follow me on Twitter @IanDHanley  
https://lnkd.in/e3x74inZ  

🔒  
\#microsoftsecurity🛡 #microsoftsentinel⚔ \#devsecops🛠 \#cybersecuritytips💪 \#learn 📚 #cloudsecurity ☁ \#azure⚡  
\#internetofthings ⚙ \#raspberrypi 🥧  

=======================================