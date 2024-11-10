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

Filenames are of the form `subhalo_{ID}_153.hdf5` where `{ID}` is the value of `SUBHALOIDX_0B` in `galaxies.fits`. 

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

All units have been convered from simulated $h=1$ quantiteis to $h=0.704$.

| Dataset | Unit | Description |  
| ------- | ---- | ------------|
| `Coordinates` | Mpc | Particle coordinates relative to the center of the host halo potential | 
| `DMIDs` | Integer | Coco N-body ("dark matter") particle ID associated with tag | 
| `HSML` | Mpc | Particle smoothing lengths | 
| `LookbackFormed` | Gyr | Lookback time at which stellar population tag formed (i.e. stellar population age) | 
| `Mass` | Msun |  Present-day mass of stellar population tag | 
| `Mmetal` | Msun | Present-day mass of metals in stellar population tag  | 
| `ParticleIDs` | Integer | Unique integer ID of stellar population tag | 
| `SubhaloNr` | Integer | ID of subhalo to which tagged DM particle is bound (-1: unbound particles) | 
| `TPSnapshot` | Integer | Snapshot of simulation at which tag was assigned | 
| `Velocities` | km/s | Particle velocities relative to the center of the host halo potential | 

Potentially useful values stored as attributes in the `/Header` group include;

- `BoxSize` : the size of the cutout region for this host halo, in Mpc (NOT the size of the Coco simulation box)
- `GalaxyNumber` : the row number of the central galaxy in the companion `galaxies.fits` table.
- `HSMLNGB`: the number of neighbours used to calculate the adaptive smoothing scale `HSML` for each particle.
- `HaloVelBoxFrame`: the center-of-potential velocity of the halo in the Coco simulation box rest frame.
- `HubbleParam`: The value of the Hubble parameter assumed in Coco

#### Note on the N-body particle mass

We refer to the simulated particles that are used for the positions and velocities of the tags as "N-body particles". Typically (e.g.  in the data model below) these are also called "dark matter particles", occasionally leading to  confusion about their dynamical mass. In a pure N-body cosmological simulation like Coco, all the particles have a mass $m_p$ such that:

$\frac{(\texttt{Number of particles}) \times m_p} {\texttt{Volume occupied by particles}} = \texttt{Total matter density} = (\Omega_\mathrm{{DM}} + \Omega_\mathrm{{b}}) \rho_\mathrm{crit}$

In other words, the dynamical mass of the N-body particle in the simulation includes both the baryon and dark matter contributions to the matter density. Another way of saying this is that the original N-body simulation treats that baryonic contribution as another form of dark matter.

#### Note on stellar evolution

We refer to "oresent-day mass" is the description of the `Mass` and `Mmetal` datasets because the mass of a stellar population changes with time as material is returned to the interstellar medium by winds and supernovae (recycling). The Lacey et al. (2016) Galform model assumes instantaneous recycling, i.e. all stellar population (tag) masses refer to long-lived (mostly main-sequence) stars and compact remanants. See Galform papers for details. 

For luminosity calculations, it may be necessary to know the intial masses of these stellar populations. In this case, this can be done simply by multiplying the present-day mass by a factor 1/R, where R is the assumed instaneous recycled fraction. 

However, for the Lacey et al. 2016 model, this is slightly complicated by the fact that two different initial mass functions (hence values of R) were assumed: a top-heavy IMF in starbursts and a regular (Kennicutt) IMF for quiescent star formation. Unfortunately, the information to track which population formed in which mode is not included in the data for this release.

For the time being, to reasonable approximation, you can just assume the value for the quiescent mode: R = 0.49.

#### Example usage

Example of reading.

#### Acknowledgements

We kindly request use of these data and references to the underlying models to acknowledge the following:

- Cooper et al. (2025) for any use of the Coco particle tagging data;
- Hellwing et al. (2016) for the Coco simulations
- Lacey et al. (2016) in respect of the galaxy formation model used in Cooper et al. (2024)
- Cooper et al. (2010) and Cooper et al. (2017) in respect of the STINGS particle tagging method;
