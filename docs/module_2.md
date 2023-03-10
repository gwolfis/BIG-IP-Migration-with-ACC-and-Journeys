# Module 2: Use ACC to convert to AS3

In this module ACC will get used convert the app services configuration.

**Step 1:** In VSC, go to the **Config Explorer** and select **Partitions > Common**.

**Step 2:** Use the F5 Extension right-click options to convert from object-based config to AS3 json schema by selecting **Convert to AS3 with ACC**.

**Step 3:** Change the following object in the A3 declaration

| Object Name|Old Value|New Value|
|------------|---------|---------|
| Tenant Name| Common | https_app|


**Step 4:** Save the AS3 json schema by pressing `Ctrl+s` and name it **as3.json**. Place where to save it is a don't care.

**Step 5:** Use the 'mouse right-click' options to **POST** the AS3 declaration to the connected BIG-IP.

* Wait for the response you will receive in VSC.
* This reponse should be have an HTTP Code of 200 and a message of success.

**Step 6:** Use the GUI of the BIG-IP to check if the AS3 declaration has been deployed. (admin/journeys2021)

(Don't forget to change the parition in order to see the deployed VS , Pool and Pool members)

**Step 7:** Go to the Ubuntu Jumphost desktop and use the **F5 Demo App** to test the application.

# Summary
We used the same UCS file to grab the BIG-IP configuration stored in partition /Common and turned this is into an AS3 json schema.

ACC makes that migrations per-app can be deployed.

[PREVIOUS](../docs/module_1.md)      [NEXT](../docs/module_3.md)