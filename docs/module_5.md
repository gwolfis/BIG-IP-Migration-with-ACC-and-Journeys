# Module 5: Restore a UCS on a BIG-IP using F5 Journeys Lab UCS Modifier

In this lab, we are going to use Journeys Lab UCS Modifier to restore a UCS on a BIG-IP 13.1, then upgrade it to 16.1 (in-place upgrade).

**Note:** In this lab, we are using a lab UCS for the demo but you could get a UCS from your customer and restore it on one of the BIG-IP available in this blueprint. Just make sure the BIG-IP you use to restore the UCS has the same version as the UCS. You could use the Journeys-App to upload the UCS from your laptop into the Ubuntu system under ``/tmp/journeys/<session name>``.

1. SSH to the BIG-IP 13.1 and [restore the BIG-IP configuration to factory default settings](https://support.f5.com/csp/article/K13127):
```
tmsh load /sys config default
reboot
```

2. Wait for the prompt to show *[root@localhost:Active:Standalone] config #*. Then, log in on the BIG-IP with TMUI with admin/admin and confirm the system was reset correctly.
You may need to run the ``tmsh load /sys config default`` command another time after the reboot is the system show errors loading certificates.

**Note:** Don't worry, we saved a UCS backup which is stored on the Ubuntu system. The goal is to start with a fresh box where we will use the tool to restore the UCS, then upgrade to a specific BIG-IP version to validate the upgrade.

3. SSH into the Ubuntu server.
4. Use the Journeys Lab UCS Modifier to sanitize the source UCS so that it can be loaded into a different target BIG-IP. 
```
cd  /home/ubuntu/ucs
docker run -t -i -v /home/ubuntu/ucs:/modifier/ucs f5devcentral/f5-journeyslab-ucsmodifier:latest
ucs-modifier -h
ucs-modifier -u /modifier/ucs/lab-bigip-restore-demo.ucs -m 10.1.1.5 -p default -o /modifier/ucs/lab-bigip-restore-demo_modified.ucs -d
exit
```
&nbsp;

5. Transfer the UCS modified on the BIG-IP 13.1 (password is **default**)
```
scp -c aes128-cbc lab-bigip-restore-demo_modified.ucs root@10.1.1.5:/tmp
```
&nbsp;

6. Move the modified UCS under /var/local/ucs.
```
mv /tmp/lab-bigip-restore-demo_modified.ucs /var/local/ucs
tar -ztf /var/local/ucs/lab-bigip-restore-demo_modified.ucs | tail -5
```
&nbsp;

7. Backup the BIG-IP
```
tmsh save sys ucs $(echo $HOSTNAME | cut -d'.' -f1)-$(date +%H%M-%m%d%y)
ls -lrt /var/local/ucs
```
&nbsp;

8. Restore the UCS on the target BIG-IP with the same version (when possible). Make sure you set the admin/root passwords once the UCS has been restored successfully.
```
tmsh load sys ucs lab-bigip-restore-demo_modified.ucs no-license keep-current-management-ip reset-trust platform-migrate
tmsh modify /auth user admin password journeys2021
tmsh save /sys config partitions all
echo "root:journeys2021" | chpasswd
reboot
```
&nbsp;
Note: if the tmsh load sys ucs fails, look for the error message and manually edit the bigip.conf file to mitigate the issue.

If you are restoring another UCS containing cluster information, you may need to run those additional steps to complete the UCS restore:
```
tmsh delete /cm trust-domain Root
tmsh modify auth user admin shell bash
tmsh save sys config
bigstart restart devmgmtd
```
&nbsp;

9. Log in on the BIG-IP with TMUI and confirm the system was restored correctly.

10. Upgrade BIG-IP 13.1 to 15.1 (download the image on [downloads.f5.com](https://downloads.f5.com) also see [K13845](https://support.f5.com/csp/article/K13845)).

**Option 1 - Use BIG-IQ to upgrade BIG-IP**: Follow instructions on this [KB Article](https://support.f5.com/csp/article/K14812626)

**Option 2 - Upgrade BIG-IP locally**: Follow instructions on this [KB Article](https://support.f5.com/csp/article/K51113020)

11. Perform necessary sanity checks as needed.

# Resources

## F5 Journeys App
Instructions on how to install and use Journeys App on [GitHub](https://github.com/f5devcentral/f5-journeys).
The Journeys App is already installed on the Ubuntu server in the blueprint.

There is also a swagger available on the Ubuntu server which lets you browse the Journeys API. 
You can use VS code available also on the Ubuntu server to try those out, open `journeys-api.http` in VS code and see a few examples using the VS code REST API client.

## F5 Journeys Lab UCS Modifier 
Learn more about [GitHub](https://github.com/f5devcentral/f5-journeys-lab-ucs-modifier).
The Journeys App is already installed on the Ubuntu server in the blueprint.

## F5 VSCode Extension
Learn more about F5 VSCode Extension on [GitHub](https://f5devcentral.github.io/vscode-f5/#/).
Visual Studio Code, as well as the Extension, are already installed on the Ubuntu server in the blueprint (password is `journeys`).