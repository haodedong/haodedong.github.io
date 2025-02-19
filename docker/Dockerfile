# 使用官方 Nginx 镜像为基础
FROM nginx:alpine

# 设置工作目录（Nginx 默认 HTML 目录）
WORKDIR /usr/share/nginx/html

# 将打包后的 Vue 静态文件（dist 文件夹）复制到镜像中
COPY dist/ ./

# 将自定义的 Nginx 配置文件复制到镜像
COPY default.conf /etc/nginx/conf.d/default.conf

# 暴露端口（默认 80）
EXPOSE 80

# 启动 Nginx
CMD ["nginx", "-g", "daemon off;"]