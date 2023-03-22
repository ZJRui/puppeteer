FROM node:18

# Install latest chrome dev package and fonts to support major charsets (Chinese, Japanese, Arabic, Hebrew, Thai and a few others)
# Note: this installs the necessary libs to make the bundled version of Chromium that Puppeteer
# installs, work.
RUN apt-get update \
    && apt-get install -y wget gnupg \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | gpg --dearmor -o /usr/share/keyrings/googlechrome-linux-keyring.gpg \
    && sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/googlechrome-linux-keyring.gpg] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update \
    && apt-get install -y google-chrome-stable fonts-ipafont-gothic fonts-wqy-zenhei fonts-thai-tlwg fonts-khmeros fonts-kacst fonts-freefont-ttf libxss1 \
      --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd -r pptruser && useradd -rm -g pptruser -G audio,video pptruser



# 在上面 创建了 用户和用户组 groupadd -r pptruser && useradd -rm -g pptruser -G audio,video pptruser
# -r 表示创建系统用户组或者系统用户  -g 指定用户登陆组的GID或者组名 -m 创建用户的HOme目录 -G 指定用户除了登陆组之外所属的一个或者多个附加组



# 指定使用的用户 user daemon:指定运行容器时的用户名或UID，后续的run 也会使用指定的用户
# 被挂载的目录是root用户的，但是容器内使用的是pptruser用户， ppt用户在挂载目录下创建文件
#会提示没有权限，关于解决 《Docker 容器用户无法操作挂载目录的问题》参考 https://www.yuque.com/wuqimaheihuitailang/ochg4c/zgwsfczo9vtltv9u
#
USER pptruser

#workdir /path/to/wordir:为后续的run cmd entrypoint指定配置工作目录

WORKDIR /home/pptruser

COPY puppeteer-latest.tgz puppeteer-core-latest.tgz ./

# Install puppeteer and puppeteer-core into /home/pptruser/node_modules.
RUN npm i ./puppeteer-core-latest.tgz ./puppeteer-latest.tgz \
    && rm ./puppeteer-core-latest.tgz ./puppeteer-latest.tgz \
    && (node -e "require('child_process').execSync(require('puppeteer').executablePath() + ' --credits', {stdio: 'inherit'})" > THIRD_PARTY_NOTICES)


# dockerfile 中没有使用entrypoint。CMD指定启动容器时执行的命令。 如果用户启动容器时指定了
#运行命令，则会覆盖掉cmd指定的命令。比如 https://pptr.dev/guides/docker 中的示例：
#docker run -i --init --cap-add=SYS_ADMIN --rm ghcr.io/puppeteer/puppeteer:latest node -e "$(cat path/to/script.js)"
#就是指定 运行node scrpt.js

#node -e, --eval=...                      evaluate script
CMD ["google-chrome-stable"]
