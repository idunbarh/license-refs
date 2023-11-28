# License External Reference Example

This is an example of separating licensing information (licensee, license type,
expiration, etc ...) for an end user of COTS software from an immutable released SBOM.

The intent is per user licenses can be captured with the `acme_software-license.cdx.json`.
Each licensee would recent a unique `acme_software-license.cdx.json` with their license
information. `acme_software-1.0.0.tar.gz.cdx.json` is common among all consumers of a
products SBOM.

Both are CycloneDX.

## acme_software-license.cdx.json

This is the CycloneDX SBOM containing only the bare-minimum required fields to be
CycloneDX and include metadata licensing information that will be unique per
granted license for COTS software.

It leverages the `root` component with an `externalReference` of `bom` type to
reference the product's released immutable SBOM.

## acme_software-1.0.0.tar.gz.cdx.json

This the immutable SBOM released for each version of the a product.

## hopctl-merged.json

This is the "merged" SBOM from hoppr using the following command.

``` shell
hopctl merge --sbom-dir ./
```

This is what we would leverage internally for tracking and has several benefits:

- Producers "original" `acme_software-1.0.0.tar.gz.cdx.json` sbom would not be modified
- Traceability to the "original" `acme_software-1.0.0.tar.gz.cdx.json` would exist an `externalReference` of `bom` type in the merged sbom.
- The "original" `acme_software-1.0.0.tar.gz.cdx.json` can be immutable, and can be updated with new releases 
without modifying the `acme_software-license.cdx.json` assuming a consistent `bom-ref` is used.