D. Mozzherin, D. Paul

# Preservation Strategies for Biodiversity Data

We are witnessing a fast proliferation of biodiversity informatics projects.
The data accumulated by them is also growing rapidly, often exponentially.
Most of these projects start small and do not give much thought to the data architecture.
However, over time, the data may increase in size to such an extent that handling and preserving it becomes an almost insurmountable problem.
The most common challenges include migrating data from one data storage to another, organizing backups, providing fast disaster recovery, and preparing data to be accessible for posterity.
The biodiversity data collected today will be indispensable for future research, and it is our responsibility to preserve it for next generations.

Some of the most common risk factors are the end of funding, retirement of a researcher, or the departure of a critical researcher or programmer.
Hardware dysfunction, hurricanes, tornadoes, and severe magnetic storms are risks that could destroy the data carefully collected by large groups of people.

The nature of electronic publishing creates a "Bibliotheca Alexandrina effect" where a massive amount of data is used widely, but exists in only one location.
The disappearance of the data in this location leads to a permanent data loss and is an estitential threat to the project.

Biodiversity data becomes more valuable over time and should survive for several centuries.
However, SSD and HDD storage solutions have an expiration date of only a few years.
We propose the following solutions to provide data robustness and resilience:

1. Use time-based file storage.

Most of the biodiversity "Big data" are files that are written once and never changed again.
We suggest to separate storage into a read-only part and small read/write sections.
Data from the read/write section migrates to the read-only part often, for example, daily.

2. Use a Copy-On-Write file system, such as ZFS.

ZFS allows incremental backups and much faster data transfer than other file systems.
It allows performing backups using distributed locations (different cities or even countries).
Regular backups can work even with slow internet connections.
ZFS provides real-time data integrity checks and uses powerful tools for data healing.

3. Split data and its backups into smaller chunks.

Dividing backups into 2-8 terabyte chunks allows running backups using cheap hardware.
Assuming that the data is read-only, such data organization always splits the backup into chunks, with hardware costs changing from tens of thousands of dollars to less than two thousand dollars.

4. Split the data even further, where the atomic unit is the size of optical M-disks.

Optical M-disks are analogous to Sumerian clay tablets.
Data written on such disks does not deteriorate for hundreds of years.
The storage does not depend on magnetic properties and is impervious to electromagnetic disasters.
Optical disks can be easily and cheaply copied and distributed to libraries worldwide.

Implementing these suggestions will ensure the survival of the data and accompanying software for hundreds of years to come.
