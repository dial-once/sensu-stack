FROM elasticsearch:2.2.0

# Install the required plugins
RUN plugin install polyfractal/elasticsearch-inquisitor
RUN plugin install royrusso/elasticsearch-HQ
RUN plugin install https://github.com/NLPchina/elasticsearch-sql/releases/download/2.2.0/elasticsearch-sql-2.2.0.zip

CMD ["elasticsearch"]
