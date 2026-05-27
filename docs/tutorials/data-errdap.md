(errdap)=

# Put data on IGE's Errdap catalog

## Disclaimer

This device is still a work in progress. Processes are not yet in production mode and are still dependent on the availability of a few people. If the need is identified and growing we will put in place automatic procedures and team's delegates so that it is more effective

For now the catalog lives at http://129.88.193.205/erddap/index.html and is only accessible on UGA's network (use the [VPN](https://ige-intranet.osug.fr/spip.php?article640) outside the Campus)

## Prerequisites

First you need to be able to connect to [ige-calcul1](https://ige-ping.github.io/public-docs/docs/clusters/Ige/ige-calcul1.html#igecal1), this is where data transfer can happen 

Then, you have to create your personnal space into your team's space (e.g. cd /catalog/meocean/; mkdir alberta)

## Transfer

You can check the total amount of space available for the catalog by typing the command ```df -h``` and looking for the line

```
152.77.136.14:/DATA_ERDDAP/ige-calcul-storage            48T   13T   36T  27% /catalog
```

The third number will tell you how much space is available.

For now, we suggest that your dataset does not exceed 5Tb.

## Documentation

You need to provide a ini file alongside your dataset called dataset_metadata.info with the following lines, answer on one line :

- mandatory lines :
  - DatasetId= (must be unique and available, otherwise it will be name of the directory+unique tag)
  - Title=
  - Summary= 
  - ContactName=
  - ContactMail=
  - Institution=IGE
  - License=CCBY4
  - EndofSharingDate=
  - Netcdf=Oui ou Non

- optionnal
  - doi=
  - keywords=

 An example can be found [here](https://github.com/ige-PING/public-docs/blob/main/docs/tutorials/template_dataset_metadata.info) 

