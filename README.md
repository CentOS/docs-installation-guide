# CentOS Installation Guide

This repository contains the sources that make up the [CentOS Installation Guide](https://docs.centos.org/en-US/centos/install-guide/). Please report Issues and submit Pull Requests for **Content Fixes** here. For other issues or fixes, use:

* [CentOS_Docs](https://github.com/CentOS/docs) - the builder repository for the entire website, including for example structure configuration
* [CentOS_Docs_Web_UI](https://github.com/CentOS/docs-web-ui) - the website's user interface (e.g. CSS styling) sources

## Repository structure

The documentation is broken up into two top level directories. The `legacy_docs`
directory contains the debranded single-page html documentation. As the
directory name implies, the contents of this directory are to be considered
legacy and updates will likely not happen.

The `modules` directory contains ASCIIDoc sources which are actively maintained
and which can be used to build the CentOS 7 Installation Guide using the `build.sh`
and `preview.sh` scripts, as described below. The build script used a Docker container
to run the Antora publishing system and compose a static website out of the ASCIIDoc
sources, and the preview script runs another container with `nginx` that allows you
to preview the site locally. Details are described further in this document.

## Structure

```
|-- README.md
|-- antora.yml ....................... 1.
|-- build.sh ......................... 2.
|-- preview.sh ....................... 3.
|-- site.yml ......................... 4.
`-- modules
    `-- ROOT ......................... 5.
        |-- assets
        |   `-- images ............... 6.
        |       `-- pizza.png
        |-- nav.adoc ................. 7.
        `-- pages .................... 8.
            |-- architecture.adoc
            |-- community.adoc
            |-- faq.adoc
            |-- index.adoc
            |-- pizza-dough.adoc
            `-- pizza-owen.adoc
```

1. Metadata definition.
2. A script that does a local build. Uses docker.
3. A script that shows a preview of the site in a web browser by running a local web server. Uses docker.
4. A definition file for the build script.
5. A "root module of this documentation component". Please read below for an explanation.
6. **Images** to be used on any page.
7. **Menu definition.** Also defines the hierarchy of all the pages.
8. **Pages with the actual content.** They can be also organised into subdirectories if desired.

## Components and Modules

Antora introduces two new terms:

* **Component** — Simply put, a component is a part of the documentation website with its own menu. Components can also be versioned.
* **Module** — A component can be broken down into multiple modules. Modules still share a single menu on the site, but their sources can be stored in different git repositories, even owned by different groups. The default module is called `ROOT` (that's what is in this example; the guide actually uses `install-guide`). If you don't want to use multiple modules, you can use `ROOT`. But to define more modules, simply duplicate the `ROOT` directory and name it anything you want. You can store modules in one or more git repositories.

## How to edit these documents

All of this is written in AsciiDoc. It's a simple mostly-plain-text
markup language. You may want to look at:

* [AsciiDoc Syntax Quick Reference](http://asciidoctor.org/docs/asciidoc-syntax-quick-reference/)
* [AsciiDoc Writer’s  Guide](http://asciidoctor.org/docs/asciidoc-writers-guide/)
* [Antora Documentation](https://docs.antora.org/antora/1.0/page/)

## Local preview

This repo includes scripts to build and preview the contents of this repository. Both scripts use docker, so please make sure you have it installed on your system. Please see below for instructions.

To build and preview the site, run:

```
$ ./build.sh && ./preview.sh
```

The result will be available at http://localhost:8080.

### Installing docker on Fedora

```
$ sudo dnf install docker
$ sudo systemctl start docker && sudo systemctl enable docker
```
