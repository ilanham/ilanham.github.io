---
title: 'Docker Run Commands'
date: '2024-09-18T18:27:28-04:00'
draft: false
tags: ['Docker', 'Run', 'Postgres', 'MSSQL']
---

Sometimes I work with Docker every day for a few weeks, but then I don't need to touch it again for months at a time. I don't think my story is unique there - my role isn't in DevOps, so I figure out what I need, save the commands to a note somewhere, and move along.

Most often I use Microsoft SQL Server at work and PostgreSQL on personal projects, so I tend to keep copies of those commands in different notes. I want to collect my most frequently used ones here.

All of the volume mounts here are meant to be used with Named Volumes. I've tried to move all of my stuff away from bind-mounts. Check out my post on [Named Volumes]({{< ref "docker_volumes.md" >}}), or take a look at the [Docker Docs](https://docs.docker.com/engine/storage/volumes/) for more details.

## Pulling the Latest Images

{{< tabs items="PgSQL, MSSQL" defaultIndex="0" >}}

  {{< tab >}}
  ```bash
  docker pull postgres:latest
  ```
  {{< /tab >}}
  {{< tab >}}
  ```bash
  docker pull mcr.microsoft.com/mssql/server:2022-latest
  ```

  I tend to forget the naming convention for Microsoft's container registry. You can substitute the `2022` for a different version offered by Microsoft.  

  [Source](https://learn.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-ver16&tabs=cli&pivots=cs1-bash)
  {{< /tab >}}

{{< /tabs >}}

## Run Commands

{{< tabs items="PgSQL, MSSQL" defaultIndex="0" >}}

  {{< tab >}}
  ```bash
  docker run --name pg \
    -p 5432:5432 \
    -e POSTGRES_PASSWORD=<secret> \
    -v pgdata:/var/lib/postgresql/data \
    -d postgres
  ```
  [Source](https://www.docker.com/blog/how-to-use-the-postgres-docker-official-image/#1-Environment-variables)
  {{< /tab >}}
  {{< tab >}}
  ```bash
  docker run --name SQL22 \
      -p 1433:1433 \
      -e "ACCEPT_EULA=Y" \
      -e "MSSQL_SA_PASSWORD=<secret>" \
      -v mssql_data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2022-latest
  ```
  [Source](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-docker-container-configure)
  {{< /tab >}}

{{< /tabs >}}