FROM ubuntu

WORKDIR /root

RUN apt-get update && apt-get install -y openjdk-8-jdk wget

ENV HADOOP_VERSION 2.8.3
RUN wget https://www.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz && \
    tar -xzvf hadoop-$HADOOP_VERSION.tar.gz && \
    mv hadoop-$HADOOP_VERSION /usr/local/hadoop && \
    rm hadoop-$HADOOP_VERSION.tar.gz

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV HADOOP_HOME=/usr/local/hadoop
ENV PATH=$PATH:/usr/local/hadoop/bin:/usr/local/hadoop/sbin

RUN mkdir -p /data/hdfs/namenode && \
    mkdir -p /data/hdfs/datanode && \
    mkdir -p /data/hdfs/snn && \
    mkdir -p /data/yarn/nodemanager && \
    mkdir $HADOOP_HOME/logs

COPY config/* /tmp/

RUN mv /tmp/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml && \
    mv /tmp/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml && \
    mv /tmp/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml && \
    mv /tmp/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml

# format namenode
RUN /usr/local/hadoop/bin/hdfs namenode -format

