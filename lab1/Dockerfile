FROM ubuntu
RUN apt-get update 
RUN apt-get install -y figlet
RUN apt-get install -y make gcc
COPY hello.c /
RUN make hello
#CMD /hello
#ENTRYPOINT ["figlet","marioumet"]
ENV var1="salut! avec ENV"
WORKDIR	/test
