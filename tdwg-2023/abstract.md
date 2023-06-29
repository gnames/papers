D. Mozzherin, D. Paul

# Preservation Strategies for Biodiversity Data

We are witnessing a fast proliferation of biodiversity informatics projects.
The data accumulated by these initiatives often grows rapidly, even exponentially.
Most of these projects start small and may not have the optimal data architecture in place.
Organizations may lack the necessary expertise and or money to strategically address the care and feeding of this expanding data pile. 
In other cases, individuals with the expertise to address these needs may be present but lack the power or status to take effective actions.
Over time, the data may increase in size to such an extent that handling and preserving it becomes an almost insurmountable problem.
The most common technical challenges include migrating data from one data storage to another, organizing backups, providing fast disaster recovery, and preparing data to be accessible for posterity.
Some sociotechnical and strategic hurdles noted when trying to address data stewardship include funding, data leadership and vision (or lack of), and organizational structure and behavior.
The biodiversity data collected today will be indispensable for future research, and it is our collective responsibility to preserve it for current and future generations.

Some of the most common information loss risk factors are the end of funding, retirement of a researcher, or the departure of a critical researcher or programmer.
More risk factors, hardware disfunction, hurricanes, tornadoes, and severe magnetic storms, can destroy the data carefully collected by large groups of people.

The nature of electronic publishing potentially creates a "Library of Alexandria" where a massive amount of data is used widely, but exists in only one location.
The disappearance of the data in this location leads to a permanent data loss and is an existential threat to the project.

Biodiversity data becomes more valuable over time and should survive for several centuries.
However, SSD (solid-state drive) and HDD (hard disk drive) storage solutions have an expiration date of only a few years.
We propose the following solutions to provide data robustness and resilience:

# Technical tactics

1. Use time-based file storage.

Most of the biodiversity "Big data" are files that are written once and never changed again.
We suggest to separate storage into a read-only part and small read/write sections.
Data from the read/write section migrates to the read-only part often, for example, daily.

2. Use a Copy-On-Write file system, such as ZFS (Zettabyte File System).

ZFS allows incremental backups and much faster data transfer than other file systems.
It allows performing backups using distributed locations (different cities or even countries).
Regular backups can work even with slow internet connections.
ZFS provides real-time data integrity checks and uses powerful tools for data healing.

3. Split data and its backups into smaller chunks.

Dividing backups into 2-8 terabyte chunks allows running backups using cheap hardware.
Assuming that the data is read-only, such data organization always splits the backup into chunks, with hardware costs changing from tens of thousands of dollars to less than two thousand dollars.

4. Split the data even further, where the atomic unit is the size of optical M-disks.

Optical M-disks ([see M-disc on Wikipedia](https://en.wikipedia.org/wiki/M-DISC)) are analogous to Sumerian clay tablets.
Data written on such disks does not deteriorate for hundreds of years.
The storage does not depend on magnetic properties and is impervious to electromagnetic disasters.
Optical disks can be easily and cheaply copied and distributed to libraries worldwide.

# Sociotechnical insights
The above examples of a collective strategy to preserve data epitomize "LOCKSS" (that is, lots of copies keep stuff safe) and make it clear that these copies need to be in varying formats.
Many groups and individuals experience needing to address and plan for preventing the potential data loss situations we describe in this talk at various scales (e.g. an individual's own project, to the Global Biodiversity Information Facility (GBIF)).
Many of us will note we often look to see how others address these data needs.
Recently, The [Species File Group (SFG)](https://speciesfilegroup.org/) did this exercise to evaluate and address our data growth needs (Mozzherin et al 2023).
We recognize and emphasize here the need for a) personnell with the knowledge and skills to build, maintain, and evolve robust strategies and infrastructure to make data accessible and preserve it, b) funding to back the most suitable architectural strategies to do so, and c) those who can address our data architecture needs to have a seat at the leadership table at our organizations.
We encourage our colleagues to evaluate the status of **data leadership** at your organizations (Stack et al 2018, Kalms 2012).
Implementing these suggestions will (at least help to) ensure the survival of the data and accompanying software for hundreds of years to come.

# References
Kalms, B. (2012) Digitisation: A strategic approach for natural history collections
https://www.ala.org.au/wp-content/uploads/2011/10/Digitisation-guide-120326.pdf

Mozzherin D, Pereira H, Yoder M, Paul D. Dealing with an Exponential Data Growth. March 2023 https://github.com/gnames/papers/blob/master/devops-blog-2023/blog.md

Stack C, Stadolnik EM. Data leadership: Defining the expertise your organization needs. November 2018 https://www.spencerstuart.com/research-and-insight/data-leadership-defining-the-expertise-your-organization-needs
