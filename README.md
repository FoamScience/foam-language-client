# A Language Client for OpenFOAM cases

A simple OpenFOAM language extension which adds (some) language support for OpenFOAM
case dictionaries to Visual Studio Code.

## Overview of supported features

Head to [this slide](https://foamscience.github.io/openfoam-with-neovim/#/12) for an overview of all supported features.
Though, in Visual Studio Code you'll be using different commands to trigger them.

## Configuration

This extension **does not** currently provide syntax highlighting support.
We're waiting for [VSCode to support Tree-Sitter](https://github.com/microsoft/vscode/issues/50140).
Mean while, you should continue to use [Zhikui Guo's highlighting extension](https://marketplace.visualstudio.com/items?itemName=zhikui.vscode-openfoam)

Anyway, you'll need to correctly detect the file type for the language client to get triggered;
For example, add the following to your Visual Studio Code settings to recognize OpenFOAM files
(`File->Preferences->Settings`):
```json
"files.associations": {
    "*Dict": "OpenFOAM",
    "*Properties": "OpenFOAM",
    "fvSchemes": "OpenFOAM",
    "fvSolution": "OpenFOAM",
    "**/constant/g": "OpenFOAM",
    "**/0/*": "OpenFOAM"
}
```

## Want to help?

Please refer to [this issue](https://github.com/FoamScience/foam-language-server/issues/7).
