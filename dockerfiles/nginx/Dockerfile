FROM nginx:1.15.7
# WORKDIR /usr/local/nginx/html

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone