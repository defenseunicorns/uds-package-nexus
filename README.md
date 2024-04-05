# uds-package-nexus
UDS Nexus Zarf Package

# uds-capability-nexus
Bigbang [Nexus Repository Manager](https://repo1.dso.mil/big-bang/product/packages/nexus)

## Deployment Prerequisites

#### General

- Create `nexus` namespace
- Label `nexus` namespace with `istio-injection: enabled`

#### Database

- A Postgres database is running on port `5432` and accessible to the cluster
- This database can be logged into via the username configured with `NEXUS_DB_USERNAME`. The default is `nexus`.
- This database instance has a psql database created matching the configuration of `NEXUS_DB_NAME`. The default is `nexusdb`.
- Configure the `NEXUS_DB_PASSWORD` to match your database.
- The database user has read/write access to the above mentioned database

#### Pro License
- You must provide a valid Nexus license to use the external DB configuration. If a license is not provided Nexus will default to the OSS version and will use an internal H2 DB.
- Provide your license via the Zarf deploy time variable `NEXUS_LICENSE_KEY`.

#### NEXUS_VM_PARAMS
- This package provides the same default as the upstream registry1 chart. You may need to update these to your needs.

`-Dcom.redhat.fips=false -Xms2703M -Xmx2703M -XX:MaxDirectMemorySize=2703M -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -Djava.util.prefs.userRoot=/nexus-data/javaprefs`