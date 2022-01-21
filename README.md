This notebook is for configuration purposes: Mounting ADLS Storage to Databricks.
1- Steps to assign access of Databricks to ADLS Storage:
Go to Azure Active Directory and create app registrations and give appropriate name, in this case databricks-service-app
Go to databricks-service-app and copy Client ID, Tenant ID. Create new secret from certficates and secrets then copy the key.
Create four variables storage_account_name client_id tenant_id client_secret and fill them with appropriate values.
Follow config code shown in video or checkout https://docs.microsoft.com/en-us/azure/databricks/data/data-sources/azure/adls-gen2/azure-datalake-gen2-sp-access#—mount-adls-gen2-storage to copy the code
2- Steps to Secure the credentials (client-id,tenant-id,secret-id) instead of exposing it
Create resource Azure Key Vault and create the secrets databricks-app-client-id databricks-app-client-secret databricks-app-tenant-id.
Go to properties tab and copy Vault URI and Resource ID
Go to https://{databricks-instance}#secrets/createScope and create scope with name formula1-scope and paste the vault uri and resource id.
storage_account_name = "formula1dlnoconfuse"
client_id = dbutils.secrets.get(scope="formula1-scope",key="databricks-app-client-id")
tenant_id = dbutils.secrets.get(scope="formula1-scope",key="databricks-app-tenant-id")
client_secret = dbutils.secrets.get(scope="formula1-scope",key="databricks-app-client-secret")
Thanks for reading!
