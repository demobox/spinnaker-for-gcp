# Install Spinnaker

## Select GCP project

Select the project in which you'll install Spinnaker, then click **Start**, below.

<walkthrough-project-billing-setup>
</walkthrough-project-billing-setup>

## Spinnaker Installation

Now let's provision Spinnaker within {{project-id}}.

Click the copy/paste button on the command below to copy that command to your shell,
then press **Enter** to run it from the Shell.

### Configure the environment.

```bash
PROJECT_ID={{project-id}} ~/spinnaker-for-gcp/scripts/install/setup_properties.sh
```

After that script finishes, you can use the command below to open the properties file for your Spinnaker
installation. This is optional.

```bash
cloudshell edit ~/spinnaker-for-gcp/scripts/install/properties
```

**Proceed with caution**. If you edit this file, the installation might not work
as expected.

### Begin the installation

**This will take some time**

```bash
~/spinnaker-for-gcp/scripts/install/setup.sh
```

Watch the Cloud Shell command line to see when it completes, then click
**Next** to continue to the next step.

## Connect to Spinnaker

You'll now run commands to...
* connect to Spinnaker 
* open the Spinnaker UI (Deck) in a browser window

You have two choices:
* forward port 8080 to tunnel to Spinnaker from your Cloud Shell
* expose Deck securely via a public IP

### Forward the port to Deck, and connect

Don't use the `hal deploy connect` command. Instead, use the following command
only.

```bash
~/spinnaker-for-gcp/scripts/manage/connect_unsecured.sh
```

To connect to the Deck UI, click the link below, which highlights the Preview
button above.

<walkthrough-spotlight-pointer
    spotlightId="devshell-web-preview-button"
    text="Connect to Spinnaker via 'Preview on port 8080'">
</walkthrough-spotlight-pointer>


### Expose Spinnaker publicly

If you would like to connect to Spinnaker without relying on port forwarding, we can
expose it via a secure domain behind the [Identity-Aware Proxy](https://cloud.google.com/iap/).

Note that this phase could take 30-60 minutes. **Spinnaker will be inaccessible during this time.**

```bash
~/spinnaker-for-gcp/scripts/expose/configure_endpoint.sh
```

### View Spinnaker Audit Log

View the who, what, when and where of your Spinnaker installation
[here](https://console.developers.google.com/logs/viewer?project={{project-id}}&resource=cloud_function&minLogLevel=200).

### View Spinnaker Container Logs

View the logging output of the individual components of your Spinnaker installation
[here](https://console.developers.google.com/logs/viewer?project={{project-id}}&resource=k8s_container%2Fnamespace_name%2Fspinnaker).

## Next steps: manage Spinnaker

Now that you've installed Spinnaker on Google Kubernetes Engine, and
accessed it via port forwarding or made it available over the public
internet, you'll use this same console to manage your Spinnaker instance.

You can open this console by navigating to the Kubernetes Application on the
[Applications](https://console.developers.google.com/kubernetes/application?project={{project-id}})
view. The application's *Next Steps* section contains the relevant links and
operator instructions.

You can...

* Use [Halyard](https://www.spinnaker.io/reference/halyard/) to further
configure Spinnaker
* Add provider accounts
* Upgrade Spinnaker
* Add more operators

To start managing Spinnaker:

```bash
~/spinnaker-for-gcp/scripts/manage/update_console.sh
```
