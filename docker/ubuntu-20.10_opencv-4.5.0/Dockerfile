FROM ubuntu:20.10

RUN apt update && apt install -y wget pkg-config cmake git checkinstall

RUN echo 1

RUN git clone https://github.com/opencv/opencv_contrib.git && git clone https://github.com/opencv/opencv.git

RUN cd opencv_contrib && git checkout tags/4.5.5 && cd ../opencv && git checkout tags/4.5.5-openvino-2022.1.0

RUN mkdir build && cd build && cmake -D OPENCV_GENERATE_PKGCONFIG=YES -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib/modules ../opencv

RUN cd build && make -j16

RUN ldconfig

#build deb package:

RUN cd build && checkinstall --default --type debian --install=no --pkgname opencv --pkgversion "4.5.5" --pkglicense "3-clause BSD License" --pakdir ~ --maintainer "php-opencv" --addso --autodoinst make install
