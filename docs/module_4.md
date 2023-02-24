# Module 4: Full Migration using Journeys App

In this lab, we are going to use Journeys App to migrate the entire BIG-IP configuration from the BIG-IP 13.1 to the BIG-IP 16.1.

**Step 1:** Navigate under the Ubuntu system and open the **Journeys App (Direct)**.

**Step 2:** Start a new *Full Migration* Journeys.

**Step 3:** Read through the Journey supported migration gaps and once done hit **Acknowledge**.

**Step 4:** Give it a name like **full-migration-to-16_1**. Click **Next**.

**Step 5:** Select *Read the configuration from a live BIG-IP System* and enter BIG-IP 13.1 ip address and credentials (10.1.1.5, admin/journeys2021) and click **Discover**.

**Step 6:** Select **Load Configuration** and once loaded **Confirm** and hit **Next**.

**Step 7:** Set the destination device  BIG-IP 15.1 ``10.1.1.8`` or BIG-IP 16.1 ``10.1.1.6`` (admin/journeys2021), click **Discover** and go **Next**.

**Step 8:** Go through **System Compatibility** and click **Next**.

**Step 9:** Verify & Edit Configuration (optional). This operation can take up to 15 minutes.

```
Notes: You may encounter warnings (e.g. ``/Common/serverssl, default option no-tlsv1.3 set``). Load validation can produce false positive output if the configuration contains any parts subject to fix-up scripts built into the BIG-IP ucs load process. These fix-ups cannot be automatically incorporated in the validation module. [More details](https://github.com/f5devcentral/f5-journeys#load-validation).
```

**Step 10:** Deploy the modified UCS by selecting **Next** and **Deploy Now**.

**Step 11:** Fill in the BIG-IP creds for source and destination and don't forget to use **Discover**, keep the **Crearte backup UCS** option and once again select **Deploy Now**.

**Notes**:
- You can also use the UCS available in the ubuntu server under ``/home/ubuntu/ucs`` called ``full-migration-demo.ucs`` using the offline mode. This UCS contains all the known system compatibility issues with VELOS.
- There is a bash script available on the ubuntu server ``/home/ubuntu/demo-journeys-backup-restore.sh`` which can be used to demo backup/restore use case using Journeys App.
- **BIG-IP 12.1** is also available if you need to restore a custom BIG-IP configuration from your customer on it (follow instructions under **Module 5: Restore a UCS ...**)

[PREVIOUS](../docs/module_3.md)      [NEXT](../docs/module_5.md)