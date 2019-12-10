FROM alpine:3.6
RUN echo http://dl-cdn.alpinelinux.org/alpine/v3.6/main | tee /etc/apk/repositories \
##    && echo http://dl-cdn.alpinelinux.org/alpine/v3.6/testing | tee -a /etc/apk/repositories \
    && echo http://dl-cdn.alpinelinux.org/alpine/v3.6/community | tee -a /etc/apk/repositories \
    && echo "|--> Install basics pre-requisites" \
    && apk add -U --no-cache tini bash \
        curl ca-certificates python3 py3-numpy py3-numpy-f2py \
        freetype jpeg libpng libstdc++ libgomp graphviz font-noto \
## Setup de basic requeriments
    && echo "|--> Install Python basics" \
    && python3 -m ensurepip \
    && rm -r /usr/lib/python*/ensurepip \
    && pip3 --no-cache-dir install --upgrade pip setuptools wheel \
    && if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip; fi \
    && if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi \
    && ln -s locale.h /usr/include/xlocale.h \
## Dev dependencies and others stuffs...
    && echo "|--> Install build dependencies" \
    && apk add -U --no-cache --virtual=.build-deps \
        build-base linux-headers python3-dev cmake jpeg-dev \
        libffi-dev openblas-dev py-numpy-dev freetype-dev libpng-dev libexecinfo-dev g++ make swig zlib-dev\
    && echo "|--> Install Python packages" \
    && pip install -U --no-cache-dir xgboost numpy pandas scipy \
        nose six Cython lockfile joblib \
        psutil pyyaml liac-arff pynisher>=0.4 pyrfr==0.7.4 \
	smac Pyro4 joblib statsmodels matplotlib
RUN echo "|--> Install ConfigSpace==0.4.7" \
    && pip install -U --no-cache-dir ConfigSpace==0.4.7 \
RUN echo "|--> Install scikit-learn==0.19.0" \
    && pip install -U --no-cache-dir scikit-learn==0.19.0 \
RUN echo "|--> Install auto-sklearn" \
    && pip install -U --no-cache-dir auto-sklearn \
## Cleaning
    && echo "|--> Cleaning" \
    && rm /usr/include/xlocale.h \
    && rm -rf /root/.cache \
    && rm -rf /var/cache/apk/* \
    && apk del .build-deps \
    && find /usr/lib/python3.6 -name __pycache__ | xargs rm -r \
    && rm -rf /root/.[acpw]* \

