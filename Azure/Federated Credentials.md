Federated Login allows us to use service principal to authenticate to Azure without the requirement for client secret. This works in the use case to deploy Azure Resource using GitHub Actions.

Ref: [MS Docs](https://learn.microsoft.com/en-us/azure/developer/github/connect-from-azure?tabs=azure-portal%2Cwindows#create-an-azure-active-directory-application-and-service-principal)

## Azure Portal

1.  Go to **App registrations** in the [Azure portal](https://portal.azure.com/) and open the app you want to configure.
2.  Within the app, go to **Certificates and secrets**.  
    ![Select Certificates & secrets.](https://learn.microsoft.com/en-us/azure/developer/github/media/federated-certificates-secrets.png)
3.  In the **Federated credentials** tab, select **Add credential**. ![Add the federated credential](https://learn.microsoft.com/en-us/azure/developer/github/media/add-federated-credential.png)
4.  Select the credential scenario **GitHub Actions deploying Azure resources**. Generate your credential by entering your credential details.

## Azure CLI

```shell
az rest --method POST --uri 'https://graph.microsoft.com/beta/applications/<APPLICATION-OBJECT-ID>/federatedIdentityCredentials' --body '{"name":"<CREDENTIAL-NAME>","issuer":"https://token.actions.githubusercontent.com","subject":"repo:organization/repository:environment:Production","description":"Testing","audiences":["api://AzureADTokenExchange"]}'
```

-   Replace `APPLICATION-OBJECT-ID` with the **objectId (generated while creating app)** for your Azure Active Directory application.
-   Set a value for `CREDENTIAL-NAME` to reference later.
-   Set the `subject`. The value of this is defined by GitHub depending on your workflow:
    -   Jobs in your GitHub Actions environment: `repo:< Organization/Repository >:environment:< Name >`
    -   For Jobs not tied to an environment, include the ref path for branch/tag based on the ref path used for triggering the workflow: `repo:< Organization/Repository >:ref:< ref path>`. For example, `repo:n-username/ node_express:ref:refs/heads/my-branch` or `repo:n-username/ node_express:ref:refs/tags/my-tag`.
    -   For workflows triggered by a pull request event: `repo:< Organization/Repository >:pull_request`.