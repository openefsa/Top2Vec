FROM rocker/r-ver:4.1.1

RUN apt-get update && apt-get -y install expect curl rlwrap libssl-dev build-essential zlib1g-dev  libncurses5-dev libgdbm-dev libnss3-dev  libreadline-dev libffi-dev  libbz2-dev libbluetooth-dev libbz2-dev libdb-dev libexpat1-dev libffi-dev libgdbm-dev liblzma-dev libmpdec-dev libncursesw5-dev libreadline-dev libsqlite3-dev libssl-dev zlib1g-dev  git libbz2-dev

RUN curl -O https://www.python.org/ftp/python/3.9.7/Python-3.9.7.tar.xz
RUN tar xf Python-3.9.7.tar.xz
RUN cd Python-3.9.7 && ./configure --enable-shared --with-ensurepip=install && make && make install && ldconfig

RUN unbuffer pip3 install numpy==1.20.3
COPY requirements.txt .
RUN unbuffer pip3 install -r requirements.txt

RUN unbuffer git clone https://github.com/openefsa/Top2Vec.git -b progressLog && \
    cd Top2Vec &&  git checkout f4ddb560cb8f9c480388e459ab289eb4fadd6636 && \
    #unbuffer pip3 install -r requirements.txt && \
    unbuffer python3 setup.py develop --no-deps --user
RUN pip3 install numpy==1.20
RUN curl https://gist.githubusercontent.com/behrica/91b3f958fad80247069ade3b96646dcf/raw/7d27ec07bfe7b6cef1598c530bff50882f84ba70/PWI_top2vec.py \
    -o /usr/local/lib/python3.9/site-packages/PWI_top2vec.py
