FROM rocker/verse:3.6.2

RUN apt-get update \
        && apt-get install -y --no-install-recommends \
        pandoc \
        r-base

RUN install2.r --error --deps TRUE \
        DiagrammeR \
        brms

RUN install2.r --error --deps TRUE \
        extrafont \
        xkcd \
        && R -e "download.file('http://simonsoftware.se/other/xkcd.ttf',dest='xkcd.ttf', mode='wb')" \
        && R -e "require(extrafont); system('mkdir -p ~/.fonts'); system('cp xkcd.ttf ~/.fonts'); font_import(pattern = '[X/x]kcd', prompt=FALSE)" \
        && R -e "require(extrafont); loadfonts()"

RUN R -e "if (!requireNamespace('BiocManager', quietly = TRUE)) install.packages('BiocManager'); BiocManager::install('rhdf5')"

RUN install2.r --error --deps TRUE \
        blogdown \
        && R -e "blogdown::install_hugo()"

