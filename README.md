# A Language Client for OpenFOAM cases

A simple OpenFOAM language extension which adds (some) language support for OpenFOAM
case dictionaries to Visual Studio Code.

## Overview of supported features

Head to [this slide](https://foamscience.github.io/openfoam-with-neovim/#/12) for an overview of all
supported features of the underlying LSP server.

A quick run-down of the important features:
1. **An OpenFOAM Language** file type.
2. A Tree-Sitter grammar for OpenFOAM.
3. File symbols (Outline) support for OpenFOAM dictionaries.

## Configuration

### Syntax highlighting

This extension **does not** currently provide syntax highlighting support on its own.
We're waiting for [VSCode to support Tree-Sitter](https://github.com/microsoft/vscode/issues/50140)
and now [Explore using tree sitter for syntax highlighting](https://github.com/microsoft/vscode/issues/210475) to
get merged.

Mean while, you can use this [generic tree-sitter-vscode extension](https://marketplace.visualstudio.com/items?itemName=AlecGhost.tree-sitter-vscode) in the following way (replace `/path/to` with something that works for you):

```bash
npm i -g tree-sitter tree-sitter-cli
git clone https://github.com/tree-sitter/tree-sitter-cpp /path/to/tree-sitter-cpp
cd /path/to/tree-sitter-cpp
tree-sitter build --wasm
git clone https://github.com/FoamScience/tree-sitter-foam /path/to/tree-sitter-foam
cd /path/to/tree-sitter-foam
tree-sitter build --wasm
```

In VScode's extension configuration:
```json
"tree-sitter-vscode.languageConfigs": [
    {
        "lang": "openfoam",
        "parser": "/path/to/tree-sitter-foam/tree-sitter-foam.wasm",
        "highlights": "/path/to/tree-sitter-foam/queries/highlights.scm",
        "injections": "/path/to/tree-sitter-foam/queries/injections.scm"
    },
    {
        "lang": "cpp",
        "parser": "/path/to/tree-sitter-cpp/tree-sitter-cpp.wasm",
        "highlights": "/path/to/tree-sitter-cpp/queries/highlights.scm",
        "injections": "/path/to/tree-sitter-cpp/queries/injections.scm"
    },        
],
```

>[!TIP]
> Configuring the `cpp` grammar helps in highlighting the `code` blocks in
> OpenFOAM dictionaries. Although, this is optional.

### File type detection

You will need to correctly detect the file type for the language client to get triggered;
For example, add the following to your Visual Studio Code settings to recognize some common OpenFOAM case files
(`File->Preferences->Settings`):
```json
"files.associations": {
    "*Dict": "openfoam",
    "*Properties": "openfoam",
    "fvSchemes": "openfoam",
    "fvSolution": "openfoam",
    "**/constant/g": "openfoam",
    "**/0/*": "openfoam"
}
```

### Known issues

Currently, `code system/someDict` will cause the LSP server to segfault.

It is recommended to open the whole case path with VSCode instead: `code .`

## Want to help?

Please refer to [this issue](https://github.com/FoamScience/foam-language-server/issues/7).
