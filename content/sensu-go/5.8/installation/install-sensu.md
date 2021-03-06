---
title: "Installing Sensu"
linkTitle: "Install Sensu"
description: "Sensu Go is available for Linux, Windows (agent and CLI only), macOS (CLI only), and Docker. Read the installation guide to installed the Sensu backend, agent, and sensuctl CLI tool."
weight: 1
version: "5.8"
product: "Sensu Go"
platformContent: true
platforms: ["Ubuntu/Debian", "RHEL/CentOS", "Windows", "macOS", "Docker"]
menu:
  sensu-go-5.8:
    parent: installation
---

Select a platform from the dropdown above.
Sensu Go is available for Linux, Windows (agent and CLI only), macOS (CLI only), and Docker.
See the list of [supported platforms][5] for more information.
Sensu downloads are provided under the [Sensu License][13].

{{< platformBlock "Ubuntu/Debian RHEL/CentOS" >}}

## Install the Sensu backend
The Sensu backend is available for Ubuntu/Debian, RHEL/CentOS, and [Docker](#deploy-sensu-with-docker).
In addition to packages, [binary-only distributions][20] for Linux are available for `amd64`, `arm64`, `armv5`, `armv6`, `armv7`, and `386` architectures.

### 1. Install the package

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian" >}}

#### Ubuntu/Debian
Add the Sensu repository.

{{< highlight shell >}}
curl -s https://packagecloud.io/install/repositories/sensu/stable/script.deb.sh | sudo bash
{{< /highlight >}}

Install the `sensu-go-backend` package.

{{< highlight shell >}}
sudo apt-get install sensu-go-backend
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "RHEL/CentOS" >}}

#### RHEL/CentOS

Add the Sensu repository.

{{< highlight shell >}}
curl -s https://packagecloud.io/install/repositories/sensu/stable/script.rpm.sh | sudo bash
{{< /highlight >}}

Install the `sensu-go-backend` package.

{{< highlight shell >}}
sudo yum install sensu-go-backend
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS" >}}

### 2. Create the configuration file

Copy the example backend config file to the default config path.

{{< highlight shell >}}
sudo cp /usr/share/doc/sensu-go-backend-5.8.0/backend.yml.example /etc/sensu/backend.yml
{{< /highlight >}}

_NOTE: The Sensu backend can be configured using a `/etc/sensu/backend.yml` configuration file or using `sensu-backend start` configuration flags. For more information, see the [backend reference][6]._

### 3. Start the service

Start the backend using a service manager.

{{< highlight shell >}}
sudo service sensu-backend start
{{< /highlight >}}

Verify that the backend is running.

{{< highlight shell >}}
service sensu-backend status
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS" >}}

### Next steps

Now that you've installed the Sensu backend:

