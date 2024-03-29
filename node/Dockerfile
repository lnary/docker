FROM node:12.2-stretch

MAINTAINER kennylee26 <kennylee26@gmail.com>

RUN apt-get update && \
    apt-get install -y curl git unzip vim wget && \
    apt-get install -y locales kde-l10n-zhcn && \ 
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 由于各大镜像源间接性抽风，谨慎起见还是从官方源安装
# 如果必需本地构建，再尝试挪到上面，不过就得看看当时镜像源是否抽风了。
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY stretch.sources.list /etc/apt/sources.list

RUN sed -i 's/# zh_CN.UTF-8 UTF-8/zh_CN.UTF-8 UTF-8/g' /etc/locale.gen

RUN locale && locale-gen "zh_CN.UTF-8"
       
# Set environment variables.
ENV HOME /root
ENV LANG=zh_CN.UTF-8\
    LANGUAGE=zh_CN:zh:en_US:en\
    LC_ALL=zh_CN.UTF-8\
    TZ=Asia/Shanghai\
    TERM=xterm

RUN ln -fs /usr/share/zoneinfo/$TZ /etc/localtime && \
            echo $TZ > /etc/timezone && \        
            dpkg-reconfigure --frontend noninteractive tzdata && \
            dpkg-reconfigure --frontend noninteractive locales

# Define working directory.
WORKDIR $HOME

# add cnpm for taobao registry
RUN npm install -g cnpm --registry=https://registry.npm.taobao.org

CMD [ "node" ]
