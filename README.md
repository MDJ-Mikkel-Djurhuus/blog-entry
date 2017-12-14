![Software Development Evolution](https://blog.heliossolutions.in/wp-content/uploads/2017/05/Software-Development-Evolution-From-Waterfall-to-Agile-to-DevOps.jpg)

# Intro To DevOps

In the wave of new age technologies, the technology industry is witnessing new tools and methods of Software Development, new and old problems. In order to have faster and better quality of development, we must solve our new and old problems. The age old problem of human made errors, and human inefficiency is primarily what DevOps is eliminating<sup>[1](#1)</sup>. As well as removing the nervous and scary feeling of pushing a new release and hoping you remembered to do everything right. Leaving more time for developers to actually develop code, and spend less time on things that can be automated. There are not just many tools for software developers but there are new development methodologies for software development experts to explore areas of software development processes.

Among these processes, DevOps is the next big thing in the IT industry<sup>[2](#2)</sup>. More Software Developers are now choosing DevOps and IT Companies are also training their resources with DevOps management<sup>[3](#3)</sup>. It's reducing the gap between development tools and final IT solutions for enterprises and businesses.

# DevOps
![DevOps](https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Devops-toolchain.svg/512px-Devops-toolchain.svg.png)

DevOps is a software engineering culture and practice, that aims at unifying software development (Dev) and software operation (Ops).

As DevOps is intended to be a cross-functional mode of working, rather than a single DevOps tool there are sets (or "toolchains") of multiple tools. Such DevOps tools are expected to fit into one or more of these categories, reflective of key aspects of the development and delivery process:

- Code — code development and review, source code management tools, code merging
- Build — continuous integration tools, build status
- Test — continuous testing tools that provide feedback on business risks
- Package — artifact repository, application pre-deployment staging
- Release — change management, release approvals, release automation
- Configure — infrastructure configuration and management, Infrastructure as Code tools
- Monitor — applications performance monitoring, end–user experience

The goals of DevOps span the entire delivery pipeline. They include:

- Improved deployment frequency;
- Faster time to market;
- Lower failure rate of new releases;
- Shortened lead time between fixes;
- Faster mean time to recovery (in the event of a new release crashing or otherwise disabling the current system).

## What led DevOps to come into existence
Let’s consider developing software in a traditional way using a Waterfall Model.

![waterfall](https://cdn.edureka.co/blog/wp-content/uploads/2016/10/Waterfall-Model-Devops-Tutorial-Edureka.png)

- In phase 1 – Complete Requirement is gathered and SRS is developed
- In phase 2 – This System is Planned and Designed using the SRS
- In phase 3 – Implementation of the System takes place
- In phase 4 – System is tested and its quality is assured
- In phase 5 – System is deployed to the end users
- In phase 6 – Regular Maintenance of the system is done

### Waterfall Model Challenges
The waterfall method is the traditional method for developing software. It was the primary method of developing during the early days. Even though it has gotten a bad rep these days. It's even gotten so bad some people are swearing you can't develop software with the waterfall method. But if we look back, we can see plenty of software solutions were created in the 80s, 90s and 00s where the waterfall method was the only, or primary method. 

It's not as bad as it's seen as nowadays. But, it's far from perfect as well. In the following diagram, the issues with the waterfall model is shown.

![alt](https://cdn.edureka.co/blog/wp-content/uploads/2016/10/WaterFall-Model-Challenges-DevOps-Tutorial-Edureka-2.png)
Looking at the diagram above, we can clearly see the issues and challenges presented both in development and operations sections of the system's lifetime. When looking at the issues from a developer's point of view, we can ascertain two major challenges:
- Huge time waste during code deployment.
- Time wasted on working on old code, pending code and new code due to the high deployment times.

Operations weren't optimal either. With operations we have 4 major challenges. As seen in the diagram. These are as follows:
- High difficulty of maintaining a near 100% uptime of prod. environment.
- Automation of infrastructure weren't very effective.
- The amount of servers we need to monitor today is way higher than 10-20 years ago, and with this trend, it'll only keep increasing, maybe exponentially.
- Getting feedback and thus being able to diagnose an issue could prove to be near impossible.

![alt](https://cdn.edureka.co/blog/wp-content/uploads/2016/10/Possible-solutions-to-address-the-challenges-faced-with-WaterFall-Model-DevOps-Tutorial-Edureka-1-1.png)

Looking at the diagram above, we can see suggested solutions faced by both operators and developers. These are highlighted in blue. With these suggested solutions we can now set the guidelines for an Ideal Software Development Strategy.

Developer's point of view:
- System where the time from code to release is significantly minimized, ideally removed.
- System where working on the current production code is possible. This could be with very short and well planned sprints.

Operator's point of view:
- System need at least 99% up time.
- Systems and tools to make admin tasks more accessible and easier.
- Monitoring and feedback systems with high efficiency.
- More efficient teamwork between development and operations. 

### How DevOps solves some common issues
Lets focus on how DevOps handles the issues otherwise encountered during deveopment and operations. The table below demonstrates how how DevOps takes care of the issues.

![alt](https://cdn.edureka.co/blog/wp-content/uploads/2016/10/DevOps-Addressing-Dev-Challenges-DevOps-Tutorial-Edureka-1.png)

Delving deeper, we can use the table below.

![alt](https://cdn.edureka.co/blog/wp-content/uploads/2016/10/DevOps-Addressing-Ops-Challenges-DevOps-Tutorial-Edureka-1.png)

At this point, we still haven't given you any tools other than concepts, on how to implement DevOps. It's important to not only make an accepting culture for DevOps, but also teach developers the tools they'll need to properly apply the DevOps functionalities. 
Some of the various tools we'd recommend looking at are GIT, Docker, Chef, Jenkins, Puppet, Selenium, AWS just to name a few. The list goes on, if you choose to search for tools on your own.
Each of these tools help DevOps in various stages: Continuous Development, Continuous Integration, Continuous Testing, Continuous Deployment, Continuous Monitoring.

We need all of these stages to ensure we always deliver a high quality product to the customer, at a very fast rate. You might notice the excessive use of "continuous". That's because it's important for the process to be as smooth as possible. This includes working on current production code, and pushing small changes as soon as they can be verified as properly functional.

Examining the diagram below, it's easier distinguishable in which stage each tool can be used.

![alt](https://cdn.edureka.co/blog/wp-content/uploads/2016/10/DevOps-Tools-DevOps-Tutorial-Edureka-1.png)

Categorized by the different stages of DevOps, we can see which tools belongs where. It's therefore important to firstly know about the stages, and then learn more about the tools afterwards.

The lifecycle of DevOps can be crudely broken down into the following stages:
- Continuous Development
- Continuous Integration
- Continuous Testing
- Continuous Monitoring
- Virtualization and Containerization

All of these stages are simply building blocks upon which to achieve DevOps. 

Now try building your own DevOps solution!

## References
<a name="1">1</a>: https://www.digitaldoughnut.com/articles/2016/june/what-is-devops-and-how-does-it-help-organizations
<a name="2">2</a>: https://trends.google.com/trends/explore?date=all&q=devops
<a name="3">3</a>: https://techbeacon.com/10-companies-killing-it-devops
