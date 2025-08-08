# ACCESS-OM3

## About the model

ACCESS-OM3 is an ocean - sea ice (- wave) model under development. ACCESS-OM3 is built and deployed automatically to `gadi` on NCI (see below for details). In general, most users should start from one of the tested [configurations](https://github.com/accESS-NRI/access-om3-configs). 

For more information see the [ACCESS-Hive Docs model description](https://docs.access-hive.org.au/models/configurations/access-om/#access-om3) and [how to run the model](https://docs.access-hive.org.au/models/run-a-model/run-access-om3).

## About this repository

This is the Model Deployment Repository for the ACCESS-OM3 model. This repository contains a [spack environment](https://spack.readthedocs.io/en/latest/environments.html) manifest file ([`spack.yaml`](./spack.yaml)) that defines all the essential components of the model, including exact versions of the source code used.

## Releases

The software in this repository contributes to [access-om3 model configurations](https://github.com/accESS-NRI/access-om3-configs). Release information will be available on the [ACCESS Hive Forum](https://forum.access-hive.org.au/t/access-om3-release-information/4494) when supported releases are made.

## Support

[ACCESS-NRI](https://www.access-nri.org.au) supports ACCESS-OM3 for the Australian Research Community.

Any questions about ACCESS-NRI releases of ACCESS-OM3 should be done through the [ACCESS-Hive Forum](https://forum.access-hive.org.au/). See the [ACCESS Help and Support topic](https://forum.access-hive.org.au/t/access-help-and-support/908) for details on how to do this.

### Build

ACCESS-NRI is using [spack](https://spack.io), a build from source package manager designed for use with high performance computing.

Spack automatically builds all the components and their dependencies, producing model component executables. Spack already contains support for compiling thousands of common software packages. Spack packages for the components are defined in the [spack packages repository](https://github.com/ACCESS-NRI/spack_packages/).

ACCESS-OM3 is built and deployed automatically to `gadi` on NCI (see below). However it is possible to use spack to compile the model using the `spack.yaml` environment file in this repository. To do so follow the [instructions on for configuring spack on `gadi`](https://access-hive.org.au/getting_started/spack/).

Then clone this repository and run the following commands on `gadi`:

```bash
spack env create access-om3 spack.yaml
spack env activate access-om3
spack install
```

to create a spack environment called `access-om3` and build all the components, the locations of which can be found using `spack find --paths`.

### Deployment

ACCESS-OM3 is deployed automatically when a new version of the [`spack.yaml`](./spack.yaml) file is committed to `main` or a dedicated `backport/VERSION` branch. All the ACCESS-OM3 components are built using `spack` on `gadi` and installed under the [`vk83`](https://my.nci.org.au/mancini/project/vk83) project in `/g/data/vk83`. It is necessary to be a member of [`vk83`](https://my.nci.org.au/mancini/project/vk83) project to use ACCESS-NRI deployments of ACCESS-OM3.

The deployment process also creates a GitHub release with the same tag. All releases are available under the [Releases page](https://github.com/ACCESS-NRI/ACCESS-OM3/releases). Each release has a changelog and meta-data with detailed information about the build and deployment, including:

- paths on `gadi` to all executables built in the deployment process (`spack.location`)
- a `spack.lock` file, which is a complete build provenance document, listing all the components that were built and their dependencies, versions, compiler version, build flags and build architecture. It is also installable via spack similarly to the `spack.yaml`. 
- the environment `spack.yaml` file used for deployment

Additionally the deployment creates environment modulefiles, the [standard method for deploying software on `gadi`](https://opus.nci.org.au/display/Help/Environment+Modules). To view available ACCESS-OM3 versions:

```bash
module use /g/data/vk83/modules
module avail access-om3
```

For users of ACCESS-OM3 model configurations released by ACCESS-NRI, knowledge of the exact location of the model executables is not required. Model configurations will be updated with new model components when necessary.

For information on contributing your own fixes to the ACCESS-OM3 `spack.yaml`, see the [Hive Docs article](https://docs.access-hive.org.au/models/run-a-model/create-a-prerelease/) on creating a prerelease.
