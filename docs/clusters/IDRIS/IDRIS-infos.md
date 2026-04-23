
# IDRIS: Jean-Zay

[IDRIS](http://www.idris.fr/docs/idris/missions)
is the national computing center of the CNRS.

Most information on the Jean-Zay machine can be found
on the [Jean-Zay webpage at IDRIS](http://www.idris.fr/docs/jean-zay/nouvel-utilisateur/).

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
and which is directly accessible fro the outside world).

## Connecting to Jean-Zay

You can only connect from one of the IP address provided to IDRIS.

To connect by SSH through an IGE proxy server,
edit the SSH configuration file (`~/.ssh/config`) to include:

```
Host ige-proxy
     HostName address_of_the_IGE_proxy
     User your_IGE_user_name

Host jean-zay
     ProxyJump ige-proxy
     HostName jean-zay.idris.fr
     User your_IDRIS_user_name
```

You can then connect to Jean-Zay with the command:

```
ssh jean-zay
```

Then you can share SSH keys (with the proxy and jean-zay)
to avoid giving your password at each connection.

## Workspaces and storage

Before producing data, always check that your project
has got enough resources to store them.
To know about available quota, run the commands:
`idr_quota_user`and `idr_quota_project`.

Quotas are organized according to the workspaces, which differ by:
(i) the volume of available space,
(ii) the security of the data (backups), and
(iii) the type of access to the data.
They can be accessed using environment variables:

  - **$HOME** : home directory, with **small size** (3Gb) but very **frequent back-up**,
            mainly used to store small precious data, like code, configurations, etc.
            Quota is per user.
  - **$WORK** : workspace available for **bigger data**, but with **no back-up**,
            usually used to make moderate size simulation or run testcases.
            Quota is per project and typical status is full,
            so be careful to avoid blocking other users.
  - **$SCRATCH** : workspace available **big data** (no quota), but only **temporary**
               (erased automatically after one month),
               with very fast access from the processor (faster than HOME and WORK),
               usually used to put data used and produced by big simulations.
               Good practice is to automatically save final results to STORE
               by a separate postprocessing to avoid automatic deletion.
  - **$STORE** : safe long-term storage of big data, not accessible from computing jobs.
             Be careful of the limited quota on the number of files (inodes),
             thus avoid storing many small files and make archives if necessary(tar).
             Quota is per project, so check what you do (in size and inodes).


## Submitting jobs

Before running computations, always check that your project 
has got enough resources.
To know about available resources, run the command': `idracct`.

Details on job submissions can be found here:
[here](http://www.idris.fr/docs/category/exécutioncontrôle-de-travaux).

## Computing on several projects

If your account is associated to several projects,
you can use the resources of each of them.

- To see your projects : `idrproj`
- To change the default project : `idrproj -d grp1`
- To change the active project : `eval $(idrenv -d grp1)`

Be careful, switching projects will change the env variables HOME, SCRATCH, WORK and STORE.

## Conda environment

- Conda is already installed on jean-zay, you can activate one of the pre-existing environment
via the `module load python=version` command (see all the versions available with `module avail python`)

- You can then create your own environment, that will create a .conda repository in your HOME,
you better move it to your WORK and make a link, because it will increase in size and inodes quite rapidly.



