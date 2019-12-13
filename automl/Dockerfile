FROM python:3.6.8-alpine3.8

RUN apk add --update --no-cache \
    --virtual=.build-dependencies \
    git && \
    mkdir /src && \
    cd /src && \
    git clone --recursive -b v0.81 https://github.com/dmlc/xgboost && \
    sed -i '/#define DMLC_LOG_STACK_TRACE 1/d' /src/xgboost/dmlc-core/include/dmlc/base.h && \
    sed -i '/#define DMLC_LOG_STACK_TRACE 1/d' /src/xgboost/rabit/include/dmlc/base.h && \
    apk del .build-dependencies

RUN apk add --update --no-cache \
    --virtual=.build-dependencies \
    make gfortran gcc musl-dev linux-headers swig cmake \
    python3-dev \
    py-setuptools g++ && \
    apk add --no-cache openblas lapack-dev libexecinfo-dev freetype-dev libstdc++ libgomp && \
    pip install setuptools && \
    pip install Cython==0.29.7 && \
    pip install numpy==1.16.1 && \
    pip install scipy==1.3.0 && \
    pip install pandas==0.24.2 scikit-learn==0.21.3 && \
    pip install statsmodels==0.10.1 && \
    pip install joblib && \
    pip install psutil && \
    pip install ConfigSpace==0.4.10 && \
    pip install pynisher==0.4.2 && \
    pip install pyrfr==0.8.0 && \
    pip install matplotlib && \
    pip install lightgbm && \
    pip install sobol_seq && \
    pip install lazy_import && \
    pip install pymongo && \
    pip install hyperopt && \ 
    ln -s locale.h /usr/include/xlocale.h && \
    cd /src/xgboost; make -j4 && \
    cd /src/xgboost/python-package && \
    python3 setup.py install && \
    rm /usr/include/xlocale.h && \
    rm -r /root/.cache && \
    rm -rf /src && \
    apk del .build-dependencies
