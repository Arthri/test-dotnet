# test-dotnet
A reusable workflow for running tests for .NET projects.

## Installation
Add a new workflow under `.github/workflows` with the following contents,
```yml
name: Continuous Integration

on:
  push:
    branches: [ master, dev ]
  pull_request:
    branches: [ master, dev ]

jobs:
  test:
    uses: Arthri/test-dotnet/.github/workflows/i.yml@v1
```

## Usage

### Machine
The workflow, by default, runs on Ubuntu 24.04 (as of April 09, 2025). The machine that the workflow runs on can be changed by using the `runs-on` input parameter.
```yml
name: Continuous Integration

on:
  push:
    branches: [ master, dev ]
  pull_request:
    branches: [ master, dev ]

jobs:
  test:
    uses: Arthri/test-dotnet/.github/workflows/i.yml@v1
    with:
      runs-on: windows-2022
```

### .NET Version
The workflow uses [actions/setup-dotnet](https://github.com/actions/setup-dotnet) under the hood to setup the .NET environment. The workflow supports overriding the .NET version restored through the `dotnet-version` input parameter, corresponding to the parameter of the same name of actions/setup-dotnet.

### Timeout
The workflow has a default timeout of 5 minutes, which can be changed by setting the `timeout-minutes` input parameter.
```yml
name: Continuous Integration

on:
  push:
    branches: [ master, dev ]
  pull_request:
    branches: [ master, dev ]

jobs:
  test:
    uses: Arthri/test-dotnet/.github/workflows/i.yml@v1
    with:
      # Set the timeout back to the GitHub default of 30 minutes
      timeout-minutes: 30
```

### Additional Arguments
Additional arguments can be passed to the `dotnet test` command using the `test-arguments` input parameter.
```yml
name: Continuous Integration

on:
  push:
    branches: [ master, dev ]
  pull_request:
    branches: [ master, dev ]

jobs:
  test:
    uses: Arthri/test-dotnet/.github/workflows/i.yml@v1
    with:
      # Run the tests on .NET 6
      test-arguments: -f net6.0
```
