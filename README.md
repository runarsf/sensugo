# SensuGo docker(-compose)

### Getting started

```bash
git clone https://github.com/runarsf/sensugo.git
cd sensugo
cp -r default-data/ data
docker-compose up -d
```

### Sensu Go admin credentials

- Default username: `admin`
- Default password: `secret`
- Create a new file called `.env` in the root of the repository:
```bash
SENSU_BACKEND_CLUSTER_ADMIN_USERNAME=username
SENSU_BACKEND_CLUSTER_ADMIN_PASSWORD=password
```

### [Creating a read-only user](https://docs.sensu.io/sensu-go/latest/guides/create-read-only-user/)

```bash
docker exec -it sensuctl bash
./bin/sensuctl user create bob --password='password' --groups=ops
./bin/sensuctl cluster-role create global-event-reader --verb=get,list --resource=events
./bin/sensuctl cluster-role-binding create ops-event-reader --cluster-role=global-event-reader --group=ops
```

<details>
  <summary>Resources</summary>

- https://docs.sensu.io/sensu-go/5.15/reference/backend/#configuration-via-environment-variables
- https://github.com/sensu/sandbox/tree/master/sensu-go-docker
- https://github.com/sensu/sensu-go/blob/master/docker-compose.yaml
- https://docs.sensu.io/sensu-go/latest/installation/install-sensu/#3-initialize
- https://docs.sensu.io/sensu-go/latest/installation/install-sensu/
- Consider using `from:` to build the base image in addition to the Dockerfile
  * https://github.com/docker/compose/issues/210#issuecomment-49578942
- https://stackoverflow.com/a/48651071
- https://docs.sensu.io/sensu-go/latest/guides/create-read-only-user/
- This container does *not* work on 32-bit systems.
</details>