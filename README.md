# Workshop - Migrating BIG-IP with ACC and Journeys

## Introduction
F5 BIG-IP has been around for a very long time and used throughout numberous use cases to support applications staying healthy and enforcing the security of that application as well as securing the communcation between the user and the application.

There always comes a point in time where you need to switch gears and your IT needs migration in order to stay in the game.

'Modern' reasons to migrate your BIG-IP are:

* Software only approach makes that all hardware needs to be turned into software and F5 provides BIG-IP Virtual Edition (VE).

* IT has become a business enabler and use of multi-cloud, micro-services and APIs make that automation becomes essential. This requires moving from imperative (AKA object-based) into decalarative (AKA template-based) configurations.

* Your BIG-IP real-estate needs a tech-refresh and migration will take place from iSeries/Viprion to the new F5 BIG-IP platforms VELOS/Rseries.

Looking at the several reasons it becomes clear that each reason must have its own approach defined. Hence, there is nothing more personal then a migration.

## Workshop
F5 has developed a two tools to support migration use cases like the ones previously mentioned:

* **BIG-IP Automation Config Converter (ACC)**: 
BIG-IP ACC converts configuration files to either an F5 BIG-IP Application Services 3 Extension (BIG-IP AS3)
or an F5 BIG-IP Declarative Onboarding (BIG-IP DO) declaration.

* **F5 Journeys**: JOURNEYS is an application designed to assist F5 Customers with migrating a BIG-IP configuration to a new F5 device and enable new ways of migrating.

During this workshop you will learn:

* How to use BIG-IP ACC to convert BIG-IP configs.
* How to leverage F5 Journeys in your migration approaches.
* Ability to choose which tool suits best for the purpose.

## Lab environment
This workshop makes use of the UDF lab **Journeys Procut Team Demo/Lab**. When you want to follow this workshop without having access to UDF you need these minimum ste of requirements:

* A deployed F5 BIG-IP (can be either hardware or software) and ideally two to migrate from one to another.
* A host from where you are able to log into the BIG-IP.
* This host should have VSC installed with the F5 extension, F5 Journeys.

## Sources
* F5 BIG-IP Automation Config Converter (BIG-IP ACC): https://clouddocs.f5.com/products/extensions/f5-automation-config-converter/latest/

* F5 Journeys: https://github.com/f5devcentral/f5-journeys

**********************************
## Table of Contents
**********************************

**[Module 1: BIG-IP bigip_base.conf migration with ACC](docs/module_1.md)**

**[Module 2: Use ACC to convert to AS3](docs/module_2.md)**

**[Module 3: Per-App migration BIG-IP with Journeys](docs/module_3.md)**

**[Module 4: Lab Full Migration using Journeys App](docs/module_4.md)**

**[Module 5: Restore a UCS on a BIG-IP using F5 Journeys Lab UCS Modifier](docs/module_5.md)**

