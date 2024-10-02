# adf-tools

Atlassian Document Format PHP Tools

This repository is a fork of Damien Harper's original repository [adf-tools](https://github.com/DamienHarper/adf-tools), with the following changes added:

- [Allow direct append for nodes for complex composition](https://github.com/sgrigorjev/adf-tools/pull/1):  allow two alternative ways of constructing a document, one existing through a chain of calls, and one through a direct append of nodes for more complex documents.
- [Added extension node](https://github.com/sgrigorjev/adf-tools/pull/2): added `Extension` node that used in Confluence documents.

### Pull requests to the original repository

- [Allow direct append for nodes for complex composition #16](https://github.com/DamienHarper/adf-tools/pull/16)
- [Added extension node (used in Confluence documents) #17](https://github.com/DamienHarper/adf-tools/pull/17)

If the listed pull requests are accepted by the original library author, this repository will no longer be needed, the original library should be used in that case.

## Documentation
- Documentation of this library can be found [here](doc/index.md).
- [Official Atlassian Document Format](https://developer.atlassian.com/cloud/jira/platform/apis/document/structure/)
- [Atlassian Document Format JSON Schema](https://unpkg.com/@atlaskit/adf-schema@24.0.0/dist/json-schema/v1/full.json)

## Credits
- Thanks to [all contributors](https://github.com/DamienHarper/adf-tools/graphs/contributors)

## License
`adf-tools` is free to use and is licensed under the [MIT license](http://www.opensource.org/licenses/mit-license.php)
