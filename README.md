# jupyterlab-mathjax3-web

A JupyterLab extension for rendering math with MathJax **3**.

The default LaTeX renderer in JupyterLab uses MathJax **2**. This extension substitutes the MathJax 2 renderer with the MathJax 3 renderer. 

Compared to the official [jupyterlab-mathjax3](https://github.com/jupyterlab/jupyter-renderers/tree/master/packages/mathjax3-extension) which introduces the MathJax 3 into JupyterLab via **node** and **webpack**, this extension exposes MathJax 3 to the browser's global environment by loading script from the **web**, so that MathJax 3 can be used by other components in JupyterLab like our [jsxgraph-magic](https://github.com/chunxy/jsxgraph-magic.git).

## Requirements

- JupyterLab >= 3.0

## Install

To install the extension, execute:

```shell
pip install jupyterlab-mathjax3-web
```

## `tex` configuration

This MathJax 3 extension allows user configuration. MathJax 3 is [configured via a global JavaScript object](https://docs.mathjax.org/en/latest/web/configuration.html#web-configuration). Therefore, we can configure it in a [JSON](https://en.wikipedia.org/wiki/JSON) file and load this configuration every time we open the JupyterLab.

Out of the many configurable items, `tex` is the most useful and applicable one to be accessed by users. It controls math delimiters, macros, packages, etc. We decide to make `tex` configuration available in this extension.

To configure your `tex` options, open **Setting -> MathJax 3 Config...** This will open the **Advanced Settings** page of JupyterLab. There you will find a **MathJax 3 Config** item. The **System Defaults** will be

```json
{
    "displayMath": [
        [
            "$$",
            "$$"
        ],
        [
            "\\[",
            "\\]"
        ]
    ],

    "inlineMath": [
        [
            "$",
            "$"
        ],
        [
            "\\(",
            "\\)"
        ]
    ],

    "processEnvironments": true,

    "processEscapes": true
}
```

Open and edit the **User Preferences** according to MathJax's `tex` schema. For example, you can add macros and add tags with

```json
{
    "macros": {
        R: "\\mathbb{R}", 
        E: "\\mathrm{E}", 
        RR: "{\\bf R}",
        bold: ["{\\bf #1}",1]
    },
    "tags": "all",
}
```

For a full list configurable options under `tex`, please refer to [MathJax's webpage](https://docs.mathjax.org/en/latest/options/input/tex.html).

## Contributing

### Development install

Note: You will need NodeJS to build the extension package.

The `jlpm` command is JupyterLab's pinned version of [yarn](https://yarnpkg.com/) that is installed with JupyterLab. You may use `yarn` or `npm` in lieu of `jlpm` below.

```shell
# Clone the repo to your local environment
# Change directory to the jupyterlab-mathjax3-web directory
# Install package in development mode
pip install -e .
# Link your development version of the extension with JupyterLab
jupyter labextension develop . --overwrite
# Rebuild extension Typescript source after making changes
jlpm run build
```

You can watch the source directory and run JupyterLab at the same time in different terminals to watch for changes in the extension's source and automatically rebuild the extension.

```shell
# Watch the source directory in one terminal, automatically rebuilding when needed
jlpm run watch
# Run JupyterLab in another terminal
jupyter lab
```

With the watch command running, every saved change will immediately be built locally and available in your running JupyterLab. Refresh JupyterLab to load the change in your browser (you may need to wait several seconds for the extension to be rebuilt).

By default, the `jlpm run build` command generates the source maps for this extension to make it easier to debug using the browser dev tools. To also generate source maps for the JupyterLab core extensions, you can run the following command:

```shell
jupyter lab build --minimize=False
```

### Development uninstall

```shell
pip uninstall jupyterlab-mathjax3-web
```

Then you need to manually remove the `labextension` because it seems that the above won't remove these JupyterLab files:

```shell
cd PYTHON_ENV/share/jupyter/labextensions
rm jupyterlab-mathjax3-web -rf
```

where `PYTHON_ENV` should be expanded to your Python environment.

## Note

This JupyterLab extension will disable the official MathJax 2 and MathJax 3 extension to avoid potential conflict.
