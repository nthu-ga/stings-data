# STINGS Data releases

STINGS stands for Stellar Tags in N-body Galaxy Simulations. The method is described in the following series of papers:

- [Cooper et al. (2010)](http://adsabs.harvard.edu/abs/2010MNRAS.406..744C)
- [Cooper et al. (2013)](https://ui.adsabs.harvard.edu/abs/2013MNRAS.434.3348C)
- [Cooper et al. (2015)](https://ui.adsabs.harvard.edu/abs/2015MNRAS.451.2703C)
- [Cooper et al. (2017)](https://ui.adsabs.harvard.edu/abs/2017MNRAS.469.1691C)

This repository documents publically released data produced with STINGS, starting with the COCO simulations of Cooper et al. (2025). 

Data for the original C10 models of stellar halos in the Aquarius simulations can be found at https://github.com/nthu-ga/aquarius-halos.

### COCO / Galform (Cooper et al. 2025) Data Release 1

Description.

#### Downloading 

The particle data can be found on Zenodo.

How to download.

#### Data model

```
 _ Header
|_ PartType0
    |_ Coordinates
    |_ LastTreeIndex
    |_ Mass
    |_ ParticleIDs
    |_ SubgroupNr
    |_ Velocities
|_ PartType1    
    |_ Coordinates    
    |_ LastTreeIndex    
    |_ Mass
    |_ ParticleIDs
    |_ SubgroupNr
    |_ Velocities
```

#### Example usage

Example of reading.
