---
date: "2019-05-24T00:00:00Z"
title: A simple Docker walkthrough
---
According to [the official docker page](https://www.docker.com/resources/what-container) -

>A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.


Docker helps programmers to deliver their software in a reliable and consistent manner. Since it has everything required to the application it is designed for, it alleviates the problem of "It works on my PC, don't know why it doesn't work on yours!"

Getting started with Docker is as simple as-

1. Download docker community edition for your system from the [official docker download link](https://www.docker.com/products/docker-desktop).
2. Install docker on your system.
3. Run Docker on the system.

Now if you open up the terminal and type-
{{< highlight shell >}}
docker version
{{< / highlight >}}

You should see something like this-
{{< highlight shell >}}
Client: Docker Engine - Community
 Version:           18.09.2
 API version:       1.39
 Go version:        go1.10.8
 Git commit:        6247962
 Built:             Sun Feb 10 04:12:39 2019
 OS/Arch:           darwin/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.2
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.6
  Git commit:       6247962
  Built:            Sun Feb 10 04:13:06 2019
  OS/Arch:          linux/amd64
  Experimental:     false
{{< / highlight >}}

We have successfully installed docker onto our system. But now, how do we use this wonderful tool for the benefits of a _containerised application_?

Let's begin with something really simple.
One of the starting points of writing a Dockerised application is writing something called a Dockerfile.
The Dockerfile defines how the containerised application is to be built.

We shall be calling our application docker-example.
Go to the terminal and create a new project directory and then navigate to it-

{{< highlight shell >}}
mkdir ~/docker-example
cd docker-example
{{< / highlight >}}


Suppose we have a program called application.py, a Python3 application that we need to containerise.

{{< highlight shell >}}
cat application.py
{{< / highlight >}}


{{< highlight python >}}
import platform
print(platform.system())
print(platform.release())
print("Hello! This message is from a container!")
{{< / highlight >}}

The output when the program is run from the computer directly looks like this-
{{< highlight shell >}}
python3 application.py
Darwin
18.5.0
Hello! This message is from a container!
{{< / highlight >}}

Open up your favorite text editor and create a file called Dockerfile. You can [read more about Dockerfiles here](https://docs.docker.com/engine/reference/builder/).
{{< highlight shell >}}
touch Dockerfile
{{< / highlight >}}

Now edit the contents of the file to this-

{{< highlight docker >}}
FROM python:3

WORKDIR /usr/src/app

COPY . .

CMD [ "python", "application.py" ]
{{< / highlight >}}


Once the file is saved, drop back into the terminal and type this command-
{{< highlight shell >}}
docker build -t docker-example .
{{< / highlight >}}

The -t is being used here to _tag_ the image to the name _docker_example_.

Docker will download the latest [python 3 base docker image](https://hub.docker.com/_/python) first, if it does not exist on your computer.

After the build is done, you should see an image like this-

{{< highlight shell >}}
Successfully built 403f70f033e0
Successfully tagged docker-example:latest
{{< / highlight >}}

The 403f70f033e0 here is the container id that is built. If we had not specified the tag, it would have only displayed the container id and not the tag.
In that scenario, tagging could be done by-
{{< highlight shell >}}
docker tag 403f70f033e0 docker-example
{{< / highlight >}}


This means our containerised application is ready and we can now run it by the following command-
{{< highlight shell >}}
docker run docker-example
{{< / highlight >}}


We should be seeing an output similar to this-
{{< highlight shell >}}
Linux
4.9.125-linuxkit
Hello! This message is from a container!
{{< / highlight >}}

Note that the output says Linux even though my system is actually Darwin(MacOS). This means our application is running from the docker container and we can start availing all the benefits listed in the first paragraph of this article.

And there we have it! A really simple walkthrough to Docker. If you managed to follow all the steps correctly, you have successfully run your first containerised application.

You can find my repository with all the files required for this walkthrough at [this sample github repo](https://github.com/shreyashag/docker-example).

Docker is really much much more than this though, and I hope to follow up this article with more detailed articles on this subject.
