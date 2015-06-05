# docker-heka

Our simple heka container.

## Usage

The way to run this is to have your app container generate all the necesary config as a /heka volume.

Then you run this container with something like the following (assuming the container to be monitored is `scc-node1`:

```console
$ docker run --name scc-node1-heka  \
    --net container:scc-node1       \
    --volumes-from scc-node1        \
    -d stellar/heka
```

This will start a heka process using `/heka/hekad.toml` from the app container's exported volume, as well as the same networking stack as the container. The allows the app and hekad to communicate with eachother freely.

Any logs that need to be monitored will also need to be exported as volumes from the app container so that the heka container can see them.
