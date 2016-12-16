# atlassian
It's Atlassian docker compose file, to run Atlassian products with docker on one single machine.

```
jira.example.com   wiki.example.com   bitbucket.example.com   pma.exemple.com
       +                   +                    +                    +
       |                   |                    |                    |
       +----------------------------------------+--------------------+
                           |
                           v
                         Nginx
                           +
       +-------------------+----------------------+-----------------------------+
       |                   |                     |                              |
       v                   v                     v                              v
   Atlassian Jira    Atlassian Confluence   Atlassian Bitbucket             PhpMyAdmin
 [host:jira:8080]   [host:confluence:8090]  [host:bitbucket:7990]      [host:phpmyadmin:8080]
       +                   +                     |
       |                   |                     |
       +-----------------------------------------+
                           |
                           v
                         Mysql
                   [host:database:3306]
                           +
                           |
       +------------------------------------------+
       |                   |                      |
       v                   v                      v
   [db:jira]           [db:wiki]          [db:bitbucket]
```


Atlassian supported products:

- Jira `7.2.6`
- Confluence `6.0.2`
- Bitbucket `4.10.1`

With:
- Mysql `5.6`
- Nginx `latest`


Docker image source files:

- [cptactionhank/atlassian-jira](https://hub.docker.com/r/cptactionhank/atlassian-jira/)
- [cptactionhank/atlassian-confluence](https://hub.docker.com/r/cptactionhank/atlassian-confluence/)
- [cptactionhank/atlassian-bitbucket](https://hub.docker.com/r/atlassian/bitbucket-server/)
- [nginx](https://hub.docker.com/_/nginx/)
- [postgres](https://hub.docker.com/_/postgres/)

How to use:

1. Clone the atlassian:
       ```
       $ git clone https://github.com/omidraha/atlassian
       ```
       
2. Make persistent directories:
       ```
       $ mkdir -p ~/workspace/docker/atlassian/jira
       $ mkdir -p ~/workspace/docker/atlassian/confluence
       $ mkdir -p ~/workspace/docker/atlassian/bitbucket
       $ mkdir -p ~/workspace/docker/postgres
       $ mkdir -p ~/workspace/docker/nginx
       ```
       
       The path of directories hard coded on `docker-compose.yml` file, if you want to use another path,
       You also need to apply your change on `docker-compose.yml` file.
       
3. Set permission of directories:
       ```
       $ sudo chown -R daemon:daemon   ~/workspace/docker/atlassian
       ```
       
4. Run docker compose:
       ```
       $ docker-compose up
       ```
       
5. Set `DNS` on somewhere you want to connect to host of `docker-compose`:
       ```
       $ vim /etc/hosts
           127.0.0.1 jira.example.com www.jira.example.com
           127.0.0.1 wiki.example.com www.wiki.example.com
           127.0.0.1 bitbucket.example.com www.bitbucket.example.com
       ```
       Replace `127.0.0.1` with IP of host that `docker-compose` command run on it.

6. Create Data Bases:
       ```
       $ docker exec -it atlassian_database_1  psql -U postgres
           postgres=# CREATE DATABASE jira;
           postgres=# CREATE DATABASE wiki;
           postgres=# CREATE DATABASE bitbucket;
           postgres=# \l
           postgres-# \q
       ```
       
7. Browse Atlassian products:
       ```
       http:://jira.example.com
       http:://wiki.example.com
       http:://bitbucket.example.com
       ```

