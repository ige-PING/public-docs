(gricad)=

# Gricad mesocenter

Gricad infrastructure provides a lot of resources for all Grenoble University labs. It includes CPU/GPU resources.

For now the most used cluster is dahu which is used for CPU resources.

Gricad is open for any student/researcher/engineer. If you have a contract with Grenoble University, you have already an internal account defined by Agalan Credentials. If you are outside the campus and even outside France, you will get an external account as long as you have an institutional email.

For both cases you will need to log in to a special interface [Perseus](https://perseus.univ-grenoble-alpes.fr) and create an account anyway to join a project.

@IGE, we are a providing a {ref}`straighforward documentation<dahu>`, to start computing rapidly.

You can also have a look at [a more detailled documentation from Gricad](https://gricad-doc.univ-grenoble-alpes.fr/hpc/).

## Architecture of the clusters

### Dahu

Dahu was the main HPC part of GRICAD before the creation of kraken and gathers all CPUs

### Bigfoot

Bigfoot gathers all GPU nodes before the creation of Kraken, as of August 2026, it is composed of :

  - 3 nodes with 4 GPUs Tesla V100 with NV-link
  - 4 nodes with 4 GPUs Tesla V100 with PCIe 
  - 5 nodes with 2 GPUs Tesla A100 

More detailed on bigfoot can be found {ref}`here<bigfoot>`

### Kraken

The kraken supercomputer is splitted in 2 specialized clusters : kraken-cpu and kraken-gpu (by default when you connect to kraken you end up on kraken-cpu)

As of August 2026, Kraken is composed of :

  - 58 AMD EPYC CPU nodes with 192 cores and 768Gb
  - 12 AMD EPYC CPU fat nodes with 192 cores and 1536Gb
  - 13 GPU nodes : AMD EPYC and NVIDIA H100 and H200

More details can be found on this [page](https://gricad-doc.univ-grenoble-alpes.fr/hpc/kraken/kraken/)
