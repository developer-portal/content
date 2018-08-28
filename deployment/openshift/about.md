---
title: OpenShift
subsection: openshift
section: deployment
description: OpenShift
---

# {{page.title}}

OpenShift Origin is a distribution of [Kubernetes](https://kubernetes.io) optimized for continuous application development and multi-tenant deployment. It adds developer and operations-centric tools on top of Kubernetes to enable rapid application development, easy deployment and scaling, and long-term lifecycle maintenance for small and large teams.

Features:

* Easily build applications with integrated service discovery and persistent storage.
* Quickly and easily scale applications to handle periods of increased demand.
  * Support for automatic high availability, load balancing, health checking, and failover.
* Push source code to your Git repository and automatically deploy containerized applications.
* Web console and command-line client for building and monitoring applications.
* Centralized administration and management of an entire stack, team, or organization.
  * Create reusable templates for components of your system, and iteratively deploy them over time.
  * Roll out modifications to software stacks to your entire organization in a controlled fashion.
  * Integration with your existing authentication mechanisms, including LDAP, Active Directory, and public OAuth providers such as GitHub.
* Multi-tenancy support, including team and user isolation of containers, builds, and network communication.
  * Allow developers to run containers securely with fine-grained controls in production.
  * Limit, track, and manage the developers and teams on the platform.
* Integrated Docker registry, automatic edge load balancing, cluster logging, and integrated metrics.

## Start a local OpenShift all-in-one cluster

The quickest way to try out OpenShift on your own computer is using the `oc cluster up` command.
First, install the dependencies. We'll need [Docker](/tools/docker/docker-installation.html) and the `origin-clients` that provides the `oc` binary.

```console
$ sudo dnf install origin-clients docker
```

*Note*: we recommend following the steps in the [Docker installation page](/tools/docker/docker-installation.html#why-cant-i-use-docker-command-as-a-non-root-user-by-default) to add your user to the `docker` group, so that you can run the `docker` command without `sudo`.

Now, let's start our local all-in-one cluster. The command `oc cluster up` takes care of everything:

```console
$ oc cluster up
-- Checking OpenShift client ... OK
-- Checking Docker client ... OK
-- Checking Docker version ... OK
-- Checking for existing OpenShift container ... OK
-- Checking for openshift/origin:v1.3.1 image ...
   Pulling image openshift/origin:v1.3.1
   Pulled 0/3 layers, 3% complete
   Pulled 1/3 layers, 71% complete
   Pulled 2/3 layers, 86% complete
   Pulled 3/3 layers, 100% complete
   Extracting
   Image pull complete
-- Checking Docker daemon configuration ... FAIL
   Error: did not detect an --insecure-registry argument on the Docker daemon
   Solution:

     Ensure that the Docker daemon is running with the following argument:
        --insecure-registry 172.30.0.0/16
```

If you are running a default installation of Docker, you will run into the error above.
That is okay. We will follow the suggestion on screen. The good news is that `oc cluster up` downloaded the Docker image for running OpenShift Origin, so next time we run it, we already have the images offline.

To change the Docker configuration permanently, edit (as the `root` user) the file `/etc/containers/registries.conf` and add `172.30.0.0/16` to the list of `registries` under `[registries.insecure]` category. For example:

```
[registries.insecure]
registries = ['172.30.0.0/16']
```

Then, restart the Docker daemon:

```console
$ sudo systemctl restart docker
```

And let's run `oc cluster up` again:

```console
$ oc cluster up
-- Checking OpenShift client ... OK
-- Checking Docker client ... OK
-- Checking Docker version ... OK
-- Checking for existing OpenShift container ... OK
-- Checking for openshift/origin:v1.3.1 image ... OK
-- Checking Docker daemon configuration ... OK
-- Checking for available ports ... OK
-- Checking type of volume mount ...
   Using nsenter mounter for OpenShift volumes
-- Creating host directories ... OK
-- Finding server IP ...
   Using 10.0.2.15 as the server IP
-- Starting OpenShift container ...
   Creating initial OpenShift configuration
   Starting OpenShift using container 'origin'
   Waiting for API server to start listening
   OpenShift server started
-- Installing registry ... OK
-- Installing router ... OK
-- Importing image streams ... OK
-- Importing templates ... OK
-- Login to server ... OK
-- Creating initial project "myproject" ... OK
-- Server Information ...
   OpenShift server started.
   The server is accessible via web console at:
       https://10.0.2.15:8443

   You are logged in as:
       User:     developer
       Password: developer

   To login as administrator:
       oc login -u system:admin

```

Done! Follow the instructions on the screen to access the OpenShift Origin Web Console.

## Deploying your first application

You can deploy application from the Web Console or from the command line.
As a demo and to test your new environment, you can deploy a sample Ruby application:

```console
$ oc new-app https://github.com/openshift/ruby-hello-world
--> Found Docker image 8a8cd6f (43 hours old) from Docker Hub for "centos/ruby-22-centos7"

    Ruby 2.2
    --------
    Platform for building and running Ruby 2.2 applications

    Tags: builder, ruby, ruby22

    * An image stream will be created as "ruby-22-centos7:latest" that will track the source image
    * A Docker build using source code from https://github.com/openshift/ruby-hello-world will be created
      * The resulting image will be pushed to image stream "ruby-hello-world:latest"
      * Every time "ruby-22-centos7:latest" changes a new build will be triggered
    * This image will be deployed in deployment config "ruby-hello-world"
    * Port 8080 will be load balanced by service "ruby-hello-world"
      * Other containers can access this service through the hostname "ruby-hello-world"

--> Creating resources with label app=ruby-hello-world ...
    imagestream "ruby-22-centos7" created
    imagestream "ruby-hello-world" created
    buildconfig "ruby-hello-world" created
    deploymentconfig "ruby-hello-world" created
    service "ruby-hello-world" created
--> Success
    Build scheduled, use 'oc logs -f bc/ruby-hello-world' to track its progress.
    Run 'oc status' to view your app.
```

You can find more comprehensive walkthroughs in the official documentation under [References](#references).

## Online Developer Preview

An Online offering of the new OpenShift platform based on Docker and Kubernetes is available as a Developer Preview.
For more information visit:

[Online Developer Preview](https://www.openshift.com/devpreview/index.html)

Once you sign up, you can interact with the cluster in the cloud using the same `oc` client tool we installed on the previous section.
For more information, consult the [References](#references) below.

## References

* [Official Documentation](https://docs.openshift.org/latest/welcome/)
    * [OpenShift Web Console Walkthrough](https://docs.openshift.org/latest/getting_started/developers_console.html)
    * [OpenShift Command Line Walkthrough](https://docs.openshift.org/latest/getting_started/developers_cli.html)
* [Upstream GitHub repository](https://github.com/openshift/origin)
* [`oc cluster` command documentation](https://github.com/openshift/origin/blob/master/docs/cluster_up_down.md)
* [OpenShift Online Documentation](https://docs.openshift.com/online/welcome/index.html)
    * [OpenShift Online: Basic Walkthrough](https://docs.openshift.com/online/getting_started/basic_walkthrough.html)
    * [OpenShift Online: Command Line Setup](https://docs.openshift.com/online/cli_reference/get_started_cli.html#basic-setup-and-login)
