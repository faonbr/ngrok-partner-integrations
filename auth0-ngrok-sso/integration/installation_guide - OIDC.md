The ngrok SSO Integration allows Auth0 to be the identity provider for your application with no code changes.

## What is ngrok?

ngrok is the fastest way to provide connectivity, security, and observability to your production applications. ngrok's ingress-as-a-service platform adds secure SAML authentication to any application without any code changes allowing you to focus on delivering value to your users.

## Prerequisites

1. An ngrok account.
1. Set up a Connection, which is a source of users. Connections can be databases, social identity providers, or enterprise identity providers, and can be shared among different applications. You may set up more than one connection for use with SSO integrations.


## Configure Auth0 SSO Integration

Inside your Auth0 account:

1. On the left menu, select **Applications**, select **Applications**, and then select **Create Application**.

1. On the **Create application** popup, enter `ngrok oidc` in the **name** field, select the **Single Page Web Applications** tile, and then select **Create**.

1. On the **ngrok oidc** page, select the **Settings** view and make note of the **Domain**, **Client ID**, and **Client Secret** values.

1. Enter `https://idp.ngrok.com/oauth2/callback` in the **Allowed Callback URLs** field, and enter the URL provided by the ngrok agent to expose your application to the internet in the **Application Login URI** field (i.e. `https://myexample.ngrok.dev`).

1. select **Save Changes**.

Assign Auth0 groups to the ngrok app:

1. On the **Dashboard**, select **User Management** on the left menu, select **Users**, and then select **Create User**.

1. Enter an email address in the **Email** field, provide a **Password**, and then select **Create**.


## Set up ngrok

ngrok can leverage Auth0 SSO in two ways:

- From the ngrok CLI (using the `--oidc` parameter)
- From the ngrok dashboard

### **Option 1**: ngrok CLI

> **Note:** For this tutorial, we assume you have an app running locally (i.e., on localhost:3000) with the ngrok client installed.

1. Launch a terminal

1. Enter the following command to launch an ngrok tunnel with Auth0 SSO:
    ```bash
    ngrok http 3000 --oidc=AUTH0_OAUTH_URL \
    --oidc-client-id=Auth0_CLIENT_ID \
    --oidc-client-secret=Auth0_CLIENT_SECRET \
    ```
    **Note**: Replace the following with values:
    - Auth0_OAUTH_URL: The domain value you copied from Auth0, in the form of an URL (i.e. `https://dev-abcd1234.us.auth0.com/`).
    - Auth0_CLIENT_ID: The client id you copied from Auth0.
    - Auth0_CLIENT_SECRET: The client secret you copied from Auth0.
    
    Alternatively, add the `--domain YOUR_DOMAIN` argument to get your custom URL, replacing `YOUR_DOMAIN` with your URL of preference.

1. Copy the URL available next to **Forwarding** (for example, `https://Auth0-sso-test.ngrok.dev`).

1. Skip to **Step 3**

### **Option 2**: ngrok Edge

To configure an edge with Auth0:

1. Access the [ngrok Dashboard](https://dashboard.ngrok.com/) and sign in using your ngrok account.

1. On the left menu, select **Cloud Edge** and then select **Edges**.

1. If you don't have an edge already set to add Auth0 SSO, create a test edge:
    * Select **+ New Edge**.
    * Select **Create HTTPS Edge**.
    * Select the **pencil icon** next to "no description", enter `Edge with Auth0 SSO OIDC` as the edge name, and select **Save**.

1. On the edge settings menu, select **OIDC**.

1. Select **Begin setup** and enter the following values into the fields:
    ![Auth0 config in ngrok](img/auth0-1.png)

    * **Issuer URL**: The domain value you copied from Auth0, in the form of a URL (i.e. `https://dev-abcd1234.us.auth0.com/`).
    * **Client ID**:  The client id you copied from Auth0.
    * **Client Secret**: The client secret you copied from Auth0.

1. Select **Save** at the top, and then select the left arrow to go back to the **Edges** page.

1. Launch a tunnel connected to your Auth0 edge:

    :::tip Note 
    For this step, we assume you have an app running locally (i.e. on localhost:3000) with the ngrok client installed.
    :::

    1. Select **Start a tunnel**.

    1. Select the **copy icon** next to the tunnel command.

    1. Launch a tunnel:
        * Launch a terminal.
        * Paste the command but replace `http://localhost:80` with your localhost app address (i.e., `http://localhost:3000`).
        * Select **Enter** and an ngrok tunnel associated with your edge configuration will launch.

    1. To confirm that the tunnel is connected to your edge:
        * Return to the ngrok dashboard
        * Close the **Start a tunnel** and the **Tunnel group** tabs
        * Refresh the test edge page. Under traffic, you will see the message _You have 1 tunnel online. Start additional tunnels to begin load balancing._

1. In the test edge, copy the **endpoint URL** and use this URL to test the Auth0 Authentication by pasting into another browser tab.

## Troubleshooting

* **ERR_NGROK_6528**: Verify that you started the ngrok tunnel of your cloud edge.
   **Fix**: In your edge configuration, select **Start a tunnel** and follow the instructions to run ngrok in a terminal.

* **HTTP ERROR 404**: Verify that the port number in the ngrok start-tunnel command is the same your app uses and the host points to the correct server of your app.
   **Fix**: Update the ngrok command with the correct host and port.

* **Wrong email or password** in Auth0's login page: Verify that the user is registered in Auth0.
   **Fix**: In the **Auth0 dashboard**, select **User Management** > **Users** and create a new user and verify how to [configure the sources of identity to use](https://auth0.com/docs/get-started/applications/update-application-connections) in your SSO integration.
   
* If you are still having trouble configuring this integration, please reach out to [ngrok Support](mailto:support@ngrok.com).
