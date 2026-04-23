# WRF-Chem-Polar

**WRF-Chem-Polar** is a regional chemistry–climate modeling system based on WRF-Chem, developed collaboratively at IGE and LATMOS (France). 
WRF-Chem-Polar is based on WRF-Chem (developed at NCAR and NOAA, USA) with substantial developments to adapt the model to research applications in polar environments, with a main focus on the Arctic. These developments address key processes that are either absent from, or insufficiently represented in, the standard WRF-Chem distribution, particularly those controlling aerosol-cloud interactions, boundary layer chemistry, and surface-atmosphere coupling over snow, sea ice, and the polar ocean. 

More information:
- [Model homepage](https://wrf-chem-polar.eu)
- [GitHub organization](https://github.com/WRF-Chem-Polar)


### Model Code
The model code is a fork of the main distribution of WRF:
- [Model code](https://github.com/WRF-Chem-Polar/WRF-Chem-Polar)
Detailed documentation of the polar-specific developments is available in [polar-options.md](https://github.com/WRF-Chem-Polar/WRF-Chem-Polar/blob/polar/main/polar-options.md).  

### Infrastructure

A dedicated [infrastructure](https://github.com/WRF-Chem-Polar/WRF-infra) is provided to support reproducible and efficient workflows, including:
- Model configuration and execution scripts 
- Automated testing of developments  
- Post-processing and analysis tools  

The [infrastructure](https://github.com/WRF-Chem-Polar/WRF-infra) is designed for WRF-Chem-Polar, however itcan also be used with standard WRF and WRF-Chem configurations that do not include polar-specific developments.



##  People involved at IGE

|   Name       |  Position         |  Team            |  Building          | What                                                 |
| -------------|:-----------------:|:----------------:|:------------------:|:----------------------------------------------------:|
| [Jennie Thomas](https://www.jennielthomas.fr)    		| CNRS Senior Research Scientist      	| OPERA          	|    MCP             	| Direction and development |
| Lucas Bastien    		| CNRS Research Engineer      	| OPERA/CryoDyn/PING          	|    MCP             	| Software engineering |
| Lucas Giboni    		| PhD student      	| OPERA          	|    OSUG-B             	| Use and development |
| Ruth Price    		| Postdoc      	| OPERA          	|    MCP             	| Use and development |


