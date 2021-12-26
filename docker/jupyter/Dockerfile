FROM jupyter/datascience-notebook:2021-11-10

USER root

RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    g++ && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

ENV LD_LIBRARY_PATH="/usr/local/lib"

# install CRF++
RUN cd /opt \
  && wget --content-disposition "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7QVR6VXJ5dWExSTQ" \
  && tar -zxvf CRF++-0.58.tar.gz \
  && rm CRF++-0.58.tar.gz \
  && cd CRF++-0.58 \
  && ./configure \
  && make \
  && make install

# install MeCab
RUN cd /opt \
  && wget --content-disposition "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7cENtOXlicTFaRUE" \
  && tar -zxvf mecab-0.996.tar.gz \
  && rm mecab-0.996.tar.gz \
  && cd mecab-0.996 \
  && ./configure --with-charset=utf8 \
  && make \
  && make check \
  && make install
RUN cd /opt \
  && wget --content-disposition "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7MWVlSDBCSXZMTXM" \
  && tar -zxvf mecab-ipadic-2.7.0-20070801.tar.gz \
  && rm mecab-ipadic-2.7.0-20070801.tar.gz \
  && cd mecab-ipadic-2.7.0-20070801 \
  && ./configure  --with-charset=utf-8 \
  && make \
  && make install

# install CaboCha
RUN cd /opt \
  && FILE_ID=0B4y35FiV1wh7SDd1Q1dUQkZQaUU \
  && FILE_NAME=cabocha-0.69.tar.bz2 \
  && curl -sc /tmp/cookie "https://drive.google.com/uc?export=download&id=${FILE_ID}" > /dev/null \
  && CODE="$(awk '/_warning_/ {print $NF}' /tmp/cookie)" \
  && curl -Lb /tmp/cookie "https://drive.google.com/uc?export=download&confirm=${CODE}&id=${FILE_ID}" -o ${FILE_NAME} \
  && tar -jxvf cabocha-0.69.tar.bz2 \
  && rm cabocha-0.69.tar.bz2 \
  && cd cabocha-0.69 \
  && ./configure  --with-charset=UTF8 \
  && make \
  && make check \
  && make install \
  && cd python \
  && python setup.py install

RUN ldconfig

