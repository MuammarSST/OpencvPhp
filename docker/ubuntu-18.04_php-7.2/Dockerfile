FROM ubuntu:18.04

RUN apt update && export DEBIAN_FRONTEND=noninteractive && apt install -y php-cli wget pkg-config cmake git php-cli php-dev checkinstall

RUN wget https://raw.githubusercontent.com/php-opencv/php-opencv-packages/master/opencv_4.5.5_amd64.deb && dpkg -i opencv_4.5.5_amd64.deb && rm opencv_4.5.5_amd64.deb

RUN git clone https://github.com/php-opencv/php-opencv.git

RUN cd php-opencv && phpize && ./configure --with-php-config=/usr/bin/php-config && make && make test

#build deb package:

RUN cd php-opencv && checkinstall --default --type debian --install=no --pkgname php-opencv --pkgversion "7.2-4.5" --pkglicense "Apache 2.0" --pakdir ~ --maintainer "php-opencv" --addso --autodoinst make install

RUN echo "extension=opencv.so" > /etc/php/7.2/cli/conf.d/opencv.ini
