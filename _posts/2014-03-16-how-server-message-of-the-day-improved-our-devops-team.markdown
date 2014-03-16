---
layout: post
title:  "How server Message of the Day (MOTD) improved our DevOps team."
date:   2014-03-16 15:54:14
categories: DevOps Infrastructure
---

Our Infrastructure team for the Cloud Control Panel at Rackspace has around ~200 public cloud servers across production, preproduction, staging, and test environments. At a high level our general layout for hosting the Cloud Control Panel includes load balancers running apache, web nodes which serve the base content with django, javascript served from cdn (content delivery network), twisted servers which proxy requests for making calls to Rackspace apis from the frontend, and a cluster of Cassandra nodes for managing sessions, preferences, and api cache data. We manage provisioning and mangement of our servers with [littlechef][littlechef] (chef-solo) combined with [littlechef-rackspace][littlechef-rackspace].

When I first started working on this team we had almost no documentation about how the different types of servers in our environment were setup. When you would SSH onto a node to debug an issue or alert it would take a little extra digging to get started. While we do use chef for configuration of our servers it would take awhile to trace all of the different recipes, where they install services, what scripts you can run, and other useful information about that node. One of our developers ([Alex Meng][alexmeng]) for a hackday took it upon himself to help our process a bit more by generating useful MOTD's for our servers via chef. Here is an example:

<img src="http://b7cc86bc05773bcecd41-4057535a55b255b6cbfb486a61b5692d.r49.cf1.rackcdn.com/reach_cass_motd.png" alt="Example of a Cassandra node MOTD in our test environment">

This is an example of a Cassandra node in our environment. The MOTD is great for immediately being able to start diagnosing issues without having to look at chef for where everything on this node is located. A couple of things I want to highlight about this picture.

When you first ssh into a node the very top shows some basic **load information** about the node and what **network interfaces** it has available. The next piece of information we add is our **project name** along with the **node name** (cassandra, load balancer, proxy, web), **region** (dfw, ord, syd), **environment** (test, staging, preprod, production) and **hostname** which is blurred out. This helps a person ensure they know they are on the right node and the environment is large so people are more careful if they need to debug a production box.

The next section describes the **services running** on the box. This one only happens to be running Cassandra, but some nodes might be running multiple services (in general, our nodes are assigned a single function, but some applications require multiple services on a box). It will also describe where **logs** and **important configuration** files are located on the node. Other things we include sometimes on here are location of **script files** or **cron jobs** that are running on the system.

The final piece of information we leave in the MOTD is a link to the **documentation** which describes in detail the role of this node in our architecture.

In the past year that we have had MOTD's on all of our nodes I realize how important and helpful it is to disperse information about our architecture and make it easier to enable other developers to operate on it. The MOTD provides one key piece for organizing this information immediately when acting on a single node.

[littlechef]: https://github.com/tobami/littlechef
[littlechef-rackspace]: https://github.com/tildedave/littlechef-rackspace
[alexmeng]: https://github.com/AMeng
