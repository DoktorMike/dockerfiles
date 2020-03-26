FROM rocker/verse:3.6.2

MAINTAINER Michael Green (micke.green@gmail.com)

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
        && apt-get install -y --no-install-recommends \
        pandoc \
        r-base \
        r-cran-rstan \
        libgdal-dev \
        libudunits2-dev

RUN R -e "if (!requireNamespace('BiocManager', quietly = TRUE)) install.packages('BiocManager'); BiocManager::install('rhdf5')"

RUN install2.r --error --deps TRUE remotes \
        && R -e "require(remotes); remotes::install_github('DoktorMike/datools')"

RUN install2.r --error --deps TRUE \
        survival \
        extrafont \
        xkcd \
        blogdown \
        DiagrammeR \
        brms \
        ggmcmc \
        plotly \
        && R -e "download.file('http://simonsoftware.se/other/xkcd.ttf',dest='xkcd.ttf', mode='wb')" \
        && R -e "require(extrafont); system('mkdir -p ~/.fonts'); system('cp xkcd.ttf ~/.fonts'); font_import(pattern = '[X/x]kcd', prompt=FALSE)" \
        && R -e "require(extrafont); loadfonts()" \
        && R -e "require(remotes); remotes::install_github('DoktorMike/datools')" \
        && R -e "blogdown::install_hugo()"

