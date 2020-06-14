FROM debian:testing-slim

ARG USER_NAME=latex
ARG USER_HOME=/home/latex
ARG USER_ID=1000
ARG USER_GECOS=LaTeX

ENV DEBIAN_FRONTEND noninteractive

RUN adduser \
    --home "$USER_HOME" \
    --uid $USER_ID \
    --gecos "$USER_GECOS" \
    --disabled-password \
    "$USER_NAME"

ARG WGET=wget
ARG MAKE=make
ARG PANDOC=pandoc
ARG PCITEPROC=pandoc-citeproc
ARG PYGMENTS=python3-pygments
ARG FIG2DEV=fig2dev
ARG JRE=default-jre-headless
ARG PERL=perl
ARG LIBYAML_TINY_PERL=libyaml-tiny-perl
ARG LIBFILE_HOMEDIR_PERL=libfile-homedir-perl
ARG LIBLOG_DISPATCH_PERL=liblog-dispatch-perl
ARG FONTCONFIG=fontconfig
ARG INKSCAPE=inkscape

# mkdir -p /usr/share/man/man1 fixes problems with installing java on ...-slim variants of debian
RUN mkdir -p /usr/share/man/man1 \
    && apt-get update \
    && apt-get install -y \
    texlive-full \
    # some auxiliary tools
    "$WGET" \
    "$MAKE" \
    # markup format conversion tool
    "$PANDOC" \
    "$PCITEPROC" \
    # XFig utilities
    "$FIG2DEV" \
    # syntax highlighting package
    "$PYGMENTS" \
    # Java runtime environment (e.g. for arara)
    "$JRE" \
    # Perl and perl packages for latexindent
    "$PERL" \
    "$LIBYAML_TINY_PERL" \
    "$LIBFILE_HOMEDIR_PERL" \
    "$LIBLOG_DISPATCH_PERL" \
    # Fontconfig for user supplied font configuration
    "$FONTCONFIG" \
    # Inkscape for converting and embedding SVGs
    "$INKSCAPE" \
    # Removing documentation packages *after* installing them is kind of hacky,
    # but it only adds some overhead while building the image.
    && apt-get --purge remove -y .\*-doc$ \
    # Remove more unnecessary stuff
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

USER latex
ENV HOME /home/latex

# Make directories for users to place fonts and fontconfig files into
RUN mkdir -p /home/latex/.config/fontconfig
RUN mkdir -p /home/latex/.local/share/fonts

RUN mkdir /home/latex/work
WORKDIR /home/latex/work
