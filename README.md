# Enterprise-grade File sharing deployment guide


## Abstract
I'll cover all the aspects (I can think of), please feel free to open issues and make it better

## Considerations

1. Open-source
 - Yes. by ALL means.

2. Operating system
 - CentOS
 - Ubuntu
 - Arch
 
3. Connectivity
 - On premise
 - air-gapped networks
 
4. High availability
- The solution must be tolerant to a failure of underlying physical hardware and/or software
- Users must not experience service level degragation during that time

5. Load balancing
 - Whenever possible, load should be balanced between participating cluster members
 - to increase performance
 - handle upgrade flows
 - look nice on presentations to managers

6. Development environment
 - Although we intend to install the service on top of other clouds, 
   our developers must be able to debug all of the components on their laptop


## Sample architectures
  - all in one
  - containerzied
  - mini HA
  - Full HA
  
## Architectural overview
The deployment can be described as a matrix of layers per nodes installation

### Layers

#### Load layer - Bind9 / HAProxy / Nginx
This layer conatians services that are meant to handle large load from the clients,
help prevent floods and denial-of-service attacks and provide ACL of some sort. 

#### Application layer - Apache / Nginx
This layer contains the web application itself, and act as a frontend for users accessing the service.

#### Database layer - MySQL + Galera / PostgreSQL
This layer contains the database for the application, actual files will not be stored here,
only transactions committed by the application, will be stored here,
                                                                               #
#### Intermediate layer - Consul / HAProxy / Redis / Memcached / K8s / Swarm
This layer contains all the volatile services that contribute to the overall application health and performance,
such as cache, service discovery and so on

#### Infrastructure Layer - Telegraf / Journald / logrotate / beats / cloud-init


## Deployment
  - Product
    - owncloud vs. seafile
  - VIP - Virtual IP / Velocity Impacted Path
  - service discovery method
  - performance vs. complexity
    - nginx
    - bind9 

