# **External DFSP alias generation:**

**As an external DFSP which doesn't use merchant acquiing system**, **I want to** add new alias records and map them to the merchant registry so that merchant that our organization acquired can start using the payment interoperablity.

**Acceptance Criteria:**

**Onboarding DFSP:**  

- The system should allow hub users to onboard a DFSP by providing necessary information, including DFSP ID,DFSP name.
- After onboarding, the system on behalf of hub user who onboarded the DFSP should generate a client secret key for authentication.

**Adding New Merchant Alias Records:**

- External DFSP users must include the client secret key in the API request headers for authentication.
- External DFSP users can add new merchant alias records through an API.
- The request body should include the following information:
  - Merchant ID: A unique identifier for the merchant from their existing system.
  - Currency: The currency associated with the merchant.
  - Alias (optional): If an alias is provided, it will be associated with the merchant in the registry.

**Alias Generation:**

- If the alias is not provided in the request, the system should generate a unique alias and associate it with the merchant in the registry.
- If the alias is provided and it already exists in the registry, the system should return a response with a failed status and an error code of "alias already existed."

**Multiple Merchant Records in a Single Request:**

- External DFSP users should be able to pass multiple merchant records in a single API request, allowing for batch processing.

**Audit Logging:**

- The system should record every transaction related to alias recording in an audit log.
- The audit log should include information about who sent the request and which alias ID was recorded.

**Security:**

- The client secret key should be securely stored and used for authentication.
