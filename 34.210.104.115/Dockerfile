FROM jupyter/scipy-notebook
ENV TWITTER_CONSUMER_KEY="
ENV TWITTER_CONSUMER_SECRET=""
ENV TWITTER_ACCESS_TOKEN=""
ENV TWITTER_ACCESS_SECRET=""
USER root
RUN conda install pymongo
RUN pip install tweepy
USER jovyan
