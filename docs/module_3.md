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

# Per-App Migration using Journeys App

In this lab, we are going to use Journeys App to migrate couple Virtual Servers from a BIG-IP 13.1 to a BIG-IP 16.1. 

**Step 1:** Navigate under the Ubuntu system and open the **Journeys App (Direct)**: ``https://10.1.1.7:8443/``.

**Step 2:** Start a new *Application Service Migration* Journeys.

**Step 3:** Acknowledge.

**Step 4:** Give it a name like **migration-to-16_1** and click Next.

**Step 5:** Select *Read the configuration from a live BIG-IP System* and enter BIG-IP 13.1 ip address and credentials (10.1.1.5, admin/journeys2021).

**Step 6:** You can look now at the merging preferences, you can keep the default. Click **Next**.

**Step 7:** You are now in the Application Inventory where you can rename tenants & apps, move virtual servers between apps, edit the virtual servers, look at the AS3 declaration for each app.

**Note**: A red tenant shows an object not supported by AS3 flagged by the tool. Journeys is using ACC in the backend to translate bigip.conf to AS3. See the [example of an issue](https://github.com/f5devcentral/f5-as3-config-converter/issues/60) filed against ACC for this error.

**Step 8:** Search for **10.1.10.15** Virtual IP Address using the search box.

**Step 9:** Rename **tenant_'x'** to `tenant_demo` by selecting the tenant and use the rename option and hit **Confirm**.

**Step 10:** Select **tenant_demo** and rename the **application_'x'** to `application_demo`.

**Step 11:** Select **application_demo** and edit both Virtual Servers and change destination IP from `10.1.10.15` to `10.1.10.17`, hit **save & Run Verification**, **exit** out, and change the next VS and when done **Close** the application and tenant windows and click **Next**.

**Step 12:** At **Deployment & Diagnostics** stage in **AS3 Tenants to Deploy** click **Add** and select **tenant_demo** and hit **Add**.

**Step 13:** Select **Edit** at **Diagnostics** and Go through the several options. Leave everything at its `Default` and hit **Apply**.

**Step 13:** Scroll down and generate the AS3 declaration, as well as the configuration files. Click **Deploy Now**.

**Step 14:** At the **Download** section and select **Generate Deployment files**. Download the AS3 file, store it in a local place and watch the AS3 template which we are about to declare.

**Step 15:** Finally hit **Deploy Now**.
**Step 16:** Enter the following:

* BIG-IP 16.1 ip address and credentials (10.1.1.6, admin/journeys2021)
* Select **Discover**
* BIG-IQ ip address and credentials (10.1.1.4, admin/journeys2021).
* Click **Deploy Now** and **Confirm**.

**Step 17:** Open BIG-IQ TMUI and navigate under the Application Tab under *Unknown Application* to see the app service deployed. You can also follow app deployment under the Application Deployment menu.

**Step 18:** Open BIG-IP 16.1 TMUI and change the partition to `tenant_demo` (top right corner) to see the Virtual Servers.

**Step 19:** Navigate under the Ubuntu system and open the F5 VSCode Extension at **Access** or use the **RDP** session if that one is still open.

**Step 20:** Open the F5 Extension and add the BIG-IP in the F5 host's section. When using the RDP session refresh `AS3 section` and check the deployed tenants.

**Step 21:** Once authenticated/Refreshed, you should see the `tenant_demo` AS3 tenant showing under the 10.1.1.6 target. From here, you can look at the app service configuration and make any edits/changes there using the F5 VSCode Extension.

[PREVIOUS](../docs/module_2.md)      [NEXT](../docs/module_4.md)