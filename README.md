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

## Main innovations

### Direct node append
In addition to the existing document composition style:
```php
$document = (new Document())
    ->bulletlist()
        ->item()
            ->paragraph()
                ->text('item 1')
            ->end()
        ->end()
        ->item()
            ->paragraph()
                ->text('item 2')
            ->end()
        ->end()
    ->end()
;
```
An alternative method has been added to directly add nodes for more complex composition:
```php
$document = (new Document())
    ->append(
        (new BulletList())
            ->append(
                (new ListItem())
                    ->append(
                        (new Paragraph())
                            ->append(new Text('item 1'))
                    ),
                (new ListItem())
                    ->append(
                        (new Paragraph())
                            ->append(new Text('item 2'))
                    )
                    
            )
    )
;
```
In this case, it will be possible to create and append nodes dynamically:
```php
$paragraph = (new Paragraph())->append(new Text('Line 1'));

if (some condition) {
    $paragraph->append(new Text('(doc)', new Link('https://example.com/doc')));
}

$document = (new Document())->append($paragraph);
```

### Extension node

Although element `Extension` is not described in [Atlassian Document Format](https://developer.atlassian.com/cloud/jira/platform/apis/document/structure/), in practice it is used in documents for the Confluence. One of the most famous extensions is, for example, the **Table of Contents**.

A new node type `Extension` has been added:
```php
$document = (new Document())
    ->extension(
        'default',
        'com.atlassian.confluence.macro.core',
        'toc',
        [
            "macroParams" => [
                "maxLevel" => [
                    "value" => "3"
                ],
                "minLevel" => [
                    "value" => "1"
                ],
                "outline" => [
                    "value" => "false"
                ],
                "printable" => [
                    "value" => "false"
                ],
                "type" => [
                    "value" => "list"
                ]
            ]
        ],
        '123cad9c-95d8-49df-8b99-00886ba0af5d',
    )
;
```
or using direct node append:
```php
$document = (new Document())
    ->append(
        new Extension(
            'default',
            'com.atlassian.confluence.macro.core',
            'toc',
            [
                "macroParams" => [
                    "maxLevel" => [
                        "value" => "3"
                    ],
                    "minLevel" => [
                        "value" => "1"
                    ],
                    "outline" => [
                        "value" => "false"
                    ],
                    "printable" => [
                        "value" => "false"
                    ],
                    "type" => [
                        "value" => "list"
                    ]
                ]
            ],
            '123cad9c-95d8-49df-8b99-00886ba0af5d',
        )
    )
;
```

## Credits
- Thanks to [all contributors](https://github.com/DamienHarper/adf-tools/graphs/contributors)

## License
`adf-tools` is free to use and is licensed under the [MIT license](http://www.opensource.org/licenses/mit-license.php)
