# MySql benchmark 

Created based on https://www.digitalocean.com/community/tutorials/how-to-measure-mysql-query-performance-with-mysqlslap

Big thanks for Sadequl Hussain who describe it.

## Requirements

- docker, docker-compose
- jupyter-notebook
- mysql-client

## How to run it?

```docker-compose up```

Phpmyadmin url: http://0.0.0.0:8183 (u: root; p:toor)

## How to test the speed?

```mysqlslap --user=root --password --host=0.0.0.0  --concurrency=4 --number-of-queries=20 --create-schema=employees --query="test_queries1.sql" --delimiter=";" --verbose --iterations=2```

Example output:
```
Benchmark
	Average number of seconds to run all queries: 16.969 seconds
	Minimum number of seconds to run all queries: 16.835 seconds
	Maximum number of seconds to run all queries: 17.103 seconds
	Number of clients running queries: 4
	Average number of queries per client: 5
```

## How to change mysql configuration?

Edit docker-compose.yml `command: --key_buffer_size=384M --sort_buffer_size=4M`

Which is here:
```
services:
  mysql:
    image: mysql:5.6
    container_name: dev_mysql
    command: --key_buffer_size=384M --sort_buffer_size=4M
```

## How to generate new queries?

There is a file called query_generator.ipynb it is python jupyter notebook file. Use it to generate queries and then replace test_queries1.sql file where is current output.