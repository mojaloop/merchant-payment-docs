# Frequently Asked Questions (FAQ) - Merchant Registry System

**Q: Is Merchant Registry a part of the switch?**

A: No, the Merchant Registry is not part of the switch. It is a value-added module that facilitates the merchant payment use case and acts as a central database system for merchants within the overall system.

**Q: What are the main functionalities of the Merchant Registry?**

A: The Merchant Registry in the acquiring system allows the acquiring process for each DFSP. It involves the collection of merchant information, approval of records by the maker, and the generation of aliases for merchants. These aliases, provided by the Merchant Registry module, enable merchants to seamlessly join the interoperable payment ecosystem.

**Q: Can DFSPs with existing merchant acquiring systems participate in the system?**

A: Yes, DFSPs with existing merchant acquiring systems can participate. They can submit merchant records to the system along with their existing aliases. The system will store the data, and if the provided alias already exists in the merchant registry, an error message will be generated.

**Q: Which QR standard is used in the QR code generation process?**

A: The EMV Co standard is used in the QR code generation process. Mandatory fields such as UUID, merchant ID, merchant alias, Merchant Doing Business As (DBA) name, and location are stored in the QR code.

**Q: Is there a specific format for the alias generated by the system?**

A: Yes, the alias is in a numeric format and is auto-generated by the database with an auto-incremental nature. Each alias is unique and sequentially generated by the system.