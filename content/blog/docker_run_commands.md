---
title: 'Docker_run_commands'
date: '2024-09-18T18:27:28-04:00'
draft: false
tags: ['Docker', 'Run', 'Postgres', 'MSSQL']
---

Sometimes I work with Docker every day for a few weeks, but then I don't need to touch it again for months at a time. I don't think my story is unique there - my role isn't in DevOps, so I figure out what I need, save the commands to a note somewhere, and move along.

I wanted to write this article mostly for myself. I'm forgetting where the specific commands are in my Notion space, but I figured I'd post what I use frequently to get a Docker container up and running for my own purposes.

## Pulling the Latest Images

{{< tabs items="MSSQL,PgSQL" defaultIndex="1" >}}

  {{< tab >}}**MSSQL**:`docker pull mcr.microsoft.com/mssql/server:2022-latest`
  I tend to forget the naming convention for Microsoft's container registry.
  [Source](https://learn.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-ver16&tabs=cli&pivots=cs1-bash){{< /tab >}}
  {{< tab >}}**PgSQL**:`docker pull postgres:latest`{{< /tab >}}

{{< /tabs >}}