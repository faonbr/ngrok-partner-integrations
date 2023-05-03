The ngrok SSO Integration allows Auth0 to act as the identity provider for your ngrok-frontended application.

## Prerequisites

1. An ngrok enterprise account with admin access to configure a cloud edge with a SAML route.
1. Set up a Connection, which is a source of users. Connections can be databases, social identity providers, or enterprise identity providers, and can be shared among different applications. You may set up more than one connection for use with SSO integrations.


## Configure Auth0 SSO Integration

1. Select **Add Integration**, select your **Tenant** and select **Continue**.

1. Enter a **Name**, then configure the integration using the following fields:
   * **Callback URL**: Enter a temporary value `https://temporary` (later you replace this value with the **ACS URL** URL of the ngrok's SAML route).
   * **Audience**: Enter a temporary value `https://temporary` (later you replace this value with the **Entity ID** URL of the ngrok's SAML route).
1. Select **Save** to enable the SSO integration.

1. In the **Tutorial** view, open the **Identity Provider Metadata** URL in a new browser tab and download the metadata xml file.

1. Select the **Connections** view and [configure the sources of identity to use](https://auth0.com/docs/get-started/applications/update-application-connections).


## Set up ngrok

To configure the integration with **ngrok**, follow the steps below with the data shown in the **Tutorial** view (which will appear when you save the initial configuration settings).

1. Log into [ngrok dashboard](https://dashboard.ngrok.com/) using your ngrok account.

1. Select **Cloud Edge** > **Edges** and create a new HTTPS edge.

1. Provide a **Description** for the edge, select **SAML** on the left panel of the **Routes** section, and then select **Begin setup**.

1. Select **Upload XML**, open the **Identity Provider Metadata** xml file you downloaded from **Auth0**, and then select **Save**.

1. Copy both the **ACS URL** and the **Entity ID** URls and update the **Settings** view of the ngrok SSO configuration in **Auth0**.

1. Select **Start a tunnel** and follow the instructions to run ngrok in a terminal.

1. Open the **Endpoints** URL of the ngrok edge in a new browser tab (You use this URL to test the Auth0 authentication).


## Troubleshooting

* **ERR_NGROK_6528**: Verify that you started the ngrok tunnel of your cloud edge.
   **Fix**: In your edge configuration, select **Start a tunnel** and follow the instructions to run ngrok in a terminal.

* **HTTP ERROR 404**: Verify that the port number in the ngrok start-tunnel command is the same your app uses and the host points to the correct server of your app.
   **Fix**: Update the ngrok command with the correct host and port.

* **Wrong email or password** in Auth0's login page: Verify that the user is registered in Auth0.
   **Fix**: In the **Auth0 dashboard**, select **User Management** > **Users** and create a new user and verify how to [configure the sources of identity to use](https://auth0.com/docs/get-started/applications/update-application-connections) in your SSO integration.