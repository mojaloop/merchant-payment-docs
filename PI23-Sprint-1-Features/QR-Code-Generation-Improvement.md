# Acceptance Criteria for QR code generation

- QR code generation must comply with the EMV Co QR standard.

**For DFSPs using Acquiring System:**

- QR codes must include the following mandatory tags:
  - Merchant Category Code (ID "52")
  - Country Code (ID "58")
  - Merchant DBA Name (ID "59")
  - Merchant City (ID "60")
  - Merchant alias (ID "28" Sub Tag ID "01")

**For DFSPs not using Acquiring System:**

- Support for DFSPs without acquiring systems is essential.
- In addition to existing mandatory fields(merchant ID,DFSP ID, alias), the system must request the following additional mandatory fields:
  - Merchant Category Code (ID "52")
  - Country Code (ID "58")
  - Merchant DBA Name (ID "59")
  - Merchant City (ID "60")
  - Merchant alias (ID "28" Sub Tag ID "01")
- Only alias and DFSP mapping should be stored in the merchant registry.
- All attributes, including additional ones, should be stored in the acquiring system.
- By storing those additional mandatory fields, system will fully adhere the EMV CO standard and also support for future scenarios such as merchant self-registration, external DFSPs using the Merchant Portal, and merchant DFSP changes is necessary.