# Access to french supercomputers

[GENCI](https://www.genci.fr/) is the frencha gency that provides access to the main 3 supercomputer centers :
  - {ref}`IDRIS<idris>`
  - {ref}`CINES<cines>`
  - {ref}`TGCC<tgcc>` 

## Getting an account

Resources on one of the machine of these centers can be obtained by submitting a project to [eDARI](https://www.edari.fr/).

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

## Connecting to a supercomputer

You can only connect from one of the IP address provided to the center.

To connect by SSH through an IGE proxy server,
edit the SSH configuration file (`~/.ssh/config`) to include:

```
Host ige-proxy
     HostName address_of_the_IGE_proxy
     User your_IGE_user_name

Host supercomputer-name
     ProxyJump ige-proxy
     HostName adress-of-the-machine
     User your_user_name
```

You can then connect to the machine with the command:

```
ssh supercomputer-name
```

Then you can share SSH keys (with the proxy and the machine)
to avoid giving your password at each connection.
