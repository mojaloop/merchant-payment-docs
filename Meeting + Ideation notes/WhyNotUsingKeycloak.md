## Why Not Use Keycloak?

### Complexity

- Keycloak can be complex to set up and manage.
- Keycloak offers a wide range of features, including Single Sign-On
  (SSO), identity brokering, and social login, which can make the initial
  setup overwhelming.
- The vast array of configuration options can be confusing.
- Managing specific DFSP users can be complex.
- Setting up a highly available and scalable environment involves
  additional complexity such as clustering, load balancing, and database
  setup.
- Keycloak produces extensive logs, but interpreting them can be
  non-trivial. Additionally, setting up monitoring and alerting requires
  additional effort.
- Incorrect configurations can lead to security vulnerabilities. A deep
  understanding of OAuth2, SAML, and other authentication and
  authorization protocols is needed to secure the environment properly.

### Overhead

- Deploying and maintaining a separate Keycloak server may introduce additional overhead, both in terms of resources and management.

### Learning Curve

- Keycloak has its own set of configurations, APIs, and terminology that need to learn.
- Need to use Two separate Libraries. [keycloak-js](https://www.npmjs.com/package/keycloak-js) for Authentication/Authorization Acccess and [keycloak-admin-client](https://www.npmjs.com/package/@keycloak/keycloak-admin-client) for Managing Accounts/Roles/Permissions via Backend.

### Vendor Lock-in

- While Keycloak is open-source, adopting it may make it harder to switch to a different identity provider in the future due to API and configuration specifics.

### Customization Limitations

- Although Keycloak is highly customizable, its customization might not be straightforward and may require diving deep into its documentation.

### Resource Usage

- Keycloak can be resource-intensive, which might be an issue for small or resource-constrained environments.

### Community and Support

- While Keycloak has a strong community and extensive documentation, commercial support might be expensive.
