The ngrok SSO Integration allows Auth0 to act as the identity provider for your ngrok-frontended application.

## Prerequisites

1. An Auth0 account and tenant. [Sign up for free](https://auth0.com/signup).
2. An ngrok enterprise account with admin access to configure edges with SAML SSO.


## Configure the Auth0 SSO Integration

1. Select **Add Integration** (at the top of this page).

1. Read the necessary access requirements, and select **Continue**.

1. Enter a **Name**, then configure the integration using the following fields:
   * **Callback URL**: Enter a temporary value `https://temporary` (later you replace this value with the **ACS URL** URL of the SAML route).
   * **Audience**: Enter a temporary value `https://temporary` (later you replace this value with the **Entity ID** URL of the SAML route).
1. Click **Save** to enable the SSO integration.

1. In the **Tutorial** view, open the **Identity Provider Metadata** URL in a new browser tab and download the metadata xml file.

1. Select the **Connections** view and [configure the sources of identity to use](https://auth0.com/docs/get-started/applications/update-application-connections).

## Set up ngrok

To configure the integration with **ngrok**, follow the steps below with the data shown in the **Tutorial** view (which will appear when you save the initial configuration settings).

1. Log into **ngrok** using your ngrok account.

1. Click **Cloud Edge** > **Edges** and create a new HTTPS edge.

1. Provide a **Description** for the edge, click **SAML** on the left panel of the **Routes** section, and then click **Begin setup**.

1. Click **Upload XML**, open the **Identity Provider Metadata** xml file you downloaded from **Auth0**, and then click **Save**.

1. Copy both the **ACS URL** and the **Entity ID** URls and update the **Settings** view of the ngrok SSO configuration in **Auth0**.

1. Click **Start a tunnel** and follow the instructions to run ngrok in a terminal.

1. Open the **Endpoints** URL of the ngrok edge (You use this URL to test the Auth0 Authentication).

## Troubleshooting

[[TODO: Common issues or links to troubleshooting resources]]
