# Buildx
|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
| `buildx bake` `buildx f`  |Build from a file | `builder` `-f` `--load` `--metadata-file` `--no-cache` `--print` `--progress` `--pull` `--push` `--sbom` `--set`
| `buildx build` `buildx b` |Start a build using Buildkit |`--add-host` `--allow` `--attest` `--build-arg` `--build-context` `--builder` `--cache-from` `--cache-to` `--cgroup-parent` `--detach` `-f` `--iidfile` `--invoke` `--label` `--load` `--metadata-file` `--network` `--no-cache` `--no-cache-filter` `--output` `--platform` `--print` `--progress` `--provenance` `--pull` `--push` `--q` `--root` `--sbom` `--secret` `--server-config` `--shm-size` `--ssh` `-t` `--target` `--ulimit`
| `buildx create` |Create a new builder instance | `--append` `--bootstrap` `--buildkitd-flags` `--config` `--driver-opt` `--leave` `--name` `--node` `--platform` `--use`<div>`--driver` : `docker-container` `kubernetes` `remote`
| `buildx du` |Disk usage|`--builder` `--filter` `--verbose`
| `buildx imagetools` |Commands to work on images in registry | `create` : `--append` `--builder` `--dry-run` `-f` `-t` `--progress` <div>`inspect` : `--builder` `--format` `--raw`
| `buildx inspect` |Inspect current builder instance |`--bootstrap` `--builder`
| `buildx install` |Install buildx as a 'docker builder' alias |
| `buildx ls` |Lists all builder instances and the nodes for each instance |
| `buildx prune` |Clears the build cache of the selected builder |`a` `-f` `--builder` `--filter` `--keep-storage` `--verbose`
| `buildx rm` |Removes the specified or current builder |`--all-inactive` `--builder` `-f` `--keep-daemon` `--keep-state`
| `buildx stop` |Stops the specified or current builder |`--builder`
| `buildx uninstall` |Uninstall the 'docker builder' alias |
| `buildx use` |Switches the current builder instance |`--builder` `--default` `--global`
| `buildx version` |Show buildx version information |

## Builder driver
- `docker` driver<div>
Uses the builder that is built into the docker daemon. With this driver, the `--load` flag is implied by default on buildx build. However, building multi-platform images or exporting cache is not currently supported.

- `docker-container` driver<div>
Uses a BuildKit container that will be spawned via docker. With this driver, both building multi-platform images and exporting cache are supported.<div>
Unlike `docker` driver, built images will not automatically appear in `docker images` and `build --load` needs to be used to achieve that.

- `kubernetes` driver<div>
Uses a kubernetes pods. With this driver, you can spin up pods with defined BuildKit container image to build your images.<div>
Unlike `docker` driver, built images will not automatically appear in `docker images` and `build --load` needs to be used to achieve that.

- `remote` driver<div>
Uses a remote instance of buildkitd over an arbitrary connection. With this driver, you manually create and manage instances of buildkit yourself, and configure buildx to point at it.<div>
Unlike `docker` driver, built images will not automatically appear in `docker images` and `build --load` needs to be used to achieve that.

[Set additional driver-specific options (--driver-opt)](https://github.com/docker/buildx/blob/master/docs/reference/buildx_create.md)


!!! quote
    [Github-BuildX](https://github.com/docker/buildx)