# Mastercard OpenBanking Connect - Backbase POC

In this repository we are implementing the [Mastercard OpenBanking Connect](https://developer.mastercard.com/open-banking-connect/documentation/) APIs to provide OIDC authentication and implementing Backbase contracts to serve account and payments services.

The custom implement components are:
- [OAuth2/OIDC Authorization Server](https://github.com/Backbase/authorization-server)
- [Mastercard Integration Service](https://github.com/Backbase/mastercard-integration-service)

These components are configured to run in a preset [Backbase environment](backbase-environment) that is available to be executed using docker compose, instructions are detailed in there.

## License

This is a proof-of-concept implementation for integration purposes. Do not use it in production.