---
layout: post
title: "PostgreSQL as Vector DB"
date:   2023-06-09
tags: [tech]
comments: true
author: GingerNg
---

### Install by docker
```
sudo docker run --name my-postgres -e POSTGRES_PASSWORD=123456 -p 5432:5432 -v /data1/ginger/data/postgres:/var/lib/postgresql/data -d postgres
```


##### Intall pgvector extension
- enter docker container
```
sudo docker exec -it my-postgres bash
```
The following commands are executed in the docker container including
(1) update the software package list
(2) install git, postgresql-server-dev-all, build-essential
(3) clone pgvector from github
(4) make and install pgvector
```
cd /tmp
apt-get update
apt-get install -y git postgresql-server-dev-all build-essential
git clone https://github.com/pgvector/pgvector.git
cd pgvector
make && make install
```


##### Useful PostgreSQL Commands

###### show version of postgresql
```
postgres --version
```
postgres (PostgreSQL) 15.3 (Debian 15.3-1.pgdg110+1)

Use the command below to enter PostgreSQL:
```
psql -U postgres
```

Activate pgvector extension in PostgreSQL
```
CREATE EXTENSION vector;
```

##### Ops for database
```
create database pgvector_example;
```

List all databases in PostgreSQL, meanwhile, show the owner, encoding, collate(排序规则) and Ctype of each database.
```
\l
```

### sql-examples

Create a table with vector type in order to use pgvector extension
```
```
##### sql-example-1
- Create a vector column with 3 dimensions
```
CREATE TABLE items (id bigserial PRIMARY KEY, embedding vector(3));
```

- Insert vectors
```
INSERT INTO items (embedding) VALUES ('[1,2,3]'), ('[4,5,6]');
```
Get the nearest neighbors by L2 distance
```
SELECT * FROM items ORDER BY embedding <-> '[3,1,2]' LIMIT 5;
```

##### sql-example-2
```
CREATE TABLE items1 (id bigserial PRIMARY KEY, sub_id bigserial, embedding vector(3));
```

```
INSERT INTO items1 (sub_id, embedding) VALUES (12, '[1,2,3]'), (13, '[4,5,6]');
```

- query_by_id
```
SELECT * FROM items1 WHERE sub_id = 12;
```

- query_by_ids
```
SELECT * FROM items1 WHERE sub_id IN (12, 13);
```

- query_by_ids cross table
```
SELECT * FROM orders WHERE customer_id IN (SELECT id FROM customers WHERE total_purchases >= 100);
```
- create index
```
CREATE INDEX <tb_name>_<col_name>_idx ON public."<tb_name>" (<col_name>);
```

#### database visualization tool/client
- DBeaver

- *Note*: This post is writen with the help of ChatGPT powed by Poe.