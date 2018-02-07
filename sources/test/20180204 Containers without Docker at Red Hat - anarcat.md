Toggle navigation [![anarcat](/favicon.png)](anarc.at/) 

*   [Bio](anarc.at/../../#top)
*   [Blog](anarc.at/../#top)
*   [Contact](anarc.at/../../contact/)

Containers without Docker at Red Hat
====================================

> This is one part of my coverage of KubeCon Austin 2017. Other articles include:
> 
> *   [An overview of KubeCon + CloudNativeCon](anarc.at/../2017-12-13-kubecon-overview/)
> *   Docker without Docker at Red Hat (this article)
> *   [Demystifying Container Runtimes](anarc.at/../2017-12-20-demystifying-container-runtimes/)

The Docker (now [Moby](https://mobyproject.org/)) project has done a lot to popularize containers in recent years. Along the way, though, it has generated concerns about its concentration of functionality into a single, monolithic system under the control of a single daemon running with root privileges: `dockerd`. Those concerns were reflected in a [talk](https://kccncna17.sched.com/event/CU8j/cri-o-hosted-by-daniel-walsh-red-hat) by Dan Walsh, head of the container team at Red Hat, at [KubeCon + CloudNativeCon](http://events.linuxfoundation.org/events/kubecon-and-cloudnativecon-north-america). Walsh spoke about the work the container team is doing to replace Docker with a set of smaller, interoperable components. His rallying cry is "no big fat daemons" as he finds them to be contrary to the venerated Unix philosophy.

The quest to modularize Docker
------------------------------

As we saw in an [earlier article](anarc.at/../2017-12-20-demystifying-container-runtimes/), the basic set of container operations is not that complicated: you need to pull a container image, create a container from the image, and start it. On top of that, you need to be able to build images and push them to a registry. Most people still use Docker for all of those steps but, as it turns out, Docker isn't the only name in town anymore: an early alternative was `rkt`, which led to the creation of various standards like CRI (runtime), OCI (image), and CNI (networking) that allow backends like [CRI-O](http://cri-o.io/) or Docker to interoperate with, for example, [Kubernetes](https://kubernetes.io/).

These standards led Red Hat to create a set of "core utils" like the CRI-O runtime that implements the parts of the standards that Kubernetes needs. But Red Hat's [OpenShift](https://www.openshift.com/) project needs more than what Kubernetes provides. Developers will want to be able to build containers and push them to the registry. Those operations need a whole different bag of tricks.

It turns out that there are multiple tools to build containers right now. Apart from Docker itself, a [session](https://kccncna17.sched.com/event/CU6B/building-better-containers-a-survey-of-container-build-tools-i-michael-ducy-chef) from Michael Ducy of Sysdig reviewed eight image builders, and that's probably not all of them. Ducy identified the ideal build tool as one that would create a minimal image in a reproducible way. A minimal image is one where there is no operating system, only the application and its essential dependencies. Ducy identified [Distroless](https://github.com/GoogleCloudPlatform/distroless), [Smith](https://github.com/oracle/smith), and [Source-to-Image](https://github.com/openshift/source-to-image) as good tools to build minimal images, which he called "micro-containers".

A reproducible container is one that you can build multiple times and always get the same result. For that, Ducy said you have to use a "declarative" approach (as opposed to "imperative"), which is understandable given that he comes from the Chef configuration-management world. He gave the examples of [Ansible Container](https://www.ansible.com/ansible-container), [Habitat](https://www.habitat.sh/), [nixos-container](https://nixos.org/nixos/manual/#ch-containers), and Smith (yes, again) as being good approaches, provided you were familiar with their domain-specific languages. He added that Habitat ships its own supervisor in its containers, which may be superfluous if you already have an external one, like systemd, Docker, or Kubernetes. To complete the list, we should mention the new [BuildKit](https://github.com/moby/buildkit) from Docker and [Buildah](https://github.com/projectatomic/buildah), which is part of Red Hat's [Project Atomic](https://www.projectatomic.io/).

Building containers with Buildah
--------------------------------

![[Buildah
logo]](https://raw.githubusercontent.com/projectatomic/buildah/master/logos/buildah-logomark_large.png "Buildah logo") Buildah's name apparently comes from Walsh's colorful [Boston accent](https://en.wikipedia.org/wiki/Boston_accent); the Boston theme permeates the branding of the tool: the logo, for example, is a Boston terrier dog (seen at right). This project takes a different approach from Ducy's decree: instead of enforcing a declarative configuration-management approach to containers, why not build simple tools that can be used by your favorite configuration-management tool? If you want to use regular command-line commands like `cp` (instead of Docker's custom `COPY` directive, for example), you can. But you can also use Ansible or Puppet, OS-specific or language-specific installers like APT or pip, or whatever other system to provision the content of your containers. This is what building a container looks like with regular shell commands and simply using `make` to install a binary inside the container:

```
    # pull a base image, equivalent to a Dockerfile's FROM command
    buildah from redhat

    # mount the base image to work on it
    crt=$(buildah mount)
    cp foo $crt
    make install DESTDIR=$crt

    # then make a snapshot
    buildah commit

```

An interesting thing with this approach is that, since you reuse normal build tools from the host environment, you can build really minimal images because you don't need to install all the dependencies in the image. Usually, when building a container image, the target application build dependencies need to be installed within the container. For example, building from source usually requires a compiler toolchain in the container, because it is not meant to access the host environment. A lot of containers will also ship basic Unix tools like `ps` or `bash` which are not actually necessary in a micro-container. Developers often forget to (or simply can't) remove some dependencies from the built containers; that common practice creates unnecessary overhead and attack surface.

The modular approach of Buildah means you can run at least parts of the build as non-root: the `mount` command still needs the `CAP_SYS_ADMIN` capability, but there is an [issue](https://github.com/projectatomic/buildah/issues/171) open to resolve this. However, Buildah [shares](https://github.com/projectatomic/buildah/issues/158) the same [limitation](https://github.com/moby/moby/issues/27886#issuecomment-281278525) as Docker in that it can't build containers inside containers. For Docker, you need to run the container in "privileged" mode, which is not possible in certain environments (like [GitLab Continuous Integration](https://about.gitlab.com/features/gitlab-ci-cd/), for example) and, even when it is possible, the configuration is [messy](https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/) at best.

The manual commit step allows fine-grained control over when to create container snapshots. While in a Dockerfile every line creates a new snapshot, with Buildah commit checkpoints are explicitly chosen, which reduces unnecessary snapshots and saves disk space. This is useful to isolate sensitive material like private keys or passwords which sometimes mistakenly end up in public images as well.

While Docker builds non-standard, Docker-specific images, Buildah produces standard OCI images among [other output formats](https://github.com/projectatomic/buildah/blob/master/docs/buildah-push.md). For backward compatibility, it has a command called `build-using-dockerfile` or [`buildah bud`](https://github.com/projectatomic/buildah/blob/master/docs/buildah-bud.md) that parses normal Dockerfiles. Buildah has a `enter` command to inspect images from the inside directly and a `run` command to start containers on the fly. It does all the work without any "fat daemon" running in the background and uses standard tools like `runc`.

Ducy's criticism of Buildah was that it was not declarative, which made it less reproducible. When allowing shell commands anything can happen: for example, a shell script might download arbitrary binaries, without any way of subsequently retracing where those come from. Shell command effects may vary according to the environment. In contrast to shell-based tools, configuration-management systems like Puppet or Chef are designed to "converge" over a final configuration that is more reliable, at least in theory: in practice you can call shell commands from configuration-management systems. Walsh, however, argued that existing configuration management _can_ be used on top of Buildah, but it doesn't _force_ users down that path. This fits well with the classic "separation" principle of the Unix philosophy ("mechanism not policy").

At this point, Buildah is in beta and Red Hat is working on integrating it into OpenShift. I have tested Buildah while writing this article and, short of some documentation issues, it generally works reliably. It could use some polishing in error handling, but it is definitely a great asset to add to your container toolbox.

Replacing the rest of the Docker command-line
---------------------------------------------

Walsh continued his presentation by giving an overview of another project that Red Hat is working on, tentatively called [libpod](https://github.com/projectatomic/libpod). The name derives from a "pod" in Kubernetes, which is a way to group containers inside a host, to share namespaces, for example.

Libpod includes the `kpod` command to inspect and manipulate container storage directly. Walsh explained this can be useful if, for example, `dockerd` hangs or if a Kubernetes cluster crashes. `kpod` is basically an independent re-implementation of the `docker` command-line tool. There is a command to list running containers (`kpod ps`) or images (`kpod images`). In fact, there is a [translation cheat sheet](https://github.com/projectatomic/libpod/blob/master/transfer.md#development-transfer) documenting all Docker commands with a `kpod` equivalent.

One of the nice things with the modular approach is that when you run a container with `kpod run`, the container is directly started as a subprocess of the current shell, instead of a subprocess of `dockerd`. In theory, this allows running containers directly from systemd, removing the duplicate work `dockerd` is doing. It enables things like [socket-activated containers](http://0pointer.de/blog/projects/socket-activated-containers.html), which is something that is [not straightforward](https://legacy-developer.atlassian.com/blog/2015/03/docker-systemd-socket-activation/) to do with Docker, or [even with Kubernetes](https://github.com/kubernetes/kubernetes/issues/484) right now. In my experiments, however, I have found that containers started with `kpod` lack some fundamental functionality, namely networking (!), although there is an [issue in progress](https://github.com/projectatomic/libpod/issues/129) to complete that implementation.

A final command we haven't covered is `push`. While the above commands provide a good process for working with local containers, they don't cover remote registries, which allow developers to actively collaborate on application packaging. Registries are also an essential part of a continuous-deployment framework. This is where the [skopeo](https://github.com/projectatomic/skopeo) project comes in. Skopeo is another Atomic project that "performs various operations on container images and image repositories", according to the `README` file. It was originally designed to inspect the contents of container registries without actually downloading the sometimes voluminous images as `docker pull` does. Docker [refused patches](https://github.com/moby/moby/pull/14258) to support inspection, suggesting the creation of a separate tool, which led to Skopeo. After `pull`, `push` was the logical next step and Skopeo can now do a bunch of other things like copying and converting images between registries without having to store a copy locally. Because this functionality was useful to other projects as well, a lot of the Skopeo code now lives in a reusable library called [containers/image](https://github.com/containers/image). That library is in turn used by [Pivotal](https://pivotal.io/), Google's [container-diff](https://github.com/GoogleCloudPlatform/container-diff), `kpod push`, and `buildah push`.

`kpod` is not directly tied to Kubernetes, so the name might change in the future — especially since Red Hat legal has not cleared the name yet. (In fact, just as this article was going to "press", the name was changed to [`podman`](https://github.com/projectatomic/libpod/blob/master/docs/podman.1.md).) The team wants to implement more "pod-level" commands which would allow operations on multiple containers, a bit like what [`docker compose`](https://docs.docker.com/compose/overview/#compose-documentation) might do. But at that level, a better tool might be [Kompose](http://kompose.io/) which can execute [Compose YAML files](https://docs.docker.com/compose/compose-file/) into a Kubernetes cluster. Some Docker commands (like [`swarm`](https://docs.docker.com/engine/swarm/)) will never be implemented, on purpose, as they are best left for Kubernetes itself to handle.

It seems that the effort to modularize Docker that started a few years ago is finally bearing fruit. While, at this point, `kpod` is under heavy development and probably should not be used in production, the design of those different tools is certainly interesting; a lot of it is ready for development environments. Right now, the only way to install libpod is to compile it from source, but we should expect packages coming out for your favorite distribution eventually.

> _This article [first appeared](https://lwn.net/Articles/741841/) in the [Linux Weekly News](http://lwn.net/)._

*   [Demystifying container runtimes](anarc.at/../2017-12-20-demystifying-container-runtimes/)
*   [Blog.](anarc.at/../)
*   [An overview of KubeCon + CloudNativeCon](anarc.at/../2017-12-13-kubecon-overview/)

[Add a comment](anarc.at/ikiwiki.cgi?do=comment&page=blog%2F2017-12-20-docker-without-docker)

Created Wednesday, à midi, December 20th, 2017. [Edited au milieu de la matinée de Monday, January 8th, 2018.](http://source.anarcat.wiki.orangeseeds.org/?p=source.git;a=history;f=blog/2017-12-20-docker-without-docker.mdwn)

Toggle navigation

*   [Tags](anarc.at/#)
    *   [conference](anarc.at/../../tag/conference/)
    *   [containers](anarc.at/../../tag/containers/)
    *   [debian-planet](anarc.at/../../tag/debian-planet/)
    *   [docker](anarc.at/../../tag/docker/)
    *   [kubernetes](anarc.at/../../tag/kubernetes/)
    *   [lwn](anarc.at/../../tag/lwn/)
*   [Links](anarc.at/#)
    *   [2017-12-13-kubecon-overview](anarc.at/../2017-12-13-kubecon-overview/)
    *   [2017-12-20-demystifying-container-runtimes](anarc.at/../2017-12-20-demystifying-container-runtimes/)
    *   [2018-01-27-summary-2017-work](anarc.at/../2018-01-27-summary-2017-work/)
*   [Meta](anarc.at/#)
    *   [Edit](anarc.at/ikiwiki.cgi?do=edit&page=blog%2F2017-12-20-docker-without-docker)
    *   [Timeline](anarc.at/../../recentchanges/)
    *   [History](http://source.anarcat.wiki.orangeseeds.org/?p=source.git;a=history;f=blog/2017-12-20-docker-without-docker.mdwn)
    *   [Prefs](anarc.at/ikiwiki.cgi?do=prefs)
    *   [Branchable](anarc.at/ikiwiki.cgi?do=branchable)
    *   [poster un commentaire](anarc.at/ikiwiki.cgi?do=comment&page=blog%2F2017-12-20-docker-without-docker)

Copyleft © 2002-2016 The Anarcat [CC-BY-SA](anarc.at/meta/license). Powered by [ikiwiki](http://ikiwiki.info/). [Valid (X)HTML 5](http://validator.w3.org/check?uri=referer).