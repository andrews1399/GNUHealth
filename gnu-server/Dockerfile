FROM tryton/tryton:6.4
CMD ["/bin/bash"]
USER root
ENV T_MAJOR 6.4

RUN apt-get update && apt-get install -y --no-install-recommends \
    gzip curl ca-certificates
RUN apt-get install -y wget \
    gnupg \
    patch
#RUN useradd -ms /bin/bash gnuhealth
#USER gnuhealth
#WORKDIR "/home/gnuhealth"
#USER gnuhealth
#RUN apt-cache policy patch
#RUN apt-get utils 
RUN wget "https://ftp.gnu.org/gnu/health/gnuhealth-latest.tar.gz" \
    && gpg --recv-key  --keyserver  keyserver.ubuntu.com 0xC015E1AE00989199 \
    && gpg --with-fingerprint --list-keys 0xC015E1AE00989199 \
    && wget https://ftp.gnu.org/gnu/health/gnuhealth-4.0.3.tar.gz.sig \
    && gpg --verify -n gnuhealth-4.0.3.tar.gz.sig gnuhealth-latest.tar.gz \
    && tar xzf gnuhealth-latest.tar.gz 
WORKDIR "/gnuhealth-4.0.3"
RUN wget -qO- https://ftp.gnu.org/gnu/health/gnuhealth-setup-latest.tar.gz | tar -xzvf - \
    && bash ./gnuhealth-setup install \
    && source ${HOME}/.gnuhealthrc \
    && cd \
    && bash ./start_gnuhealth.sh