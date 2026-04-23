
# Computing on Jean-Zay at IDRIS

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
and at least one secured IGE server (one which is always alive).

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


