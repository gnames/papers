Species File Group at INHS participates in several global projects to provide services for biodiversity community.
Three main such projects are TaxonWorks, a powerful editorial desktop for taxonomists, Global Names, tools for parsing, detecting, resolving scientific names, the Catalogue of Life, a global checklist of known species.

TaxonWorks is the group's corenerstone service. It was developed using combined expertese of three precursor taxonomic editorial tools Species Files, MX and 3i, all developed by members of SFG group.
The project matures fast and experiences exponential grouth of data.
In 2020 the images, and documents stored by Taxonworks occupied 0.3TB of data.
In 2021 is was already 1.3TB, in 2022 - 2.4 TB.
In February of 2023 there were already 2.7 TB of data and 6 million file.

Quite soon we discowered that dealing with so much data is becoming increasingly difficult.
Moving data from one computer to another was taking 5 days.
Making incremental backups was taking up to 3 hours.
We felt that we are increasingly at risk of loosing integrity of the accumulated data in case of a human mistake, hardware failure, or a disaster at the data center.
As a result we decided to rethink our strategy and provide technical solutions that would allow us to experience 10-100 fold.

Another significant problem we encountered, was the lack of full-time system administrator in the group.
We run about 50 remotely accessed services on more than 10 computers currently and we need a system that allows us to maintain high day to day availability of our systems.

Our immediate goals were:

- Fast and reliable integrity check of all the data.
- Fast and reliable transfer of the data to a new production server or a backup.
- Ability to distribute backup to several off-site location to amiliorate risks of technological or natural disasters.
- Achieving fast disaster recovery in case of such disasters.
- High availability of day to day operations with minimal envolvement in system maintenance.

On February 20th our group achieved these goals by rebuilding our systems and incorporating new hardware.
In this blog we want to share our experience and methodologies of the process.

First we decided to acquire dedicated storage hardware. We chose DELLs ME1400 for production and MD4012 for backup.
Both systems in their current configuration allow us to scale our storage up to 70TB.
However in addition to hardware we also needed a new software solution to be able to reliably work with more and more data.

We chose to us ZFS filesystem for all our production and backup needs.
ZFS was originally developed by Sun Solaris and is used by data centers to operate on multi-petabyte scale1.
This file system provided us with several very important for us features.

- every stored byte is accounted in metadata, and even smallest change in data due to cosmic rays or a disk failure can be detected and repaired.
- the speed of data transfer increased hundred-fold and allowing us to copy 2.7TB in about 4 hours.
- the speed of incremental backups increased thousand-fold allowing to send incremental changes in a matter of seconds.
- fast incremental backups now allows us to sync data remotely fast even if remote place has 100Bits/sec slow internet.

We organize remote backups in such way, that the backup is self-sufficient and can be installed in a matter of hours on a off the shelf PC to serve TaxonWorks and GN data temporary.

To achieve high availability of our services and still keeping system management within working hours and with only 1-2 hours/week system administration involvement we automated our services.
Two main software components we use are Ansible infrastructure automation tool and Kubernetes computer cluster management.
We use Git revision control system to distribute Ansible environment between system administrators.
This environment allows us to destroy and rebuild Kubernetes computer claster automatically.
With most of our infrastructure construction tasks automated saves us massive amount of time and resources.

Kubernetes cluster is a system that automates the maintenance of all our services and provides high availability for our users.
It monitors the services, and when it detects that they are broken, it automatically restores them back.
Kubernetes also has self-healing capabilities, and if something goes bad with the system itself the system fixes the problem automatically.

We Kubernetes and Ansible for more than 5 years now and they helped us dramatically to ease deployment of our services.
This automated workflow provides us very flexible and friendly environment to make changes in our system and frees our time for development of our projects.

Now, that we achieved our goals, we have plans to further increase data safety in the future.

One big problem with computer technology is its volatility.
Storage hardware solutions degrade with time and/or become technologically obsolete.
As a result only through atvie involvement of transferring data we accumulated so far we can keep it alive.
However, information about species, taxonomy would be really important for the future generations.
How can we preserve this perishable data for science?

Printing press technology gave us access to biological data published by 250 years ago by Carl Linnaeus.
The taxomic data we accumulate today need to be shared 250 years in the future.
However the massive scale of todays data does not allow it to be published as dead tree books anymore.
We are developing workflows and approaches that, will, we hope, allow to make work of collections and taxonomists be availabe a few centuries later.



