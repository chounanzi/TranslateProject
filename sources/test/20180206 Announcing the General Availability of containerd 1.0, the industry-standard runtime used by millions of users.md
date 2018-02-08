[![](https://blog.docker.com/wp-content/themes/whale_roots/assets/img/brand-full.svg)][1] [![](https://blog.docker.com/wp-content/themes/whale_roots/assets/img/brand.svg)][2]

*   [What is Docker?][3]
*   [Product][4]
*   [Get Docker][5]
    *   [For Desktops][6]
    *   [Mac][7]
    *   [Windows][8]
    *   [For Cloud Providers][9]
    *   [AWS][10]
    *   [Azure][11]
    *   [For Servers][12]
    *   [Windows Server][13]
    *   [CentOS][14]
    *   [Debian][15]
    *   [Fedora][16]
    *   [Oracle Linux][17]
    *   [RHEL][18]
    *   [SLES][19]
    *   [Ubuntu][20]
*   [Docs][21]
*   [Community][22]

*   [Create Docker ID][23]
*   [Sign In][24]

[![](https://blog.docker.com/wp-content/themes/whale_roots/assets/img/brand-full.svg)][25]

*   [Create Docker ID][26]
*   [Sign In][27]

*   [What is Docker?][28]
*   [Product][29]
*   [Get Docker][30]
    *   [For Desktops][31]
    *   [Mac][32]
    *   [Windows][33]
    *   [For Cloud Providers][34]
    *   [AWS][35]
    *   [Azure][36]
    *   [For Servers][37]
    *   [Windows Server][38]
    *   [CentOS][39]
    *   [Debian][40]
    *   [Fedora][41]
    *   [Oracle Linux][42]
    *   [RHEL][43]
    *   [SLES][44]
    *   [Ubuntu][45]
*   [Docs][46]
*   [Community][47]

Search

*   [All][48]
*   [Engineering][49]
*   [Curated][50]
*   [Docker Weekly][51]

![Patrick Chanezon](https://i0.wp.com/blog.docker.com/wp-content/uploads/Y8svq43n.jpg?fit=156%2C156&ssl=1)

Announcing the General Availability of containerd 1.0, the industry-standard runtime used by millions of users
==============================================================================================================

By [Patrick Chanezon][52] December 5, 2017

[

Twitter0





][53][

Linkedin0





][54][

Reddit0





][55][

Google+0





][56][

Facebook0





][57][

HackerNews





][58][

E-mail0





][59]

[cloud native computing foundation][60], [cncf][61], [container runtime][62], [containerd][63], [CRI-containerd][64], [gRPC][65], [Kubernetes][66]

Today, we’re pleased to announce that containerd (pronounced Con-Tay-Ner-D), an industry-standard runtime for building container solutions, has reached its 1.0 milestone. containerd has already been deployed in millions of systems in production today, making it the most widely adopted runtime and an essential upstream component of the Docker platform.

Built to address the needs of modern container platforms like Docker and orchestration systems like Kubernetes, containerd ensures users have a consistent dev to ops experience. From [Docker’s initial announcement][67] last year that it was spinning out its core runtime to [its donation to the CNCF][68] in March 2017, the containerd project has experienced significant growth and progress over the past 12 months. .

Within both the Docker and Kubernetes communities, there has been a significant uptick in contributions from independents and CNCF member companies alike including Docker, Google, NTT, IBM, Microsoft, AWS, ZTE, Huawei and ZJU. Similarly, the maintainers have been working to add key functionality to containerd.The initial containerd donation provided everything users need to ensure a seamless container experience including methods for:

*   transferring container images,
*   container execution and supervision,
*   low-level local storage and network interfaces and
*   the ability to work on both Linux, Windows and other platforms.

Additional work has been done to add even more powerful capabilities to containerd including a:

*   Complete storage and distribution system that supports both OCI and Docker image formats and
*   Robust events system
*   More sophisticated snapshot model to manage container filesystems

These changes helped the team build out a smaller interface for the snapshotters, while still fulfilling the requirements needed from things like a builder. It also reduces the amount of code needed, making it much easier to maintain in the long run.

The containerd 1.0 milestone comes after several months testing both the alpha and version versions, which enabled the  team to implement many performance improvements. Some of these,improvements include the creation of a stress testing system, improvements in garbage collection and shim memory usage.

“In 2017 key functionality has been added containerd to address the needs of modern container platforms like Docker and orchestration systems like Kubernetes,” said Michael Crosby, Maintainer for containerd and engineer at Docker. “Since our announcement in December, we have been progressing the design of the project with the goal of making it easily embeddable in higher level systems to provide core container capabilities. We will continue to work with the community to create a runtime that’s lightweight yet powerful, balancing new functionality with the desire for code that is easy to support and maintain.”

containerd is already being used by Kubernetes for its[ cri-containerd project][69], which enables users to run Kubernetes clusters using containerd as the underlying runtime. containerd is also an essential upstream component of the Docker platform and is currently used by millions of end users. There is also strong alignment with other CNCF projects: containerd exposes an API using [gRPC][70] and exposes metrics in the [Prometheus][71] format. containerd also fully leverages the Open Container Initiative (OCI) runtime, image format specifications and OCI reference implementation ([runC][72]), and will pursue OCI certification when it is available.

Key Milestones in the progress to 1.0 include:

![containerd 1.0](https://i2.wp.com/blog.docker.com/wp-content/uploads/4f8d8c4a-6233-4d96-a0a2-77ed345bf42b-5.jpg?resize=720%2C405&ssl=1)

Notable containerd facts and figures:

*   1994 GitHub stars, 401 forks
*   108 contributors
*   8 maintainers from independents and and member companies alike including Docker, Google, IBM, ZTE and ZJU .
*   3030+ commits, 26 releases

Availability and Resources

To participate in containerd: [github.com/containerd/containerd][73]

*   Getting Started with containerd: [http://mobyproject.org/blog/2017/08/15/containerd-getting-started/][74]
*   Roadmap: [https://github.com/containerd/containerd/blob/master/ROADMAP.md][75]
*   Scope table: [https://github.com/containerd/containerd#scope][76]
*   Architecture document: [https://github.com/containerd/containerd/blob/master/design/architecture.md][77]
*   APIs: [https://github.com/containerd/containerd/tree/master/api/][78].
*   Learn more about containerd at KubeCon by attending Justin Cormack’s [LinuxKit & Kubernetes talk at Austin Docker Meetup][79], Patrick Chanezon’s [Moby session][80] [Phil Estes’ session][81] or the [containerd salon][82]

[Announcing the GA of @containerd 1.0, the industry-standard runtime used by millions of users][83]

[Click To Tweet][84]

[cloud native computing foundation][85], [cncf][86], [container runtime][87], [containerd][88], [CRI-containerd][89], [gRPC][90], [Kubernetes][91]

---

![Patrick Chanezon](https://i0.wp.com/blog.docker.com/wp-content/uploads/Y8svq43n.jpg?fit=156%2C156&ssl=1)

Announcing the General Availability of containerd 1.0, the industry-standard runtime used by millions of users
==============================================================================================================

By [Patrick Chanezon][92]

Patrick Chanezon is member of technical staff at Docker Inc. He helps to build Docker, an open platform for distributed applications for developers and sysadmins. Software developer and storyteller, he spent 10 years building platforms at Netscape & Sun, then 10 years evangelizing platforms at Google, VMware & Microsoft. His main professional interest is in building and kickstarting the network effect for these wondrous two-sided markets called Platforms. He has worked on platforms for Portals, Ads, Commerce, Social, Web, Distributed Apps, and Cloud. More information is available at [linkedin.com/in/chanezon][93].

Patrick tweets at [@chanezon][94].

---

### Leave a Reply

[Click here to cancel reply.][95]

 

 Notify me of follow-up comments by email.

 Notify me of new posts by email.

### Related Posts

*   [![](http://blog.docker.io/wp-content/uploads/2013/09/9738496064_095ce31d6e_h-1024x293.jpg)][96]
    
    #### [Docker Workshop at Geekdom San Francisco by Rackspace][97]
    
    By [Victor Coisne][98]October 4, 2013 [CoreOS][99], [demo][100], [docker][101], [MailGun][102], [rackspace][103]
*   [![](https://blog.docker.com/media/j_10nFQk-300x300.jpeg)][104]
    
    #### [Guest Post: Notes on the First Docker Advisory Board Meeting][105]
    
    By [Ben Golub][106]November 4, 2014 [dgab][107], [docker][108]
*   [![Adam Herzog](https://i0.wp.com/blog.docker.com/wp-content/uploads/02c512e-1.jpg?fit=156%2C156&ssl=1)][109]
    
    #### [Docker Online Meetups #28 and #29: Production-Ready Docker Swarm and Docker Networking is Now GA][110]
    
    By [Adam Herzog][111]November 13, 2015 [cluster][112], [Cluster Management][113], [clustering][114], [docker][115], [Docker Cluster][116], [docker networking][117], [docker swarm][118], [multi-host networking][119], [networking][120]

### Get the Latest Docker News by Email

Docker Weekly is a newsletter with the latest content on Docker and the agenda for the upcoming weeks.

Subscribe to our newsletter

*   [What is Docker][121]
*   [What is a Container][122]
*   [Use Cases][123]
*   [Customers][124]
*   [For Government][125]
*   [For IT Pros][126]
*   [Find a Partner][127]
*   [Become a Partner][128]
*   [About Docker][129]
*   [Management][130]
*   [Press & News][131]
*   [Careers][132]

*   [Product][133]
*   [Pricing][134]
*   [Community Edition][135]
*   [Enterprise Edition][136]
*   [Docker Cloud][137]
*   [Docker Store][138]

*   [Documentation][139]
*   [Blog][140]
*   [RSS Feed][141]
*   [Training][142]
*   [Knowledge Base][143]
*   [Resources][144]

*   [Community][145]
*   [Open Source][146]
*   [Forums][147]
*   [Docker Captains][148]
*   [Scholarships][149]
*   [Community News][150]

*   [Status][151]
*   [Security][152]
*   [Legal][153]
*   [Contact][154]

Copyright © 2017 Docker Inc. All rights reserved.

*   [Twitter][155]
*   [Youtube][156]
*   [Google][157]
*   [Github][158]
*   [Linkedin][159]
*   [Facebook][160]
*   [Reddit][161]
*   [Slideshare][162]

---

via: [https://blog.docker.com/2017/12/cncf-containerd-1-0-ga-announcement/][163]

作者: [null][164] 选题者: [@chounanzi][165] 译者: [译者ID][166] 校对: [校对者ID][167]

本文由 [LCTT][168] 原创编译，[Linux中国][169] 荣誉推出

[1]: https://blog.docker.com/
[2]: https://blog.docker.com/
[3]: https://www.docker.com/what-docker
[4]: https://www.docker.com/get-docker
[5]: https://www.docker.com/get-docker
[6]: https://blog.docker.com/#
[7]: https://www.docker.com/docker-mac
[8]: https://www.docker.com/docker-windows
[9]: https://blog.docker.com/#
[10]: https://www.docker.com/docker-aws
[11]: https://www.docker.com/docker-microsoft-azure
[12]: https://blog.docker.com/#
[13]: https://www.docker.com/docker-windows-server
[14]: https://www.docker.com/docker-centos
[15]: https://www.docker.com/docker-debian
[16]: https://www.docker.com/docker-fedora
[17]: https://www.docker.com/docker-oracle-linux
[18]: https://www.docker.com/docker-rhel
[19]: https://www.docker.com/docker-sles
[20]: https://www.docker.com/docker-ubuntu
[21]: https://docs.docker.com/
[22]: https://www.docker.com/docker-community
[23]: https://cloud.docker.com/
[24]: https://cloud.docker.com/login
[25]: https://blog.docker.com/
[26]: https://cloud.docker.com/
[27]: https://cloud.docker.com/login
[28]: https://www.docker.com/what-docker
[29]: https://www.docker.com/get-docker
[30]: https://www.docker.com/get-docker
[31]: https://blog.docker.com/#
[32]: https://www.docker.com/docker-mac
[33]: https://www.docker.com/docker-windows
[34]: https://blog.docker.com/#
[35]: https://www.docker.com/docker-aws
[36]: https://www.docker.com/docker-microsoft-azure
[37]: https://blog.docker.com/#
[38]: https://www.docker.com/docker-windows-server
[39]: https://www.docker.com/docker-centos
[40]: https://www.docker.com/docker-debian
[41]: https://www.docker.com/docker-fedora
[42]: https://www.docker.com/docker-oracle-linux
[43]: https://www.docker.com/docker-rhel
[44]: https://www.docker.com/docker-sles
[45]: https://www.docker.com/docker-ubuntu
[46]: https://docs.docker.com/
[47]: https://www.docker.com/docker-community
[48]: https://blog.docker.com/
[49]: https://blog.docker.com/category/engineering
[50]: https://blog.docker.com/curated/
[51]: https://blog.docker.com/docker-weekly-archives/
[52]: https://blog.docker.com/author/chanezon/
[53]: https://blog.docker.com/javascript:void(0)
[54]: http://www.linkedin.com/shareArticle?mini=true&url=https://blog.docker.com/2017/12/cncf-containerd-1-0-ga-announcement/&title=Announcing%20the%20General%20Availability%20of%20containerd%201.0%2C%20the%20industry-standard%20runtime%20used%20by%20millions%20of%20users&summary=Today, we’re pleased to announce that containerd (pronounced Con-Tay-Ner-D), an industry-standard runtime for building container solutions, has reached its 1.0 milestone. containerd has already been deployed in millions of systems in production today, making it the most widely adopted runtime and an essential upstream component of the Docker platform. Built ...
[55]: http://www.reddit.com/submit?url=https://blog.docker.com/2017/12/cncf-containerd-1-0-ga-announcement/&title=Announcing%20the%20General%20Availability%20of%20containerd%201.0%2C%20the%20industry-standard%20runtime%20used%20by%20millions%20of%20users
[56]: https://plus.google.com/share?url=https://blog.docker.com/2017/12/cncf-containerd-1-0-ga-announcement/
[57]: https://blog.docker.com/javascript:void(0)
[58]: http://news.ycombinator.com/submitlink?u=https://blog.docker.com/2017/12/cncf-containerd-1-0-ga-announcement/&t=Announcing%20the%20General%20Availability%20of%20containerd%201.0%2C%20the%20industry-standard%20runtime%20used%20by%20millions%20of%20users
[59]: https://blog.docker.com/javascript:void(0)
[60]: https://blog.docker.com/tag/cloud-native-computing-foundation/
[61]: https://blog.docker.com/tag/cncf/
[62]: https://blog.docker.com/tag/container-runtime/
[63]: https://blog.docker.com/tag/containerd/
[64]: https://blog.docker.com/tag/cri-containerd/
[65]: https://blog.docker.com/tag/grpc/
[66]: https://blog.docker.com/tag/kubernetes/
[67]: https://blog.docker.com/2016/12/introducing-containerd/
[68]: https://blog.docker.com/2017/03/docker-donates-containerd-to-cncf/
[69]: http://blog.kubernetes.io/2017/11/containerd-container-runtime-options-kubernetes.html
[70]: http://www.grpc.io/
[71]: https://prometheus.io/
[72]: https://github.com/opencontainers/runc
[73]: http://github.com/containerd/containerd
[74]: http://mobyproject.org/blog/2017/08/15/containerd-getting-started/
[75]: https://github.com/docker/containerd/blob/master/ROADMAP.md
[76]: https://github.com/docker/containerd#scope
[77]: https://github.com/docker/containerd/blob/master/design/architecture.md
[78]: https://github.com/docker/containerd/tree/master/api/
[79]: https://www.meetup.com/Docker-Austin/events/245536895/
[80]: http://sched.co/CU6G
[81]: https://kccncna17.sched.com/event/CU6g/embedding-the-containerd-runtime-for-fun-and-profit-i-phil-estes-ibm
[82]: https://kccncna17.sched.com/event/Cx9k/containerd-salon-hosted-by-derek-mcgowan-docker-lantao-liu-google
[83]: https://twitter.com/share?text=Announcing+the+GA+of+%40containerd+1.0%2C+the+industry-standard+runtime+used+by+millions+of+users&via=docker&related=docker&url=http://dockr.ly/2ArQe3G
[84]: https://twitter.com/share?text=Announcing+the+GA+of+%40containerd+1.0%2C+the+industry-standard+runtime+used+by+millions+of+users&via=docker&related=docker&url=http://dockr.ly/2ArQe3G
[85]: https://blog.docker.com/tag/cloud-native-computing-foundation/
[86]: https://blog.docker.com/tag/cncf/
[87]: https://blog.docker.com/tag/container-runtime/
[88]: https://blog.docker.com/tag/containerd/
[89]: https://blog.docker.com/tag/cri-containerd/
[90]: https://blog.docker.com/tag/grpc/
[91]: https://blog.docker.com/tag/kubernetes/
[92]: https://blog.docker.com/author/chanezon/
[93]: https://www.linkedin.com/in/chanezon
[94]: https://twitter.com/chanezon
[95]: https://blog.docker.com/2017/12/cncf-containerd-1-0-ga-announcement/#respond
[96]: https://blog.docker.com/2013/10/docker-workshop-at-geekdom-san-francisco-by-rackspace/
[97]: https://blog.docker.com/2013/10/docker-workshop-at-geekdom-san-francisco-by-rackspace/ "Docker Workshop at Geekdom San Francisco by Rackspace"
[98]: https://blog.docker.com/author/victor_c/
[99]: https://blog.docker.com/tag/coreos/
[100]: https://blog.docker.com/tag/demo/
[101]: https://blog.docker.com/tag/docker/
[102]: https://blog.docker.com/tag/mailgun/
[103]: https://blog.docker.com/tag/rackspace/
[104]: https://blog.docker.com/2014/11/guest-post-notes-on-the-first-docker-advisory-board-meeting/
[105]: https://blog.docker.com/2014/11/guest-post-notes-on-the-first-docker-advisory-board-meeting/ "Guest Post: Notes on the First Docker Advisory Board Meeting"
[106]: https://blog.docker.com/author/ben/
[107]: https://blog.docker.com/tag/dgab/
[108]: https://blog.docker.com/tag/docker/
[109]: https://blog.docker.com/2015/11/docker-online-meetups-docker-swarm-docker-networking/
[110]: https://blog.docker.com/2015/11/docker-online-meetups-docker-swarm-docker-networking/ "Docker Online Meetups #28 and #29: Production-Ready Docker Swarm and Docker Networking is Now GA"
[111]: https://blog.docker.com/author/adam/
[112]: https://blog.docker.com/tag/cluster/
[113]: https://blog.docker.com/tag/cluster-management/
[114]: https://blog.docker.com/tag/clustering/
[115]: https://blog.docker.com/tag/docker/
[116]: https://blog.docker.com/tag/docker-cluster/
[117]: https://blog.docker.com/tag/docker-networking/
[118]: https://blog.docker.com/tag/docker-swarm/
[119]: https://blog.docker.com/tag/multi-host-networking/
[120]: https://blog.docker.com/tag/networking/
[121]: https://www.docker.com/what-docker
[122]: https://www.docker.com/what-container
[123]: https://www.docker.com/use-cases
[124]: https://www.docker.com/customers
[125]: https://www.docker.com/industry-government
[126]: https://www.docker.com/itpro
[127]: https://www.docker.com/find-partner
[128]: https://www.docker.com/partners/partner-program
[129]: https://www.docker.com/company
[130]: https://www.docker.com/company/management
[131]: https://www.docker.com/company/news-and-press
[132]: https://www.docker.com/careers
[133]: https://www.docker.com/get-docker
[134]: https://www.docker.com/pricing
[135]: https://www.docker.com/community-edition
[136]: https://www.docker.com/enterprise-edition
[137]: https://cloud.docker.com/
[138]: https://store.docker.com/
[139]: https://docs.docker.com/
[140]: https://blog.docker.com/
[141]: https://blog.docker.com/feed/
[142]: https://training.docker.com/
[143]: https://success.docker.com/kbase
[144]: https://www.docker.com/products/resources
[145]: https://www.docker.com/docker-community
[146]: https://www.docker.com/technologies/overview
[147]: https://forums.docker.com/
[148]: https://www.docker.com/community/docker-captains
[149]: https://www.docker.com/docker-community/scholarships
[150]: https://blog.docker.com/curated/
[151]: http://status.docker.com/
[152]: https://docker.com/docker-security
[153]: https://www.docker.com/legal
[154]: https://www.docker.com/company/contact
[155]: http://twitter.com/docker
[156]: http://www.youtube.com/user/dockerrun
[157]: https://plus.google.com/u/0/communities/108146856671494713993
[158]: https://github.com/docker/docker
[159]: https://www.linkedin.com/company/docker
[160]: https://www.facebook.com/docker.run
[161]: http://www.reddit.com/r/docker
[162]: http://www.slideshare.net/docker
[163]: https://blog.docker.com/2017/12/cncf-containerd-1-0-ga-announcement/
[164]: undefined
[165]: https://github.com/chounanzi
[166]: https://github.com/译者ID
[167]: https://github.com/校对者ID
[168]: https://github.com/LCTT/TranslateProject
[169]: https://linux.cn/