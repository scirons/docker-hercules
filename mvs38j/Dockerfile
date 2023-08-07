FROM debian:stable as builder

RUN apt-get update && apt-get install -y \
  net-tools \
  c3270 \
  procps \
  unzip

WORKDIR /tk4/
ADD https://wotho.ethz.ch/tk4-/tk4-_v1.00_current.zip /tk4/
RUN unzip tk4-_v1.00_current.zip && rm /tk4/tk4-_v1.00_current.zip
RUN echo CONSOLE > /tk4/unattended/mode && \
  sed -ie 's#>log/3033.log##g' /tk4/mvs

FROM debian
LABEL maintainer="Gabriel Marafon - gabriel@scirons.com"
LABEL version="1.00"
LABEL description="OS/VS2 MVS 3.8j Service Level 8505, Tur(n)key Level 4- Version 1.00"
WORKDIR /tk4/
COPY --from=builder /tk4/ .
VOLUME [ "/tk4-/conf","/tk4-/local_conf","/tk4-/local_scripts","/tk4-/prt","/tk4-/dasd","/tk4-/pch","/tk4-/jcl","tk4-/log" ]
CMD ["/tk4/mvs"]
EXPOSE 3270 8038 33351 33352 33353
