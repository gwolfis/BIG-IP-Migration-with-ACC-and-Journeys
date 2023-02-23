# Module 4: Lab Full Migration using Journeys App

In this lab, we are going to use Journeys App to migrate the entire BIG-IP configuration from the BIG-IP 13.1 to the BIG-IP 16.1.

1. Navigate under the Ubuntu system and open the Journeys App: ``https://10.1.1.7:8443/``
2. Start a new *Full Migration* Journeys
3. Acknowledge
4. Give it a name. Click Next.
5. Select *Read the configuration from a live BIG-IP System* and enter BIG-IP 13.1 ip address and credentials (10.1.1.5, admin/journeys2021)
6. Set the destination device  BIG-IP 15.1 ``10.1.1.8`` or BIG-IP 16.1 ``10.1.1.6`` (admin/journeys2021)
7. Go through System Compatibility
8. Verify & Edit Configuration (optional)

**Notes**: You may encounter warnings (e.g. ``/Common/serverssl, default option no-tlsv1.3 set``). Load validation can produce false positive output if the configuration contains any parts subject to fix-up scripts built into the BIG-IP ucs load process. These fix-ups cannot be automatically incorporated in the validation module. [More details](https://github.com/f5devcentral/f5-journeys#load-validation).

9. Deploy the modified UCS.

**Notes**:
- You can also use the UCS available in the ubuntu server under ``/home/ubuntu/ucs`` called ``full-migration-demo.ucs`` using the offline mode. This UCS contains all the known system compatibility issues with VELOS.
- There is a bash script available on the ubuntu server ``/home/ubuntu/demo-journeys-backup-restore.sh`` which can be used to demo backup/restore use case using Journeys App.
- **BIG-IP 12.1** is also available if you need to restore a custom BIG-IP configuration from your customer on it (follow instructions under **Lab 3: Restore a UCS ...**)
