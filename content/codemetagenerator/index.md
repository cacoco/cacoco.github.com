# codemetagenerator [![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/cacoco/codemetagenerator)
This project is a [CodeMeta](https://codemeta.github.io/) project description generator written in [Go](https://go.dev/). View the [project on GitHub](https://github.com/cacoco/codemetagenerator).

## Installation
To install this project, you need to have [Go](https://go.dev/) installed on your machine. Once you have Go installed, you can clone this repository and build the project.

```bash
git clone https://github.com/cacoco/codemetagenerator.git
cd codemetagenerator
go build
```

Then install via `go install`

## Usage
To run this project, you can use the following commands:

```bash 
codemetagenerator --help
```

### Commands
```bash
Available Commands:
  add         Adds resources [authors, contributors, keywords] to the in-progress codemeta.json file
  clean       Clean the $HOME/.codemetagenerator directory
  delete      Delete an arbitrary key and its value from the in-progress codemeta.json file.
  generate    Generate the final codemeta.json file to the optional output file or to the console
  help        Help about any command
  licenses    List (or refresh cached) SPDX license IDs
  new         Start a new codemeta.json file. When complete, run "codemetagenerator generate" to generate the final codemeta.json file
  set         Set the value of an arbitrary key in the in-progress codemeta.json file.
```

#### New
To start a new `codemeta.json` file:

```bash
codemetagenerator new
```

This will walk you through an interactive session and will store an "in-progress" `codemeta.json` file. The expectation is that
you will continue to add more metadata, e.g., `author`, `contributor`, or `keyword`.

#### Add
Add helps with the addition of 3 specific fields: `author`, `contributor`, or `keyword`. The command provides a wizard for adding these values. 

For example to add an `author`:

```bash
codemetagenerator add author
```

will walk you through an interactive session to create a [`Person`](https://schema.org/Person) or [`Organization`](https://schema.org/Organization) author. This command can be run multiple times to add more authors. Similarly, this can also be done for adding one or more contributors:

```bash
codemetagenerator add contributor
```

Again, this command can be run multiple times to add more contributors.

To add one or more keywords:

```bash
codemetagenerator add keyword "Java" "JVM" "etc"
```

The `keyword` command accepts multiple terms but can also be run multiple times to add more keywords.

#### Delete
Properties can be removed by running the `delete` command. This allows for removing *any value* in the `codemeta.json` file for a given key specified via the [Path Syntax](#path-syntax).

```bash
codemetagenerator delete "version"
```

#### Set
New properties can be inserted or exisiting properties can be updated in the `codemeta.json` file with the `set` command. Keys must be specified via the [Path Syntax](#path-syntax).

```bash
codemetagenerator set "relatedLink" "https://thisisrelated.org"
```

#### Generate
Once creating and editing are done, you can run `generate` to produce a final `codemeta.json`. Generation accepts an optional `-o | --output` flag that allows for specifying an output file. If this flag is not provided, the output is sent to the console.

```bash
codemetagenerator generate
```

### Path Syntax
The syntax follows the `sjson` ([https://github.com/tidwall/sjson](https://github.com/tidwall/sjson)) [Path Syntax](https://github.com/tidwall/sjson?tab=readme-ov-file#path-syntax).

## CodeMeta
[CodeMeta](https://codemeta.github.io) is a [JSON-LD](https://json-ld.org/) file format used to describe software projects. See a [full example](https://github.com/ropensci/codemetar/blob/main/codemeta.json).


## License
[Apache License 2.0](https://spdx.org/licenses/Apache-2.0.html)

Copyright 2024 [Christopher Coco](https://angstrom.io/about)

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.