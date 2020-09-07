FROM rasa/rasa:latest-full 

WORKDIR /app
COPY . /app
COPY ./data /app/data

USER root

RUN pip3 install tensorflow==2.1.0 && pip3 install actions && pip3 install google && pip3 install typing==3.7.4.3 && pip3 install tweepy==3.8.0 && pip3 install beautifulsoup4==4.9.0 && pip3 install numpy==1.17.1 && pip3 install pandas==1.0.3 && pip3 install matplotlib==3.2.2 && pip3 install scipy==1.4.1 && pip3 install rasa==1.10.2 && pip3 install nltk==3.4.5 

USER 1001

RUN  rasa train

VOLUME /app
VOLUME /app/data
VOLUME /app/models

EXPOSE 5005

FROM rasa/rasa-sdk:latest

 # The Rasa SDK image runs as non-root user by default. Hence, you have to switch
 # back to the `root` user if you want to install additional dependencies
USER root

# RUN pip3 install tensorflow==2.1.0  && pip3 install actions && pip3 install google && pip3 install typing==3.7.4.3 && pip3 install tweepy==3.8.0 && pip3 install beautifulsoup4==4.9.0 && pip3 install # numpy==1.17.1 && pip3 install pandas==1.0.3 && pip3 install matplotlib==3.2.2 && pip3 install scipy==1.4.1 && pip3 install rasa==1.10.2 && pip3 install nltk==3.4.5

# Switch back to a non-root user
USER 1001

EXPOSE 5055

#ADD ./services.sh /app
#RUN chmod +x /app/services.sh

CMD ["rasa","run","-m","/app/models","--enable-api","--cors","*","--debug","&&","rasa","run","actions"] #add -p $PORT infront of each command
