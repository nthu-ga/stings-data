# STINGS Data releases

STINGS stands for Stellar Tags in N-body Galaxy Simulations. The method is described in the following series of papers:

- [Cooper et al. (2010)](http://adsabs.harvard.edu/abs/2010MNRAS.406..744C)
- [Cooper et al. (2013)](https://ui.adsabs.harvard.edu/abs/2013MNRAS.434.3348C)
- [Cooper et al. (2015)](https://ui.adsabs.harvard.edu/abs/2015MNRAS.451.2703C)
- [Cooper et al. (2017)](https://ui.adsabs.harvard.edu/abs/2017MNRAS.469.1691C)

This repository documents publically released data produced with STINGS, starting with the COCO simulations of Cooper et al. (2025). 

Data for the original C10 models of stellar halos in the Aquarius simulations can be found at https://github.com/nthu-ga/aquarius-halos.

---

### COCO / Galform (Cooper et al. 2025) Data Release 1

Description.

#### Downloading 

The particle data can be found on Zenodo.

How to download.

#### File Organization

The data are provided in HDF5 format. Each file provides data for a `cutout' around one dark matter halo, including all its satellites. 

The files are organized in the following directory structure:
```
/dr1/cutouts/lacey16/3pc/0153/NNNN
```
where NNNN is a zero-padded integer ranging from 0000 to 0099. This refers to the index of the halo in the `galaxies.fits' table:
```
/dr1/cutouts/lacey16/3pc/0153/galaxies.fits
```

Filenames are of the form `subhalo_{ID}_153.hdf5` where `{}'

```
|_ Config
|_ Header
|_ Parameters
|_ PartType4
   |_ Coordinates
   |_ DMIDs
   |_ HSML
   |_ LookbackFormed
   |_ Mass
   |_ Mmetal
   |_ ParticleIDs 
   |_ SubhaloNr
   |_ TPSnapshot
   |_ Velocities              
```

### Data Model

Each row in the particle datasets corresponds to a "tag" -- equivalent to a star particle in a hydrodynamical simulation, but deriving position and velocity (and subhalo membership) from those of a "parent" N-body particle. Multiple tags (with different ages and metallicites) can be associated with a single N-body particle.

#### File contents

All units have been convered from simulated $h=1$ quantiteis to $h=0.6777$.

|= Dataset =|= Unit =|= Description =|  
| Coordinates | Mpc | | 
| DMIDs | Integer | | 
| HSML | Mpc | | 
| LookbackFormed | Gyr | | 
| Mass | Msun | Present-day mass of metals in stellar population tag | 
| Mmetal | Msun | | 
| ParticleIDs | Integer | Unique integer ID of stellar population tag | 
| SubhaloNr | Integer | ID of subhalo to which tagged DM particle is bound (-1: unbound particles) | 
| TPSnapshot | Integer | Snapshot of simulation at which tag was assigned | 
| Velocities | km/s | Particle velocities relative to center of potential | 

#### A note on the N-body particle mass

We refer to the simulated particles that are used for the positions and velocities of the tags as "N-body particles". Typically (e.g.  in the data model below) these are also called "dark matter particles", occasionally leading to  confusion about their dynamical mass. In a pure N-body cosmological simulation like Coco, all the particles have a mass such that:

$\frac{(\texttt{Number of particles}) \times (\texttt{Particle mass})}{\texttt{Volume occupied by particles}} = \texttt{Total matter density} = \Omega_\mathrm{{m}}\rho_\mathrm{crit}$

In other words, the dynamical mass of the N-body particle in the simulation includes both the baryon and dark matter contributions to the matter density. Another way of saying this is that the original N-body simulation treats that baryonic contribution as another form of dark matter.

#### A note on stellar evolution


#### Example usage

Example of reading.

#### Acknowledgements

We kindly request use of these data and references to the underlying models to acknowledge the following:

- Cooper et al. (2024) for any use of the Coco particle tagging data;
- Hellwing et al. (2016) for the Coco simulations
- Lacey et al. (2016) in respect of the galaxy formation model used in Cooper et al. (2024)
- Cooper et al. (2010) and Cooper et al. (2017) in respect of the STINGS particle tagging method;
