# Contributing to OpenTelemetry Configuration

## Introduction

Welcome to the OpenTelemetry Configuration repository! 🎉

Thank you for considering contributing to this project. Whether you're fixing a bug, adding new features, improving documentation, or reporting an issue, we appreciate your help in making OpenTelemetry better. 

This repository is part of the OpenTelemetry ecosystem, which provides observability tooling for distributed systems. Your contributions help enhance the configuration schema for OpenTelemetry users worldwide.

If you have any questions, feel free to ask in the community channels. We’re happy to help! 😊


## Prerequisites

Before getting started, ensure you have the following installed:

- **Node.js (LTS version)** – [Install Node.js](https://nodejs.org/)
- **npm** (comes with Node.js)
- **Make** (for running development tasks)


## Local Run/Build

To set up and run the project locally, follow these steps:

### Installation
Clone the repository and install dependencies:
```bash
git clone https://github.com/open-telemetry/opentelemetry-configuration.git
cd opentelemetry-configuration
npm install
```

### Running the Build
To build the project, run:
```bash
make build
```

### Running Checks Locally
To ensure everything is set up correctly, run all validation checks:
```bash
make all
```

### Generating Descriptions
To automatically update configuration property descriptions:
```bash
make generate-descriptions
```
If any changes are detected that are not committed, the build will fail.

### Running Against a Single File
To generate descriptions for a specific YAML file:
```bash
npm run-script generate-descriptions -- /absolute/path/to/input/file.yaml /absolute/path/to/output/file.yaml
```
For debugging output:
```bash
npm run-script generate-descriptions -- /absolute/path/to/input/file.yaml /absolute/path/to/output/file.yaml --debug
```


## Pull Requests

A PR is ready to merge when:

- It has at least **1 approval** from codeowners (TODO: bump to 2 when we have more codeowners)
- There is no "request changes" from codeowners
- If a change to the schema, at least one example is updated to illustrate the change
- All required status checks pass
- The PR includes a CHANGELOG entry under **## UNRELEASED** following the form:
  ```markdown
  * {Brief description of change}
    ([#{PR Number}](https://github.com/open-telemetry/opentelemetry-configuration/pull/{PR Number}))
  ```

## Aditional Information

### Description generation

The [./examples](./examples) directory contains a variety of examples, which
include important comments describing the semantics of the configuration
properties. In order to keep these comments consistent across examples, we have
tooling which automatically generates comments for each property.

How it works:

* The [./schema/type_descriptions.yaml](./schema/type_descriptions.yaml) file
  defines descriptions for each of the properties of each type defines in
  the [JSON schema](./schema) data model.
* The [./scripts/generate-descriptions.js](./scripts/generate-comments.js) is a
  script which for a given input configuration file will:
  * Parse the YAML.
  * Walk through each key / value pair, and for each:
    * Compute the JSON dot notation location of the current key / value pair.
    * Find the first matching rule
      in [type_description.yaml](./schema/type_descriptions.yaml). Iterate
      through the rules and evaluate the key / value pair dot notation location
      against each of the rule's `path_patterns`.
    * Inject / overwrite comments for its properties according
      to `type_descriptions.yaml`.
  * Write the resulting content to specified output file or to the console.

The `make generate-descriptions` command runs this process against each file
in `./examples` and overwrites each file in the process. 

**NOTE:** The [build](./.github/workflows/build-check.yaml) will fail
if `make generate-descriptions` produces any changes which are not checked into
version control.

## Further Help

Need help? Join our community:

- **Slack**: [OpenTelemetry Slack](https://opentelemetry.io/community/)
- **GitHub Discussions**: [OpenTelemetry Discussions](https://github.com/open-telemetry/opentelemetry-configuration/discussions)
- **Issues**: If you encounter a bug, [open an issue](https://github.com/open-telemetry/opentelemetry-configuration/issues)

Thank you for contributing! 🚀
