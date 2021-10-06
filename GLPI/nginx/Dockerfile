FROM nginx:1.20.0
#FROM nginx:1.15.1

RUN apt update && \
    apt install -y bash tzdata curl ca-certificates s6 nginx-extras

#Time
ENV TW=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TW /etc/localtime && echo $TW > /etc/timezone  


EXPOSE 80
CMD ["nginx","-g","daemon off;"]
