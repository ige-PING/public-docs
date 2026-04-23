
# CINES: Adastra

[CINES](https://www.cines.fr)
is the national computing center associated to the french universties
(Centre Informatique National de l’Enseignement Supérieur).

Most information on the Adastra machine can be found
on the [Adastra webpage at CINES](https://dci.dci-gitlab.cines.fr/webextranet/index.html):

The following gives only a brief summary of useful commands and procedures.

## Getting an account

Resources on the machine can be obtained by submitting a project to [eDARI](https://www.edari.fr/).

A new account must be associated to one or more existing projects that received a resource allocation.
Usually, new users join an existing project in IGE.
This is achived by following the procedure described in the
[eDARI portal](https://www.edari.fr/documentation/index.php/Documentation_compl%C3%A8te#ModalitesAccesCalculateurs).
This requires filling forms with several information
(personnal information, IP adresses of connections,...), 
and getting approved by the IGE direction and IT department.

A good practice is to provide at least two IP adresses to secure the connections,
as for instance, the IP address of your personnal desktop,
and at least one secured IGE server (one which is always alive
and which is directly accessible from the outside world).

## Connecting to Adastra

You can only connect from one of the IP address provided in the DARI form.

To connect by SSH through an IGE proxy server,
edit the SSH configuration file (`~/.ssh/config`) to include:

```
Host ige-proxy
     HostName address_of_the_IGE_proxy
     User your_IGE_user_name

Host adastra
     ProxyJump ige-proxy
     HostName adastra.cines.fr
     User your_adastra_user_name
```

You can then connect to Adastra with the command:

```
ssh adastra
```

Then you can share SSH keys (with the proxy)
to avoid giving the password of the proxy at each connection.
But the password of Adastra will have to be provided
explicitly at each connection.

## Workspaces and storage

Before producing data, always check that your project
has got enough resources to store them.
o know about available quota, run the commands:
`myproject -s`.

Quotas are organized according to the workspaces, which differ by:
(i) the volume of available space,
(ii) the security of the data (backups), and
(iii) the type of access to the data.
They can be accessed using environment variables:

  - **$HOMEDIR** : home directory, with **small size** but very **frequent back-up**,
            mainly used to store small precious data, like code, configurations, etc.
            Quota is per user.
  - **$WORKDIR** : workspace available for **bigger data**, but with **no back-up**,
            usually used to make moderate size simulation or run testcases.
            Quota is per project and typical status is full,
            so be careful to avoid blocking other users.
  - **$SCRATCHDIR** : workspace available **big data** (no quota), but only **temporary**
               (erased automatically after one month),
               with very fast access from the processor,
               usually used to put data used and produced by big simulations.
               Good practice is to automatically save final results to STOREDIR
               by a separate postprocessing to avoid automatic deletion.
  - **$STOREDIR** : safe long-term storage of big data, not accessible from computing jobs.
             Be careful of the limited quota on the number of files (inodes),
             thus avoid storing many small files and make archives if necessary (using tar).
             Quota is per project, so check what you do (in size and inodes).

More details are available [here](https://dci.dci-gitlab.cines.fr/webextranet/data_storage_and_transfers/index.html).


## Submitting jobs

Before running computations, always check that your project 
has got enough resources.
To know about available resources, run the command': `myproject -s`.

Details on job submissions can be found here:
[here](https://dci.dci-gitlab.cines.fr/webextranet/user_support/index.html#job-submission).

## Computing on several projects

If your account is associated to several projects,
you can use the resources of each of them.

 - ```myproject -l```will list them.
 - ```myproject -a project``` will load the environment variables for this project.
 - ```myproject -c``` will show you all the path (you need to load a project first).
 - ```myproject -s <project_id>```will show the quota for one project, ```myproject -S``` for all your projects.

