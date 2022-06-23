# jupyterlab-mathjax3-global

A JupyterLab extension for rendering math with [MathJax 3](https://github.com/mathjax/mathjax).

The default LaTeX renderer in JupyterLab uses [MathJax 2](https://www.mathjax.org/). This extension substitutes the MathJax 2 renderer with the MathJax 3 renderer. 

Compared to the official [jupyterlab-mathjax3](https://github.com/jupyterlab/jupyter-renderers/tree/master/packages/mathjax3-extension), this extension exposes the MathJax 3 to the browser's global environment , so that other extensions may also use the MathJax 3.

## Requirements

- JupyterLab >= 3.0

## Install

```bash
git clone https://github.com/chunxy/jupyterlab-mathjax3-global.git
cd jupyterlab-mathjax3-global
pip install ./
```

## Uninstall

```
pip uninstall juyterlab-mathjax3-global
```

## Contributing

### Development install

Note: You will need NodeJS to build the extension package.

The `jlpm` command is JupyterLab's pinned version of
[yarn](https://yarnpkg.com/) that is installed with JupyterLab. You may use
`yarn` or `npm` in lieu of `jlpm` below.

```bash
# Clone the repo to your local environment
# Change directory to the jupyterlab-mathjax3-global directory
# Install package in development mode
pip install -e .
# Link your development version of the extension with JupyterLab
jupyter labextension develop . --overwrite
# Rebuild extension Typescript source after making changes
jlpm run build
```

You can watch the source directory and run JupyterLab at the same time in different terminals to watch for changes in the extension's source and automatically rebuild the extension.

```bash
# Watch the source directory in one terminal, automatically rebuilding when needed
jlpm run watch
# Run JupyterLab in another terminal
jupyter lab
```

With the watch command running, every saved change will immediately be built locally and available in your running JupyterLab. Refresh JupyterLab to load the change in your browser (you may need to wait several seconds for the extension to be rebuilt).

By default, the `jlpm run build` command generates the source maps for this extension to make it easier to debug using the browser dev tools. To also generate source maps for the JupyterLab core extensions, you can run the following command:

```bash
jupyter lab build --minimize=False
```

### Development uninstall

```bash
pip uninstall jupyterlab-mathjax3-global
```

Then you need to manually remove the `labextension` because the development uninstall won't remove these extra files:

```bash
cd PYTHON_ENV/share/jupyter/labextensions
rm jupyterlab-mathjax3-global -rf
```

where `PYTHON_ENV` should be expanded to your Python environment.
