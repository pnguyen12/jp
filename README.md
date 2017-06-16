[![npm](https://img.shields.io/npm/v/jp-cli.svg)](https://www.npmjs.com/package/jp-cli)
[![prettier](https://img.shields.io/badge/style-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![Beerpay](https://img.shields.io/beerpay/therealklanni/jp.svg)](https://beerpay.io/therealklanni/jp)

# jp

> A tiny commandline tool for parsing JSON from any source.

Based on the idea behind [jq](https://github.com/stedolan/jq) without the need for compiling.
Supports [Lodash .get()](https://lodash.com/docs/4.17.2#get) and [JSONPath](https://github.com/dchester/jsonpath) syntax.

```
npm install -g jp-cli
```

## Usage

```
Pipe jp onto a JSON source from the commandline to parse the output:
  cat data.json | jp [options] query

Options:
  -p, --path      Use JSON Path notation (https://github.com/dchester/jsonpath)
  -k, --keys      Print object keys only                               [boolean]
  -f, --file      Read input from file                                  [string]
  -i, --indent    Number of spaces for indentation (ignored by --human)
                                                           [number] [default: 2]
  -h, --human     Print human-readable (non-JSON) format               [boolean]
  -b, --break     Set break length of object/array for human format     [number]
  -c, --no-color  Disable color for human format                       [boolean]
  -d, --depth     Depth for human format                                [number]
  -L, --line-by-line  Parse each line as a separate input              [boolean]
  --help          Show help                                            [boolean]

Queries use the Lodash get method by default.
For more information, see https://github.com/therealklanni/jp
```

### Examples


> $ cat user-response.json | jp data.user

```js
{
  "name": "Gazorpazorpfield"
  "color": "orange"
}
```

> $ cat user-response.json | jp data.user | jp --keys

```js
[
  "name",
  "color"
]
```

> $ cat user-response.json | jp data.user.name

```js
"Gazorpazorpfield"
```

jp can also parse JSON line by line from an input

> $ [ipfs](https://github.com/ipfs/ipfs) log tail | jp -Lh event

```js
'updatePeer'
'handleFindPeerBegin'
'handleFindPeer'
'updatePeer'
'handleFindPeerBegin'
'handleFindPeer'
'Bitswap.Rebroadcast.active'
'Bitswap.Rebroadcast.idle'
... until you ^C
```
