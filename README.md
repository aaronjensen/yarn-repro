This repo demonstrates yarn corrupting the binary of phantomjs. To repro:

1. Build the docker image and run it locally: 

    ```bash
    $ docker build -t yarnrepro .
    $ docker run --rm -ti -v `pwd`:/repro yarnrepro
    ```

2. Inside the docker container:

    ```bash
    $ yarn
    $ ./node_modules/.bin/phantomjs --version
    # You should see a version number here
    $ exit
    ```

3. Start a new docker container the same way:

    ```bash
    $ docker run --rm -ti -v `pwd`:/repro yarnrepro
    ```

4. Inside the new docker container:

    ```bash
    $ rm node_modules/.yarn-integrity
    $ yarn
    $ ./node_modules/.bin/phantomjs --version
    # You should see a version number here, but there is an error instead
    $ exit
    ```
