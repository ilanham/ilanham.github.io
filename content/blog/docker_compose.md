---
title: 'Docker Compose'
date: '2024-05-13T22:32:02-04:00'
draft: false
tags: ['Docker', 'Compose']
---
Following the post for [Docker Volumes](/docker_volumes), I wanted to cover Docker Compose for two reasons:
1. Some projects that are part of the "modern data stack" use it as an entry point for local testing
  a. A single `docker run` command works well for when Compose is overkill
2. Volumes work a little differently when used with Compose vs. a container started with the `docker run` command

{{< callout type="info" >}}
   A lot of projects recommend deployment on Kubernetes in production, with Compose suggested for local testing.
{{< /callout >}}

## Local Testing

As we explore more of the modern data stack, we'll see most of these products aren't just a single service or daemon; they're a lot of moving parts that work as "*Airflow*" or "*Superset*". Compose is used to logcally separate different functions of an application into different containers. For example, Open Metadata below requires:
- Elasticsearch
- Postgres
- A few copies of it's own Dockerfile (openmetadata-server, openmetadata-ingestion, etc)
The file that specifies these requirements, `docker-compose.yml`, gives you an idea of the config required to run this application.

Here's a sample list of applications in some of the modern data stack that use Compose as an entry point for local testing:
| **Project**     | **Docs Link**                               | **GitHub**                  |
|:----------------|:--------------------------------------------|-----------------------------|
| Airbyte         | [Deploy airbyte - Using Docker Compose][1]  | [{{< icon "github" >}}][2]  |
| Apache Airflow  | [Running Airflow in Docker][3]              | [{{< icon "github" >}}][4]  |
| Apache Superset | [Installation - Using Docker Compose][5]    | [{{< icon "github" >}}][6]  |
| Hydra           | [Run locally][7]                            | [{{< icon "github" >}}][8]  |
| OpenMetadata    | [Local Docker Deployment][9]                | [{{< icon "github" >}}][10] |
| Redash          | [Setting up a Redash Instance - Docker][11] | [{{< icon "github" >}}][12] |

[1]: https://docs.airbyte.com/deploying-airbyte/docker-compose
[2]: https://github.com/airbytehq/airbyte
[3]: https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html
[4]: https://github.com/apache/airflow
[5]: https://superset.apache.org/docs/installation/docker-compose/
[6]: https://github.com/apache/superset
[7]: https://github.com/hydradatabase/hydra/tree/main?tab=readme-ov-file#run-locally
[8]: https://github.com/hydradatabase/hydra
[9]: https://docs.open-metadata.org/v1.4.x/quick-start/local-docker-deployment
[10]: https://github.com/open-metadata/OpenMetadata
[11]: https://redash.io/help/open-source/setup#-Docker
[12]: https://github.com/getredash/redash

In the list above, each of those software projects have provided a compose file, usually in their repo. It's theoretically *possible* to try and run the different components (web/db/cache) in one mega-container. You could also have a bunch of `docker run` commands for each service needed, along with port mapping, volumes/mounts, etc.  
> In my opinion, it's a lot easier to clone a repo and type `docker compose up`.

## Compose Volumes vs. Docker Container Volumes
*Technically* they're the same thing. However, volumes created as part of a `compose up` command usually aren't accessible outside of the network created for the Compose application. When a volume name is specified in a `compose.yml` file, Docker automatically prepends the file with the either `name` field in the compose file, or the folder name the compose file.

For the Open Metadata compose file, I can see a volume named `ingestion-volume-dags`. 

##### Creating Docker Volume `ingestion-volume-dags`
![docker volumes screenshot 1](/images/docker_volumes_01.png)

Even if I already have the volume created from earlier, when I run the `compose up` command for this Compose app, I can see it adds the default name of the compose application to the front of the volumes (image reference).

##### Docker Volumes after running `docker compose up`
![docker volumes screenshot 2](/images/docker_volumes_02.png)

#### Exception to volume naming with Compose
You can specify `external: True` for a volume, and Compose will use an existing volume with all of the data contained there. **But**, Compose understands that volume is managed externally to it's process, and running `compose up` without that volume already present will fail.


## References
Here's a short list of good references I've found on Docker Compose, particularly the tutorial from the "TechWorld with Nana". If you have the time (about an hour), it takes you through a sample project without too much bloat.
- [Docker Compose Overview - Docker Documentation](https://docs.docker.com/compose/)
- [Why use Compose? - Docker Documentation](https://docs.docker.com/compose/intro/features-uses/)
- [YouTube - TechWorld with Nana - Ultimate Docker Compose Tutorial](https://youtu.be/SXwC9fSwct8?si=UdP34H8ffPsBWf9C)