# Module 3: Per-App migration BIG-IP with Journeys

**Project Journeys** is about re-imagining and enabling the next generation **upgrade and migration experience** @ F5.

This program leverages tools that sales, customers, partners and consultants can use and demo/learn using this blueprint:
- [F5 Journeys App](https://github.com/f5devcentral/f5-journeys) - watch [demo1](https://youtu.be/lLm5OkJRicw) & [demo2](https://youtu.be/sPVZymcciSo)
- [F5 Journeys Lab UCS Modifier](https://github.com/f5devcentral/f5-journeys-lab-ucs-modifier)

### List of Systems & Credentials in this lab
- **BIG-IQ**: 10.1.1.4
- **BIG-IP 12.1**: 10.1.1.9 (no config)
- **BIG-IP 13.1**: 10.1.1.5 
- **BIG-IP 15.1**: 10.1.1.8 (no config)
- **BIG-IP 16.1**: 10.1.1.6 (no config)
- **Ubuntu** hosting Journeys App, Journeys Lab UCS Modifier, F5 VS code Extension, Firefox, demo apps

**Credentials:** admin and root passwords for all F5 systems are `journeys2021

# Lab 1: Per-App Migration using Journeys App

In this lab, we are going to use Journeys App to migrate couple Virtual Servers from a BIG-IP 13.1 to a BIG-IP 16.1. 

1. Navigate under the Ubuntu system and open the Journeys App: ``https://10.1.1.7:8443/``
2. Start a new *Application Service Migration* Journeys
3. Acknowledge
4. Give it a name. Click Next.
5. Select *Read the configuration from a live BIG-IP System* and enter BIG-IP 13.1 ip address and credentials (10.1.1.5, admin/journeys2021)
6. You can look now at the merging preferences, you can keep the default. Click **Next**.

7. You are now in the Application Inventory where you can rename tenants & apps, move virtual servers between apps, edit the virtual servers, look at the AS3 declaration for each app.

**Note**: A red tenant shows an object not supported by AS3 flagged by the tool. Journeys is using ACC in the backend to translate bigip.conf to AS3. See the [example of an issue](https://github.com/f5devcentral/f5-as3-config-converter/issues/60) filed against ACC for this error.

8. Search for **10.1.10.15** Virtual IP Address using the search box. This should show `tenant_X` (or `dc1_qa_corp_int` if you used regular expression in step 6.
9. Rename `tenant_x` to `demo` and `application_x` to `myApp` (if you did not used regular expression). Edit both Virtual Servers and change destination IP from `10.1.10.15` to `10.1.10.17`, save it all, and Click **Next**.
10. From the deployment page, select the `demo` and add it to the tenant/app to deploy
11. Scroll down and generate the AS3 declaration, as well as the configuration files. Click **Deploy Now**.
12. Enter BIG-IP 16.1 ip address and credentials (10.1.1.6, admin/journeys2021), as well as BIG-IQ ip address and credentials (10.1.1.4, admin/journeys2021). Do not forget to click on **Discover**. Click **Deploy Now**.
13. Open BIG-IQ TMUI and navigate under the Application Tab under *Unknown Application* to see the app service deployed. You can also follow app deployment under the Application Deployment menu.
14. Open BIG-IP 16.1 TMUI and change the partition to `demo` (top right corner) to see the Virtual Servers
15. Navigate under the Ubuntu system and open the F5 VSCode Extension
16. Open the F5 Extension and add the BIG-IQ in the F5 host's section
17. Once authenticated, you should see the `demo` AS3 tenant showing under the 10.1.1.6 target. From here, you can look at the app service configuration and make any edits/changes there using the F5 VSCode Extension.

