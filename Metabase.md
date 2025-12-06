# How to run Metabase using terminal command

Metabase provides an official Docker image via Docker Hub that can be used for deployments on any system that is running Docker. Here’s a one-liner that will start a container running Metabase.

```bash
docker run -d -p 3000:3000 --name metabase metabase/metabase
```

Change into your new Metabase directory and run the JAR. Located in \\wsl.localhost\Ubuntu\home\darwin\metabase

```bash
java --add-opens java.base/java.nio=ALL-UNNAMED -jar metabase.jar
```

Metabase will log its progress in the terminal as it starts up. Wait until you see “Metabase Initialization Complete” and visit localhost:3000.