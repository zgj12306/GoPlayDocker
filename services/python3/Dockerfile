FROM python:3

RUN apt-get update -yqq && apt-get install -yqq openssh-server && apt-get install -yqq openssh-client
WORKDIR /usr/src/app

RUN mkdir -p ~/.pip && touch ~/.pip/pip.conf && echo "[global]"> ~/.pip/pip.conf && echo "index-url = https://pypi.tuna.tsinghua.edu.cn/simple">> ~/.pip/pip.conf

RUN pip install DateTime>=4.2 &&  pip install Flask>=0.12.2
RUN pip install itsdangerous>=0.24 Jinja2>=2.10 MarkupSafe>=1.0 numpy>=1.14.2 pandas>=0.22.0 patsy>=0.5.0 pip>=9.0.3
RUN pip install PyMySQL>=0.8.0 python-dateutil>=2.7.0 pytz>=2018.3 setuptools>=18.2 six>=1.11.0 SQLAlchemy>=1.2.12 statsmodels>=0.8.0 Werkzeug>=0.14.1 wheel>=0.30.0 zope.interface>=4.4.3

#RUN pip install tqdm matplotlib empyrical
RUN pip install hmmlearn sklearn
RUN pip install tushare simplejson bs4 Flask-MySQLdb Django && pip install tushare --upgrade
RUN sed -i "36a PubkeyAuthentication yes #启用公钥私钥配对认证方式 \nPermitRootLogin yes #允许root用户使用ssh登录" /etc/ssh/sshd_config
RUN echo "root:root" | chpasswd

RUN apt-get install -yqq vim
RUN apt-get install -yqq man && apt-get install -yqq lsof
RUN pip install --upgrade pip && pip install uwsgi
RUN pip install ipython jupyter arch
RUN pip install jqdatasdk docxtpl

RUN echo "alias ll='ls -al'" >> /root/.profile
EXPOSE 22
