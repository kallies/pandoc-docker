# Pandoc Docker Container

[Docker](https://www.docker.io/) container for the source distribution of [Pandoc](http://johnmacfarlane.net/pandoc), with LaTex tools installed.

Based on jagregory/pandoc and modified for usage with [gitlab-ci](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/issues/1421).

    docker run --rm --entrypoint pandoc kallies/pandoc-docker --help

    pandoc [OPTIONS] [FILES]
    Input formats:  docbook, haddock, html, json, latex, markdown, markdown_github,
                    markdown_mmd, markdown_phpextra, markdown_strict, mediawiki,
                    native, opml, rst, textile
    Output formats: asciidoc, beamer, context, docbook, docx, dzslides, epub, epub3,
                    fb2, html, html5, json, latex, man, markdown, markdown_github,
                    markdown_mmd, markdown_phpextra, markdown_strict, mediawiki,
                    native, odt, opendocument, opml, org, pdf*, plain, revealjs,
                    rst, rtf, s5, slideous, slidy, texinfo, textile
                    [*for pdf output, use latex or beamer and -o FILENAME.pdf

A `/source` directory is created in the container, which can be mapped for use with relative file paths. Pandoc will always be run from the `/source` directory in the container.

The Dockerfile describes a user pandoc and executes commands in this context. Make sure this user has write access to your volume (e.g. by using /tmp).

## Examples

html5 output:

    docker run --rm --entrypoint pandoc -v /tmp:/source kallies/pandoc-docker -f markdown -t html5 README.md -o README.html

pdf output:

    docker run --rm --entrypoint pandoc -v /tmp:/source kallies/pandoc-docker -f markdown -t latex README.md -o README.pdf
