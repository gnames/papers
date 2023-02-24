D. Mozzherin, H. Pereira, M. Yoder, (may be Debbie?)

The Species File Group (SFG) at INHS is involved in several global projects that provide services for the biodiversity community.
Three main projects are TaxonWorks, Catalogue of Life and GlobalNames.
TaxonWorks is a powerful editorial workbench for taxonomists and collection managers.
The Catalogue of Life editorial work provides data for the global checklist of known species.
Global Names provides tools for parsing, detecting, and resolving scientific names.

TaxonWorks is the cornerstone project of our group.
It was developed by combining the expertise of three precursor taxonomic editorial tools, Species Files, MX, and 3i.
All of them were developed by members of the SFG group.
The TaxonWorks project is maturing quickly and experiencing exponential growth of data.
As of February 2023, TaxonWorks already contained 2.7 TB of data and 6 million files.

However, managing such large amounts of data has become increasingly difficult for us.
It would take 5 days to transfer data from one computer to another, and making incremental backups would take up to 3 hours.
We felt that the group is at risk of losing the integrity of the accumulated data in case of human error, hardware failure, or a disaster at the data center.
To address these issues, we decided to rethink our strategy and provide technical solutions that would allow us to experience a 10-100 fold increase in efficiency.

One significant problem we encountered was the lack of a full-time system administrator.
Currently, we run about 50 remotely accessed services on more than 10 computers.
Without a designated system administrator we need a system that would allow to maintain high day-to-day availability with minimal effort.

Our immediate goals were the following.
To achieve fast and reliable integrity checks of all the data.
To be able to efficiently and reliably transfer TaxonWorks files to a new production server or a backup.
To distribute backups to several off-site locations to mitigate risks of technological or natural disasters.
To achieve fast disaster recovery in case of such misfortunes.
To ensure high availability of day-to-day operations with minimal involvement in system maintenance.

To achieve these goals, the group acquired dedicated storage hardware, namely DELL's ME1400 for production and MD4012 for backup.
Both systems, in their current configuration, allow them to scale their storage up to 70TB.
In addition to hardware, we also needed a new software solution to be able to reliably work with more and more data.
We chose to use the Open ZFS file system for all our production and backup needs.

ZFS provided us with several very important features.
The file system checks integrity of every stored byte, and can detect and repare even the smallest data corruption resulted from cosmic rays or a disk failure.
The speed of data transfer increased more than ten-fold, allowing us to copy 2.7TB in about 4 hours.
The speed of incremental backups increased hundred-fold, allowing us to send incremental changes in a matter of seconds.
Fast incremental backups now allow us to sync data remotely quickly, even if the remote place has slow internet.

To achieve high availability of our services and still keep system management within working hours and with only 1-2 hours/week system administration involvement, we automated our workflow.
We used Ansible infrastructure automation tool and Kubernetes computer cluster management as our two main software components.
We used Git revision control system to distribute Ansible environment between system administrators.
With most of the infrastructure construction tasks automated, the group saved time and resources.

A Kubernetes cluster automates the maintenance of our services and ensures high availability for our users.
It monitors the services and restores them automatically if they break.
Kubernetes also has self-healing capabilities, so if the system itself experiences issues, it fixes them automatically.

For over five years, we have utilized Kubernetes and Ansible, which have significantly streamlined the deployment of our services.
This automated workflow has provided us with a flexible and user-friendly environment to make changes in our system, freeing up our time for projects development.

Our group generates exclusively Open Sourced projects, and for system software we also prefer such solutions.
All described above tools are released as Open Source.

Now that we have achieved our goals, we plan to increase data safety in the future.
One major problem with computer technology is its volatility.
Storage hardware solutions degrade over time and may become technologically obsolete.
As a result, it is essential to actively transfer data to keep it alive.
The data about species and taxonomy are critical for future generations.
So, how can we preserve this perishable data for science?

Printing press technology gave us access to biodiversity information published 250 years ago by Carl Linnaeus.
The taxonomic data we accumulate today needs to be accessible 250 years from now.
However, the massive scale of today's data makes it impossible to publish as dead tree books.
Therefore, we are developing workflows and approaches that we hope will enable collections and taxonomists' work to be accessible centuries later.
