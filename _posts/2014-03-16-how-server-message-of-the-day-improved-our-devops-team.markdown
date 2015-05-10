---
layout: post
title:  "How a server MOTD improved our DevOps team"
date:   2014-03-16 15:54:14
categories: DevOps Infrastructure
blurb: "Our Infrastructure team for the Cloud Control Panel at Rackspace has around ~200 public cloud servers across production, preproduction, staging, and test environments. At a high level our general layout for hosting the Cloud Control Panel includes nodes of several different types. We have load balancers running apache. Web nodes which serve the base content with Django. Javascript served from a cdn (content delivery network). Twisted servers which proxy requests for making calls to Rackspace apis from the frontend. A cluster of Cassandra nodes for managing sessions, preferences, and api cache data."
---

[littlechef]: https://github.com/tobami/littlechef
[littlechef-rackspace]: https://github.com/tildedave/littlechef-rackspace
[alexmeng]: https://github.com/AMeng

The problem
----------
Our Infrastructure team for the Cloud Control Panel at Rackspace has around ~200 public cloud servers across production, preproduction, staging, and test environments. At a high level our general layout for hosting the Cloud Control Panel includes nodes of several different types. We have load balancers running apache. Web nodes which serve the base content with Django. Javascript served from a cdn (content delivery network). Twisted servers which proxy requests for making calls to Rackspace apis from the frontend. A cluster of Cassandra nodes for managing sessions, preferences, and api cache data. All of these nodes are managed and provisioned using [littlechef][littlechef] (chef-solo) combined with [littlechef-rackspace][littlechef-rackspace].

When I first started working on this team we had almost no documentation about how the different types of servers in our environment were setup. When you would SSH onto a node to debug an issue or alert it would take a little extra digging to get started. While we do use chef for configuration of our servers it would take awhile to trace all of the different recipes, where they install services, what scripts you can run, and other useful information about that node. Another issue is making sure that developers at all levels have access to the same information. We want to make sure all, from junior to senior, developers are able to tackle issues that arise.

To that end [Alex Meng][alexmeng] one of the developers on the team took it upon himself during a hackday to improve the process. He did this by generating MOTD's for our servers via chef. Below is a Cassandra node in our test environment. The MOTD is great for immediately being able to start diagnosing issues without having to look at chef for where everything on this node is located.
<img src="/images/reach_cass_motd.png" alt="Example of a Cassandra node MOTD in our test environment. Full picture." />

Load and network information
---------
<img src="/images/reach_cass_motd_1.png" alt="Top of MOTD describing load and network interfaces. Cropped.">

When you first ssh into a node the very top shows some basic **load information** about the node and what **network interfaces** it has available. The network interfaces has proven useful if you have services running on different interfaces and need quick access to that information. For example, on this cassandra node we would access the cassandra cli (cqlsh) from the private network interface.

Node description
---------
<img src="/images/reach_cass_motd_2.png" alt="Middle of MOTD describing project name, node name, environment, hostname, and region. Cropped." />

The next piece of information we add is our **project name** along with the **node name** (cassandra, load balancer, proxy, web), **region** (dfw, ord, syd), **environment** (test, staging, preprod, production) and **hostname** which is blurred out. This helps a person ensure they know they are on the right node. The environment text is large so people are more careful if they are jumping on several boxes, some of which could be production.

Services and location of important information
---------
<img src="/images/reach_cass_motd_3.png" alt="Middle of MOTD describing project name, node name, environment, hostname, and region. Cropped." />

The next section describes the **services running** on the box. This one only happens to be running Cassandra, but some nodes might be running multiple services (in general, our nodes are assigned a single function, but some applications require multiple services on a box). It will also describe where **logs** and **important configuration** files are located on the node. Other things we include sometimes on here are location of **script files** or **cron jobs** that are running on the system. At the end of our MOTD is a link to the **documentation** which describes in detail the role of this node in our architecture.

Conclusion
---------
Our implementation of MOTD's is done via a chef recipe. All of our nodes have a "short_name" attribute which we use to identify which MOTD to use. We store these MOTD's as cookbook files and every node has a MOTD recipe which dumps the correct MOTD onto that node.

In the past year that we have had MOTD's on all of our nodes I realize how important and helpful it is to disperse information about our architecture and make it easier to enable other developers to operate on it. The MOTD provides one key piece for organizing this information immediately when acting on a single node.