- [Install the Sensu agent](#install-the-sensu-agent)
- [Install sensuctl](#install-sensuctl)
- [Sign in to the dashboard][3]

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS Windows" >}}

## Install the Sensu agent
The Sensu agent is available for Ubuntu/Debian, RHEL/CentOS, Windows, and [Docker](#deploy-sensu-with-docker).
In addition to packages, [binary-only distributions][20] for Linux are available for `amd64`, `arm64`, `armv5`, `armv6`, `armv7`, and `386` architectures and for Windows `amd64` and `386` architectures.

### 1. Install the package

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian" >}}

#### Ubuntu/Debian

Add the Sensu repository.

{{< highlight shell >}}
curl -s https://packagecloud.io/install/repositories/sensu/stable/script.deb.sh | sudo bash
{{< /highlight >}}

Install the `sensu-go-agent` package.

{{< highlight shell >}}
sudo apt-get install sensu-go-agent
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "RHEL/CentOS" >}}
#### RHEL/CentOS

Add the Sensu repository.

{{< highlight shell >}}
curl -s https://packagecloud.io/install/repositories/sensu/stable/script.rpm.sh | sudo bash
{{< /highlight >}}

Install the `sensu-go-agent` package.

{{< highlight shell >}}
sudo yum install sensu-go-agent
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Windows" >}}

#### Windows {#windows-agent}

Download the Sensu agent for Windows [`amd64`](https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-go-agent_5.8.0.2380_en-US.x64.msi) or [`386`](https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-go-agent_5.8.0_2380_en-US.x86.msi) architectures.

{{< highlight text >}}
Invoke-WebRequest https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-go-agent_5.8.0.2380_en-US.x64.msi  -OutFile "$env:userprofile\sensu-go-agent_5.8.0.2380_en-US.x64.msi"
{{< /highlight >}}

Start the installation wizard.

{{< highlight text >}}
msiexec.exe /i $env:userprofile\sensu-go-agent_5.8.0.2380_en-US.x64.msi
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS Windows" >}}

### 2. Create the configuration file

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS" >}}

#### Linux

Copy the example agent config file to the default config path.

{{< highlight shell >}}
sudo cp /usr/share/doc/sensu-go-agent-5.8.0/agent.yml.example /etc/sensu/agent.yml
{{< /highlight >}}

_NOTE: The Sensu agent can be configured using a `/etc/sensu/agent.yml` configuration file or using `sensu-agent start` configuration flags. For more information, see the [agent reference][7]._

{{< platformBlockClose >}}

{{< platformBlock "Windows" >}}

#### Windows

Copy the example agent config file from `%ALLUSERSPROFILE%\sensu\config\agent.yml.example` (default: `C:\ProgramData\sensu\config\agent.yml.example`) to `C:\ProgramData\sensu\config\agent.yml`.

{{< highlight text >}}
cp C:\ProgramData\sensu\config\agent.yml.example C:\ProgramData\sensu\config\agent.yml
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS Windows" >}}

### 3. Start the service

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS" >}}

#### Linux

Start the agent using a service manager.

{{< highlight shell >}}
sudo service sensu-agent start
{{< /highlight >}}

Verify that the agent is running.

{{< highlight shell >}}
service sensu-agent status
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Windows" >}}

#### Windows

Change to the `sensu\sensu-agent\bin` directory where you've installed Sensu.

{{< highlight text >}}
cd 'C:\Program Files\sensu\sensu-agent\bin'
{{< /highlight >}}

Run the `sensu-agent` executable.

{{< highlight text >}}
./sensu-agent.exe
{{< /highlight >}}

Run the following command to install and start the agent.

{{< highlight text >}}
./sensu-agent service install
{{< /highlight >}}

Verify that the agent is running.

{{< highlight text >}}
sc.exe query SensuAgent
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian RHEL/CentOS Windows" >}}

### Next steps

Now that you've installed the Sensu agent:

- [Install sensuctl](#install-sensuctl)
- [Create a monitoring event][9]

{{< platformBlockClose >}}

{{< platformBlock "macOS RHEL/CentOS Ubuntu/Debian Windows" >}}

## Install sensuctl
Sensu Go can be configured and used with the sensuctl command line utility.
Sensuctl is available for Ubuntu/Debian, RHEL/CentOS, Windows, and macOS.

### 1. Install the package

{{< platformBlockClose >}}

{{< platformBlock "Ubuntu/Debian" >}}

#### Ubuntu/Debian

Add the Sensu repository.

{{< highlight shell >}}
curl -s https://packagecloud.io/install/repositories/sensu/stable/script.deb.sh | sudo bash
{{< /highlight >}}

Install the `sensu-go-cli` package.

{{< highlight shell >}}
sudo apt-get install sensu-go-cli
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "RHEL/CentOS" >}}

#### RHEL/CentOS

Add the Sensu repository.

{{< highlight shell >}}
curl -s https://packagecloud.io/install/repositories/sensu/stable/script.rpm.sh | sudo bash
{{< /highlight >}}

Install the `sensu-go-cli` package.

{{< highlight shell >}}
sudo yum install sensu-go-cli
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "Windows" >}}

#### Windows

Download [sensuctl for Windows `amd64`](https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-enterprise-go_5.8.0_windows_amd64.tar.gz).

{{< highlight text >}}
Invoke-WebRequest https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-enterprise-go_5.8.0_windows_amd64.tar.gz  -OutFile C:\Users\Administrator\sensu-enterprise-go_5.8.0_windows_amd64.tar.gz
{{< /highlight >}}

Or download [sensuctl for Windows `386`](https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-enterprise-go_5.8.0_windows_386.tar.gz).

{{< highlight text >}}
Invoke-WebRequest https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-enterprise-go_5.8.0_windows_386.tar.gz  -OutFile C:\Users\Administrator\sensu-enterprise-go_5.8.0_windows_386.tar.gz
{{< /highlight >}}

See the [verifying Sensu guide][12] to verify your download using checksums.

{{< platformBlockClose >}}

{{< platformBlock "macOS" >}}

#### macOS

Download the latest release. See the [verifying Sensu guide][12] to verify your download using checksums.

{{< highlight shell >}}
curl -LO https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/5.8.0/sensu-enterprise-go_5.8.0_darwin_amd64.tar.gz
{{< /highlight >}}

Extract the archive.

{{< highlight shell >}}
tar -xvf sensu-enterprise-go_5.8.0_darwin_amd64.tar.gz
{{< /highlight >}}

Copy the executable into your PATH.

{{< highlight shell >}}
sudo cp sensuctl /usr/local/bin/
{{< /highlight >}}

{{< platformBlockClose >}}

{{< platformBlock "macOS RHEL/CentOS Ubuntu/Debian Windows" >}}

### 2. Configure sensuctl

You must configure sensuctl before it can connect to Sensu Go.
Run `sensuctl configure` to get started.

