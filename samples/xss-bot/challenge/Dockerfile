FROM kctf-nsjail

# Install latest chrome dev package and fonts to support major charsets (Chinese, Japanese, Arabic, Hebrew, Thai and a few others)
# Note: this installs the necessary libs to make the bundled version of Chromium that Puppeteer installs, work.
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update \
    && apt-get install -yq --no-install-recommends \
       libgconf-2-4 google-chrome-unstable fonts-ipafont-gothic fonts-wqy-zenhei fonts-thai-tlwg fonts-kacst \
       nodejs npm \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /home/user
COPY files /home/user
RUN cd /home/user && npm install puppeteer proof-of-work

# Since we don't need nsjail here, we could also run as user in the k8s config
CMD exec setpriv --init-groups --reset-env --reuid user --regid user --inh-caps=-all -- /usr/bin/bash -c 'while true; do /usr/bin/node /home/user/bot.js; done'
