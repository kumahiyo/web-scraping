FROM python:3.7

WORKDIR /var/www/html

# install firefox
RUN echo "deb http://deb.debian.org/debian/ unstable main contrib non-free" >> /etc/apt/sources.list.d/debian.list
RUN apt-get update
RUN apt-get install -y --no-install-recommends firefox

# install geckodriver
RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.30.0/geckodriver-v0.30.0-linux64.tar.gz
RUN tar -zxvf geckodriver-v0.30.0-linux64.tar.gz
RUN chmod +x geckodriver
RUN mv geckodriver /usr/local/bin

# install scrapy and scrapy-selenium
RUN python -m pip install --upgrade pip
RUN pip install scrapy
RUN pip install scrapy-selenium

# install pandas
RUN pip install pandas
RUN pip install openpyxl
RUN pip install xlrd
RUN pip install xlwt

# see: https://github.com/clemfromspace/scrapy-selenium/pull/101/commits/841b106b1fd8dfd1e364824c06e91cceefcb7f0a
RUN mv /usr/local/lib/python3.7/site-packages/scrapy_selenium/middlewares.py /usr/local/lib/python3.7/site-packages/scrapy_selenium/middlewares.py.bk
COPY ./lib/scrapy-selenium/patch/middlewares.py /usr/local/lib/python3.7/site-packages/scrapy_selenium/

EXPOSE 80