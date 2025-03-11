# JFrog CLI Troubleshooting Guide for Curation Audit on Yarn Projects

This repository contains a sample yarn project that demonstrates issues we're experiencing with the JFrog CLI tool when working with yarn-based projects.

## Prerequisites

- macOS (this guide uses Homebrew for installation)
- Node.js and yarn installed
- Homebrew installed

## Installing JFrog CLI

1. Open your terminal and run the following command to install JFrog CLI using Homebrew:

```bash
brew install jfrog-cli
```

2. Verify the installation by checking the version:

```bash
jfrog -v
```

The most recent version of the JFrog CLI is 2.74.0. which will be shown in the output:

```
jf version 2.74.0
```

## Project Setup

1. Clone this repository:

```bash
git clone https://github.com/danfrenette-procore/jfrog-cli-testing
cd jfrog-cli-testing
```

2. Install yarn dependencies:

```bash
yarn install
```

## Reproducing the Issue

The issue occurs when trying to use JFrog CLI with yarn projects. To reproduce:

1. Configure JFrog CLI to use your Artifactory instance:

Follow the prompts to configure your JFrog platform instance.

2. Attempt to run curation with the JFrog CLI:

Use debug mode to gather more information about the issue.

```bash
export JFROG_CLI_LOG_LEVEL=DEBUG
jf ca
```

3. Observe the error:

```
11:05:09 [Debug] JFrog CLI version: 2.74.0
11:05:09 [Debug] OS/Arch: darwin/arm64
11:05:09 [Debug] Trace ID for JFrog Platform logs: 688b8649fc23f3d2
11:05:09 [Debug] Using <Procore Artifactory> server-id configuration
11:05:09 [🔵Info] Log path: /Users/danfrenette/.jfrog/logs/jfrog-cli.2025-03-11.11-05-09.44188.log
11:05:09 [Debug] Artifactory response: 200
11:05:09 [Debug] Artifactory Call Home: Sending info...
11:05:09 [Debug] Sending HTTP POST request to: https://artifacts.procoretech-qa.com/artifactory/api/system/usage
11:05:09 [Debug] Sending HTTP POST request to: https://artifacts.procoretech-qa.com/jfconnect/api/v1/backoffice/metrics/log
```

4. Observe the logs:

```
[Info] Running curation audit on project: /Users/danfrenette/code/procore/jfrog-cli-testing
[Debug] Sending HTTP GET request to: https://artifacts.procoretech-qa.com/artifactory/api/system/version
[Debug] mapped 1 working directories with indicators/descriptors:
{
  "/Users/danfrenette/code/procore/jfrog-cli-testing": [
    "/Users/danfrenette/code/procore/jfrog-cli-testing/package.json",
    "/Users/danfrenette/code/procore/jfrog-cli-testing/yarn.lock"
  ]
}
[Debug] Detected 1 technologies at /Users/danfrenette/code/procore/jfrog-cli-testing: [yarn].
[Info] Detected: yarn.
[Info] It looks like this project uses 'yarn' to download its dependencies. This package manager however isn't supported by this command.
```


## Expected Behavior

JFrog CLI should work seamlessly with yarn projects, similar to how it works with npm projects.

## Actual Behavior

The JFrog CLI should not throw an error about the unsupported package manager.

## Contact

If you need additional information or have questions about this issue, please contact:

daniel.frenette-contractor@procore.com