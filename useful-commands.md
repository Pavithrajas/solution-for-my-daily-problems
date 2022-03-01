* To know the storage usage: `df -h` 

* To know which path is taking more storage (top 40) for the given root path: `sudo du -x / | sort -n | tail -40`

* Remove docker completely from Amazon linux: 

      sudo yum remove docker \
                    docker-client \
                    docker-client-latest \
                    docker-common \
                    docker-latest \
                    docker-latest-logrotate \
                    docker-logrotate \
                    docker-engine
      And delete

      the directories /var/lib/docker, which contains your images, containers and volumes
      and /etc/docker, which contains docker configuration files.
