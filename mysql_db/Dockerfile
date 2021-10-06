FROM vanjaydo/mysql2redis
#FROM mysql:5.7.18

#Time
ENV TW=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TW /etc/localtime && echo $TW > /etc/timezone

#Add plugin
#COPY addconf/lib_mysqludf_redis_v2.so /usr/lib/mysql/plugin/
#COPY addconf/libhiredis.so /usr/local/lib/
#COPY addconf/libhiredis.so.0.13 /usr/local/lib/

COPY addconf/mysqldb_run.sh /usr/local/bin/
RUN  chmod 755 /usr/local/bin/mysqldb_run.sh
RUN ln -s /usr/local/bin/mysqldb_run.sh /mysqldb_run.sh # backwards compat
ENTRYPOINT ["mysqldb_run.sh"]

EXPOSE 3306
CMD ["mysqld"]

