FROM ubuntu:focal

ARG DEBIAN_FRONTEND=noninteractive
RUN echo "===> Installing system dependencies..."
RUN BUILD_DEPS="curl unzip"
RUN apt-get update && apt-get install --no-install-recommends -y unzip python curl python3-pip wget fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libnspr4 libnss3 lsb-release xdg-utils libxss1 libdbus-glib-1-2 libgbm1 $BUILD_DEPS xvfb
RUN echo "===> Installing chromedriver and google-chrome..."
# RUN CHROMEDRIVER_VERSION=`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE`
RUN wget https://chromedriver.storage.googleapis.com/102.0.5005.61/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip -d /usr/bin
RUN chmod +x /usr/bin/chromedriver
RUN rm chromedriver_linux64.zip

RUN wget -O google-chrome.deb "https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb"
RUN dpkg -i google-chrome.deb
RUN apt-get install -y -f
RUN rm google-chrome.deb
RUN echo "===> DISPLAY set..."
RUN export DISPLAY=:0
RUN /usr/bin/Xvfb :0 -screen 0 1024x768x24 &
RUN sleep 5

RUN echo "===> Installing python dependencies..."
RUN pip3 install flask Flask-Cors selenium pybase64 requests PyYAML urllib3 webdriver-manager
RUN echo "===> Remove build dependencies..."
RUN apt-get remove -y $BUILD_DEPS && rm -rf /var/lib/apt/lists/*



ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONUNBUFFERED=1

COPY . /app

WORKDIR /app

# RUN python3 app/templates/swagger-yaml-to-html.py < app/templates/api.yaml > app/templates/doc.html
RUN xvfb-run python3 app/ro.py

CMD python3 app/app.py