<img src="https://imgur.com/download/iJ2Hr2C"/>

# Cloud Native Buildpacks 101

This demo project showcases how to use [Cloud Native Buildpacks](https://buildpacks.io/)
to build secure Docker images, using a single command.

Buildpacks provide a higher-level abstraction for building apps compared to Dockerfiles.
Cloud Native Buildpacks embrace modern container standards, such as the OCI image format.
They take advantage of the latest capabilities of these standards,
such as cross-repository blob mounting and image layer "rebasing" on Docker API v2 registries.

See the [announcement about Cloud Native Buildpacks](https://content.pivotal.io/blog/peace-of-mind-for-developers-and-operators-buildpacks-is-now-a-cncf-project-welcome-cloud-native-buildpacks).

## Prerequisites

You need the following components to build your first Docker image with Cloud Native Buildpacks:
 - a running Docker daemon
 - the CLI `pack`, responsible for building & packaging your app

Install `pack` using these [instructions](https://github.com/buildpack/pack/releases).

## Build your first image using Cloud Native Buildpacks

The Docker image will contain a single Java app using Spring Boot.
Thanks to `pack`, we're going to build this app and package it as a Docker image:
```shell
$ pack build cloudnativebuildpacks101
```

You don't even need a JDK nor Maven to build this app. The `java-buildpack` is automatically
downloaded: it is responsible for building the app, and making sure the resulting Docker
image is secure and ready to deploy.

You are now ready to run the app using Docker:
```shell
$ docker run --rm -p 8080:8080/tcp cloudnativebuildpacks101
```

Just go to http://localhost:8080 to see the result.

## See it live

### Deploy to Kubernetes

In case you already have a Kubernetes cluster, you may want to deploy this app to see it
in action. Feel free to use this Kubernetes descriptor:
```shell
$ kubectl apply -f deploy/k8s.yml
```

### Deploy to Cloud Foundry Application Runtime (PAS)

You can also deploy Docker images to Cloud Foundry:
```shell
$ cf push -f deploy/docker-on-cloudfoundry.yml
```

In the end, don't forget that Spring Boot apps are meant to be deployed
in a PaaS like Cloud Foundry, since it's way easier than maintaining Docker images:
```shell
$ cf push -f deploy/cloudfoundry.yml
```

**It's up to you to choose among all these deployment options the one
that better suits you.**

## Contribute

Contributions are always welcome!

Feel free to open issues & send PR.

## License

Copyright &copy; 2018 Pivotal Software, Inc.

This project is licensed under the [Apache Software License version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
