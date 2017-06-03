FROM docker.io/ubuntu:16.04

MAINTAINER Michael Green micke.green@gmail.com

RUN apt-get update -qq \
        && apt-get upgrade -y

RUN apt-get install -y --no-install-recommends \
                apt-transport-https \
                software-properties-common \
                curl \
                wget \
                git \
                libssl-dev \
                libcurl4-gnutls-dev \
                vim \
        && rm -rf /var/lib/apt/lists/*

RUN apt-get clean && apt-get -y update && apt-get install -y locales && locale-gen en_US.UTF-8
## Configure default locale, see https://github.com/rocker-org/rocker/issues/19
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.utf8 && /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

RUN add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)/" \
        && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    software-properties-common ed less locales vim-tiny wget \
    ca-certificates libcurl4-openssl-dev libssl-dev \
  && add-apt-repository --enable-source --yes "ppa:marutter/rrutter" \
  && add-apt-repository --enable-source --yes "ppa:marutter/c2d4u"

RUN apt-get update -qq \
        && apt-get install -y --no-install-recommends \
                r-base-dev \
                r-recommended \
                r-cran-devtools \
                r-cran-ggplot2 \
                r-cran-tidyr \
        && echo 'options(repos = c(CRAN = "https://cloud.r-project.org"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
        && rm -rf /var/lib/apt/lists/*

CMD ["R"]
