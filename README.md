# my-test-service

## Vault Server Config
Once vault is installed and server is started (used dev server for this), do the following:

vault secrets disable secret/

vault secrets enable -path="secret" kv

vault auth enable approle

vault write auth/approle/role/my-test-service secret_id_ttl=60m token_num_uses=100 token_ttl=60m token_max_ttl=60m secret_id_num_uses=200

vault write -f auth/approle/role/my-test-service/secret-id

# Running the application
Add the following environment variables, with the respective values created in vault:
TEST_SERVICE_APPROLE
TEST_SERVICE_SECRET_ID

Run the application with:
mvn spring-boot:run

# Reproducing the issue
Remove lines 13 and 14 of bootstrap.yml and execute the application to reproduce the issue
