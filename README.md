# 🚚 uds-package-nexus
[![Latest Release](https://img.shields.io/github/v/release/defenseunicorns/uds-package-nexus)](https://github.com/defenseunicorns/uds-package-nexus/releases)
[![Build Status](https://img.shields.io/github/actions/workflow/status/defenseunicorns/uds-package-nexus/tag-and-release.yaml)](https://github.com/defenseunicorns/uds-package-nexus/actions/workflows/tag-and-release.yaml)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/defenseunicorns/uds-package-nexus/badge)](https://api.securityscorecards.dev/projects/github.com/defenseunicorns/uds-package-nexus)


UDS Nexus Zarf Package

## Flavors

| Flavor | Description | Example Creation |
| ------ | ----------- | ---------------- |
| upstream | Uses upstream images within the package. | `zarf package create . -f upstream` |
| registry1 | Uses images from registry1.dso.mil within the package. | `zarf package create . -f registry1` |

> [!IMPORTANT]
> **NOTE:** To create the registry1 flavor you will need to be logged into Iron Bank - you can find instructions on how to do this in the [Big Bang Zarf Tutorial](https://docs.zarf.dev/tutorials/6-big-bang/#setup).

## Releases

The released packages can be found in [ghcr](https://github.com/defenseunicorns/uds-package-nexus/pkgs/container/packages%2Fuds%2Fnexus).

## Deployment Prerequisites

#### Database

- A Postgres database is running on port `5432` and accessible to the cluster
- This database can be logged into via the username configured with `NEXUS_DB_USERNAME`. The default is `nexus`.
- This database instance has a psql database created matching the configuration of `NEXUS_DB_NAME`. The default is `nexusdb`.
- Configure the `NEXUS_DB_PASSWORD` to match your database.
- The database user has read/write access to the above mentioned database

## Pro License
- Provide your base64 encoded license file via the Zarf deploy time variable `NEXUS_LICENSE_KEY`.
- External DB configuration requires a valid Nexus license to use the external DB configuration. If a license is not provided Nexus will default to the OSS version and will use an internal H2 DB.
- SSO requires a valid Nexus License. With a valid license you can enable SSO via the Zarf deploy time variable `NEXUS_SSO_ENABLED`

## NEXUS_VM_PARAMS
- This package provides the same default as the upstream registry1 chart. You may need to update these to your needs.

`-Dcom.redhat.fips=false -Xms2703M -Xmx2703M -XX:MaxDirectMemorySize=2703M -XX:+UnlockExperimentalVMOptions -XX:+UseContainerSupport -Djava.util.prefs.userRoot=/nexus-data/javaprefs`

## Additional Notes
#### Access Control
- Information about configuring access controls and related topics such as realms, privileges, roles, default roles, ect can be found [here](https://help.sonatype.com/en/access-control.html#related-topics)

#### Disconnected Environments
- When deploying in a disconnected environment, you will want to disable the outreach management capability.
![outreach-settings](docs/images/outreach-management-settings.png)
