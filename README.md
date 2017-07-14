# Atlassian
It's Atlassian docker compose file, to run Atlassian products with docker on one single machine.

```
jira.example.com   wiki.example.com   bitbucket.example.com    bamboo.example.com      
       +                   +                    +              +
       |                   |                    |              |
       +-------------------------------------------------------+ 
                                      |
                                      v
                                    Nginx
                                      +
       +------------------------------------------------------------------+
       |                   |                     |                        |
       v                   v                     v                        v
   Atlassian Jira    Atlassian Confluence   Atlassian Bitbucket         Bamboo
 [host:jira:8080]   [host:confluence:8090]  [host:bitbucket:7990]  [host:bamboo:8085]
       +                   +                     +                          +
       |                   |                     |                          |
       +-----------------------------------------+--------------------------+
                                      |
                                      v
                                   Postgres
                            [host:database:5432]
                                      +
                                      |
       +---------------------------------------------------------------------+
       |                   |                      |                          |
       v                   v                      v                          v
   [db:jira]           [db:wiki]          [db:bitbucket]                  [db:bamboo]
```


Atlassian supported products:

- Jira `7.3.0`
- Confluence `6.3.1`
- Bitbucket `latest`
- Bamboo `latest`

With:
- Postgres `latest`
- Nginx `latest`

Requirements:

- Docker version 1.13.1+
- docker-compose version 1.10.0+

Docker image source files:

- [cptactionhank/atlassian-jira](https://hub.docker.com/r/cptactionhank/atlassian-jira/)
- [cptactionhank/atlassian-confluence](https://hub.docker.com/r/cptactionhank/atlassian-confluence/)
- [cptactionhank/atlassian-bitbucket](https://hub.docker.com/r/cptactionhank/atlassian-bitbucket/)
- [cptactionhank/atlassian-bamboo](https://hub.docker.com/r/cptactionhank/atlassian-bamboo/)
- [nginx](https://hub.docker.com/_/nginx/)
- [postgres](https://hub.docker.com/r/sameersbn/postgresql/)

How to use:

1. Clone the atlassian:


    ```
    $ git clone https://github.com/omidraha/atlassian
    ```

2. Set environment variables:


    ```
    $ export DOMAIN=example.com
     ```
 
3. Run docker compose:


    ```
    $ docker-compose -p atlassian up
    ```
    
4. Set `DNS` according to the above `DOMAIN` value, on somewhere that you want to connect to host of `docker-compose`:


    ``` 
    $ vim /etc/hosts
        127.0.0.1 jira.example.com www.jira.example.com
        127.0.0.1 wiki.example.com www.wiki.example.com
        127.0.0.1 bitbucket.example.com www.bitbucket.example.com
        127.0.0.1 bamboo.example.com www.bamboo.example.com
    ```
Replace `127.0.0.1` with IP of host that `docker-compose` command run on it.

    
5. Browse Atlassian products:


        ```
        http://jira.example.com
        http://wiki.example.com
        http://bitbucket.example.com
        http://bamboo.example.com
        ```
        
Notes: 

Data persisted on the  named volumes, to see them:


       $ docker volume ls
       local               atlassian_bamboo-data
       local               atlassian_bitbucket-data
       local               atlassian_confluence-data
       local               atlassian_jira-data
       local               atlassian_database-data
