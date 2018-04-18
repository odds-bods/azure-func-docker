# azure-func-docker

This repository is docker image for azure functions.

You can run Azure Function(s) inside this docker container using azure-functions-core-tools.

## Sample dockerfile usage


1. Build and publish azure func binaries to ./out folder. This can be done by running following command:

    ```bash
    dotnet publish -c release -o out
    ```

2. Create your own docker file similar to this one

    ```bash
    FROM oddsbods/azure-func-docker:latest

    WORKDIR /app
    COPY ./out .
    ENV AzureWebJobsScriptRoot=/app

    ENTRYPOINT [ "func", "start" ]
    ```
3. Build docker image

    ```hash
    docker build --rm -f dockerfile -t <YOUR_IMAGE>:<YOUR_TAG> .
    ```

4. Docker run

    ```bash
    docker run -it -p 7071:80 <YOUR_IMAGE>:<YOUR_TAG>
    ```

5. Test/execute function

    ```bash
    curl http://localhost:7071/api/<MY_GET_FUNCTION>
    ```