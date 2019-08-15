FROM docker.elastic.co/elasticsearch/elasticsearch:6.4.0

ADD ./staysense-cosine-sim-6.4.0.zip /staysense-cosine-sim-6.4.0.zip

# Install phonetic plugin
#RUN elasticsearch-plugin install --batch analysis-phonetic

# Install cosine similarity plugin: https://github.com/StaySense/fast-cosine-similarity
RUN elasticsearch-plugin install file:/staysense-cosine-sim-6.4.0.zip
