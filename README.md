# Build Chain files generator

It's a tool either to be used as a javascript library, a CLI or a github actions. The tool generate files (images, project-list.txt, ...) based on a build-chain definition file. See: [Github Action Build Chain](https://github.com/kiegroup/github-action-build-chain/).

## Allowed configuration files versions

- 2.0

## Input Fields

- **definition-file** (mandatory): `path to the file in filesystem | URL to the file`

  > Example:
  >
  > ```
  > definition-file: './folder/whatever_definition_file.yaml'
  > definition-file: 'http://yourdomain.com/definition-file.yaml'
  > definition-file: 'https://raw.githubusercontent.com/kiegroup/droolsjbpm-build-bootstrap/master/.ci/pull-request-config.yaml'
  > definition-file: 'https://raw.githubusercontent.com/kiegroup/droolsjbpm-build-bootstrap/${BRANCH}/.ci/pull-request-config.yaml'
  > definition-file: 'https://raw.githubusercontent.com/${GROUP}/droolsjbpm-build-bootstrap/${BRANCH}/.ci/pull-request-config.yaml'
  > definition-file: 'https://raw.githubusercontent.com/${GROUP}/${PROJECT_NAME}/${BRANCH}/.ci/pull-request-config.yaml'
  > ```

  output-file-path:
  description: "the output file path to store the produced file"
  required: true
  font:
  description: "the font used to generate image, something like `14px Arial`"
  required: false

- **file-type** (required): The file type you want to produce. Possible values:

  - image: it will generate the file image based on the definition file.
  - repository-list: it will generate a plain text file with the full downstream dependency information.

- **output-file-path** (required): The file path where the file will be stored. For instance:

  > ```
  > output-file-path: 'folderx/my-project-hierarchy.png'
  > output-file-path: 'project-list.txt'
  > ```

  > **_Note:_** It make sense in case this is part of a flow where the files are either archived or stored as a new push to the repository/pull request.

- **font** (optional): The font size and name to produce the image. For instance:

  > ```
  > font: '14px Liberation Serif'
  > font: '11px IBM Plex Sans Condensed 2'
  > ```

## CLI Usage

### Generate Image

Check this example: `build-chain-files-generator -df https://raw.githubusercontent.com/kiegroup/droolsjbpm-build-bootstrap/master/.ci/pull-request-config.yaml -o image.png image`

where:

- `-df`: is the definition file
- `-o`: the file path to store the file
- `image`: the file type to generate

### Generate Repository list file

Check this example: `build-chain-files-generator -df ./pull-request-config.yaml -o file.txt repository-list`

where:

- `-df`: is the definition file
- `-o`: the file path to store the file
- `image`: the file type to generate
