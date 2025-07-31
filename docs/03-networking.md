# 📞 Mimicking the host network

While in a lab environment, we often want participants to run a container and then connect to it.

For example, start a PostgreSQL container and then use `psql` to connect to it. "Wow! That was easy to start a database!"

But, the Labspace is running inside a container. We don't want to confuse people by having to use `host.docker.internal` (which doesn't resolve while in Docker Offload as well).

## 📋 Try it out

1. In the VS Code terminal, run the following command to start a PostgreSQL container:

    ```sh
    docker run -dp 5432:5432 -e POSTGRES_PASSWORD=secret postgres
    ```

2. Connect to the database using `psql`:

    ```sh
    psql -h localhost -U postgres
    ```

    Enter the password of `secret`. You should see it connect!


### How's it work?

In the Labspace environment is a service called the **host-port-republisher**. It does the following:

1. Watches for container start events for labspace resources (remember the label we're mutating on?)
2. Extract published ports and determine the IP address for the container on the `labspace` network
3. Start `socat` processes to forward traffic from `localhost:PORT` to `container:PORT`.

This works because **the republisher service runs in the same network namespace as the IDE**. Therefore, `localhost` is the same for each container.

To ensure the communication works, the Docker Socket Proxy is mutating all new containers to put them on the Labspace network:

```yaml
mutators:
  - type: addToNetwork
    networks:
      - labspace
```