{{< highlight shell >}}
$ sensuctl configure
? Sensu Backend URL: http://127.0.0.1:8080
? Username: admin
? Password: *********
? Namespace: default
? Preferred output format: tabular
{{< /highlight >}}

By default, your Sensu installation comes with a user named `admin` with password `P@ssw0rd!`.
We **strongly** recommended that you change the password immediately.
Once authenticated, you can change the password using the `change-password` command.

{{< highlight shell >}}
$ sensuctl user change-password --interactive
? Current Password:  *********
? Password:          *********
? Confirm:           *********
{{< /highlight >}}

You can change individual values of your sensuctl configuration with the `config` subcommand.

{{< highlight shell >}}
sensuctl config set-namespace default
{{< /highlight >}}

See the [sensuctl reference][4] for more information about using sensuctl.

### 3. Activate enterprise-only features

Sensu Inc. offers support packages for Sensu Go as well as license-activated features designed for enterprises.
To learn more about enterprise features in Sensu Go, [contact the Sensu sales team](https://sensu.io/sales).

If you already have an enterprise license, [log in to your Sensu account](https://account.sensu.io/) and download your license file, then activate your license using sensuctl.

{{< highlight shell >}}
sensuctl create --file sensu_license.json
{{< /highlight >}}

You can use sensuctl to view your license details at any time.

{{< highlight shell >}}
sensuctl license info
{{< /highlight >}}

For more information about enterprise features in Sensu Go, see the [getting started guide](../../getting-started/enterprise).

### Next steps

Now that you've installed sensuctl:

- [See the sensuctl quick reference][4]
- [Create a monitoring event pipeline][10]

{{< platformBlockClose >}}

{{< platformBlock "Docker" >}}
## Deploy Sensu with Docker

Sensu Go can be run via [Docker](https://www.docker.com/) or [rkt](https://coreos.com/rkt) using the [sensu/sensu](https://hub.docker.com/r/sensu/sensu/) image. When running Sensu from Docker there are a couple of things to take into consideration.

The backend requires four exposed ports and persistent storage. This example uses a shared filesystem. Sensu Go is backed by a distributed database, and its storage should be provisioned accordingly.  We recommend local storage or something like Throughput Optimized or Provisioned IOPS EBS if local storage is unavailable.  The exposed ports are:

- 2380: Sensu storage peer listener (only other Sensu backends need access to this port)
- 3000: Sensu dashboard
- 8080: Sensu API (all users need access to this port)
- 8081: Agent API (all agents need access to this port)

We suggest, but do not require, persistent storage for Sensu backends and Sensu agents. The Sensu agent will cache runtime assets locally for each check, and the Sensu backend will cache runtime assets locally for each handler and mutator. This storage should be unique per sensu-backend/sensu-agent process.

### Start a Sensu backend
{{< highlight shell >}}
docker run -v /var/lib/sensu:/var/lib/sensu -d --name sensu-backend -p 2380:2380 \
-p 3000:3000 -p 8080:8080 -p 8081:8081 sensu/sensu:latest sensu-backend start
{{< /highlight >}}

### Start a Sensu agent
In this case, we're starting an agent with the webserver and system subscriptions as an example.
This assumes that the Sensu backend is running on another host named sensu.yourdomain.com.
If you are running these locally on the same system, add `--link sensu-backend` to your Docker arguments, and change the backend URL to `--backend-url ws://sensu-backend:8081`.

{{< highlight shell >}}
docker run -v /var/lib/sensu:/var/lib/sensu -d --name sensu-agent \
sensu/sensu:latest sensu-agent start --backend-url ws://sensu.yourdomain.com:8081 \
--subscriptions webserver,system --cache-dir /var/lib/sensu
{{< /highlight >}}

_NOTE: You can configure the backend and agent log levels by using the `--log-level` flag on either process. Log levels include `panic`, `fatal`, `error`, `warn`, `info`, and `debug`, defaulting to `warn`._

### sensuctl and Docker

It's best to run sensuctl locally and point it at the exposed API port for your the Sensu backend.
The sensuctl utility stores configuration locally, and you'll likely want to persist it across uses.
While it can be run from the docker container, doing so may be problematic.

{{< platformBlockClose >}}

[1]: https://github.com/sensu/sensu-go/releases
[2]: https://github.com/sensu/sensu-go/blob/5.1.1/packaging/files/windows/agent.yml.example
[3]: ../../dashboard/overview
[4]: ../../sensuctl/reference
[5]: ../../installation/platforms
[6]: ../../reference/backend
[7]: ../../reference/agent
[8]: ../../guides/troubleshooting
[9]: ../../guides/monitor-external-resources
[10]: ../../guides/send-slack-alerts
[11]: https://github.com/sensu/sensu-go/blob/master/packaging/files/backend.yml.example
[12]: ../verify
[13]: https://sensu.io/sensu-license
[20]: ../verify
