* create mongodb instance:
    ```
    sudo docker run --name mongodb-test -d -p 27017:27017 mongo:latest
    ```

* start the instance:
    ```
    sudo docker start mongodb-test
    ```

* stop the instance:
    ```
    sudo docker stop mongodb-test
    ```

* lookup the ps:
    ```
    sudo docker ps
    ```

* connection string:
    ```
    mongodb://localhost:27017 
    ```