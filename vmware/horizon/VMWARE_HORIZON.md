# Desktop Pools
In Horizon, you create pools of virtual machines and select settings that give all the machines in a pool a common desktop definition. Horizon can then deliver the desktops to end users via Horizon Clients. Horizon can deliver desktops from single-user virtual desktop machines, which can be virtual machines that are managed by vCenter Server, virtual machines that run on another virtualization platform, or physical computers.

You create a desktop pool from one of the following sources:

A virtual machine that runs on a virtualization platform other than vCenter Serverthat supportsHorizon Agent.
Physical desktop PC.
A virtual machine that is hosted on an ESXi host and managed by vCenter Server.
A session-based desktop on an RDS host. For more information about creating desktop pools from an RDS host, see the Setting Up Published Desktops and Applications in Horizon document.

## types of desktop pools
# dedicated pools
one-to-one
users return to the same system every time

# floating pools
one-to-many

# single-user desktop vs RDSH servers
With single-user desktops, each virtual machine allows a single end-user connection at a time. In contrast, with session-based desktops, one RDSH server can accommodate many concurrent user connections.

# instant clone desktop pool
An instant-clone desktop pool is an automated desktop pool. vCenter Server creates the desktop VMs based on the settings that you specify when you create the pool. Instant clones share a virtual disk of the golden image and therefore consume less storage than full VMs. In addition, instant clones share the memory of the golden image.

Before you can deploy a pool of desktops, you must create an optimized golden image, which includes installing and configuring a Windows or Linux operating system in a VM, optimizing the OS, and installing the various VMware agents required for desktop pool deployment.

# entitlements
You configure entitlements to control which remote desktops and applications your users can access. Before users can access remote desktops or applications, they must be entitled to use a desktop or application pool.  In this exercise, we will add an entitlement to an existing desktop pool.

# just in time management platform (JMP)
With VMware's next-gen desktop and application platform leveraging the power of the Just-in-Time Management Platform (or JMP, pronounced "jump"), IT can deliver just-in-time apps to streamline management, reduce costs, and easily maintain compliance. These applications can be accessed by end users with the efficiency and flexibility that business demands.


JUST-IN-TIME APP PROVISIONING WITH VMWARE INSTANT CLONES TECHNOLOGY
JMP technologies include VMware Instant Clones technology together with VMware App Volumes and VMware Dynamic Environment Manager.  This not only dramatically reduces the infrastructure requirements, but also enhances security, allowing you to deliver a brand new personalized desktop and application services instantly to end users every time they log in. Here are just a few of the benefits: 

Provision brand new session hosts in seconds, easily and elastically supporting peak demand.  
Enhance security by shutting down RDSH farms daily/weekly, and easily and quickly spin up brand new hosts.  
Reduce storage and operational costs by up to 70 percent with App Volumes and one-to-many provisioning, which slashes the number of images managed by up to 95 percent.
With updated Cloud Pod Architecture, scale to over 50,000 RDSH farms across 50+ sites with improved failover characteristics, in a fraction of the time of traditional application virtualization models.

# RDSH farms
A farm is a group of Windows Remote Desktop Services (RDS) hosts. You can create published desktops associated with a farm. You can also deliver a published application to many users by creating 

The Horizon Connection Server creates the instant-clone virtual machines based on the parameters that you specify when you create the farm. Instant clones share a virtual disk of a parent VM and therefore consume less storage than full virtual machines. In addition, instant clones share the memory of a parent VM and are created using the vmFork technology.

When you create an application pool or a published desktop pool, you must specify one and only one farm. The RDS hosts in a farm can host published desktops, applications, or both. A farm can support at most one published desktop pool, but it can support multiple application pools. A farm can support both types of pools simultaneously

# rdsh has better load balancing
# easy to enable


