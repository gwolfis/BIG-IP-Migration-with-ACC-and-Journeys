# Module 1: BIG-IP bigip_base.conf migration with ACC

## BIG-IP Automation Configuration Converter (ACC)

F5 BIG-IP is using an object-based way of configuring the system and stores these configs into files like bigip_base.conf and bigip.conf.

F5 natively supports REST-API and there is a large library on [F5 Clouddocs](https://clouddocs.f5.com/): https://clouddocs.f5.com/api/icontrol-rest/.

This library can be used to support your automation journey but you will find out sooner or later that actually you are extending your GUI or CLI habits now into API. Configuring the F5 BIG-IP through an imperative way. Imperative automation let's itself describe as: *"telling the system **HOW** to do something every step of the way"*. This approach, though not wrong in itself, does not allow to use the system without the appropriate knowledge.

No one without expert knowledge of the system is able to get functions from a BIG-IP which can be leveraged to support applications and its related services.

We need the declarative approach to make something repeatable and more suitable to serve automation of BIG-IPs. Declarative automation drives *"Tell the system **WHAT** you want and let it figure out **HOW** to do it"*. This makes that only a REST-API request is needed to deploy desired app services functionality.

F5 has developed tools like [DO](https://clouddocs.f5.com/products/extensions/f5-declarative-onboarding/latest/), [AS3](https://clouddocs.f5.com/products/extensions/f5-declarative-onboarding/latest/), [FAST](https://clouddocs.f5.com/products/extensions/f5-appsvcs-templates/latest/) and [TS](https://clouddocs.f5.com/products/extensions/f5-telemetry-streaming/latest/) to support declarative automation and those can be used to create your own custom set of templates to deploy F5 BIG-IP application services.

For brownfield use cases F5 developed BIG-IP ACC where object-based configurations can be migrated into declarative templates.

# Tasks
During this module you will use a BIG-IP configuration from UCS and convert it into Declarative Onboarding (DO) and deploy it as a declaration into the BIG-IP.

## Task 1 - Convert bigip_base.conf

**Step 1:** In UDF, Go to the **Ubuntu Jumphost**, right-click **Access** and select **RDP**.

**Step 2:** Use login/password (ubuntu/journeys) to enter the jumphost and start **Visual Studio Code**. VSC can be found at the desktop.

VSC is loaded with two F5 extensions:
* F5 extension - Enables the use of declarative automation like DO, AS3, TS and FAST.
* F5 ACC Chariot - Extension which allows the conversion of  object-based BIG-IP configurations from .conf, UCS or Qkview into declarative DO or AS3.

**Step 3:** Use the F5 Extension to connect to the BIG-IP which we will configure using a UCS file. 

* Go to VSC, click the F5 icon and hover to **F5 Hosts** and select the popping up `+` sign to add a host.
* In the new field type: **admin@10.1.1.6** and hit **Enter**.
* Select the new F5 host and fill in the password in the popped up field (journeys2021).

The output field in the VSC terminal section shows that the BIG-IP gets connected.


**Step 5:** Scroll down in the BIG-IPS section to the **Config Explorer** and Import a TMOS config from UCS by clicking **Import .conf/UCS/QKVIEW from local file**.

**Step 6:** From the opened **Folder** (/Home/ubuntu), select folder **ucs** and select **20230221-archive.ucs** and click **Open**.

**Step 7:** In **Config Explorer** select **Sources** and click **config/bip_base.conf**. The file bigip_base.conf opens in VSC main window.

**Step 8:** Hover over the opened bigip_base.conf file and right-click and select **Convert to DO with ACC**.

```
Note: A pop-up window might appear called 'Unlock Login Keyring' and 'Authentication required' password = journeys
```

**Step 9:** Make the following changes to the Declarative Onboarding JSON schema.

|Object Name|Old value|New value|
|---------|---------|---------|
|Hostname |bigip-a.f5demo.local |bigip-2-demo.f5.com|
|Management IP (host address)| 172.16.1.90/24 | 10.1.1.6/24 |

Remove the SNMP part from the DO JSON schema.

**Step 10:** Save the DO declaration by pressing `Ctrl+s` and save the file as **do.json**.

**Step 11:** Right-click on do.json and select **Post as DO Declaration**. 

**Step 12:** Check the configuration in the BIG-IP via the GUI.

```
VSC will claim after while that Posting DO Declaration is still ongoing (HTTP 202) while the declaration has been POSTed. Please ignore the message.
```

# Summary
Using VSC and the additional F5 extensions we connected to a BIG-IP and used an offline stored UCS file to read the bigip_base.conf and modify it to a usable Declarative Onboarding json schema. This do.json has been deployed to configure the BIG-IP via a declarative REST-API request.