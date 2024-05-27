#Use the official PostgreSQL image from the Docker Hub
FROM postgres:14.1-alpine

#Let’s have a simple postgres server running
ENV POSTGRES_DB=db \
    POSTGRES_USER=usr \
    POSTGRES_PASSWORD=pwd

# Adding initialization script
COPY CreateScheme.sql /docker-entrypoint-initdb.d/01-CreateScheme.sql
COPY InsertData.sql /docker-entrypoint-initdb.d/02-InsertData.sql