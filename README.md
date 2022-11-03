# gcm-metadata-for-cmip

contains get_historical_metadata.py

usage: get_historical_metadata('name_of_the_gcm')

"""Python function assigning metadata to the coupled model configurations contributing historical experiments to CMIP5 and 6
    Dependencies: numpy
    input = name of the coupled model configuration (list of character strings), possible entries are (case-sensitive!):
    ['access10','access13','access_cm2','access_esm1_5','awi_esm_1_1_lr','bcc_csm1_1','bcc_csm2_mr','ccsm4','cmcc_cm','cmcc_cm2_hr4','cmcc_cm2_sr5','cmcc_esm2','canesm2','canesm5',
    'cnrm_cm5','cnrm_cm6_1','cnrm_cm6_1_hr','cnrm_esm2_1','csiro_mk3_6_0','ec_earth','ec_earth3','ec_earth3_veg','ec_earth3_veg_lr','ec_earth3_aerchem',
    'ec_earth3_cc','fgoals_g2','fgoals_g3','gfdl_cm3','gfdl_cm4','gfdl_esm2g','gfdl_esm4','giss_e2_h','giss_e2_r','giss_e2_1_g','hadgem2_es','hadgem2_cc',
    'hadgem3_gc31_mm','iitm_esm','inm_cm4','inm_cm5','ipsl_cm5a_lr','ipsl_cm5a_mr','ipsl_cm6a_lr','kiost_esm','miroc5','miroc6','miroc_esm','miroc_es2l','mpi_esm_lr',
    'mpi_esm_mr','mpi_esm_1_2_lr','mpi_esm_1_2_hr','mpi_esm_1_2_ham','mri_esm1','mri_esm2_0','nesm3','noresm1_m','noresm2_lm','noresm2_mm','sam0_unicon','taiesm1']
    output = mrun_f (string) are the run specification, family_f (string) either gcm or esm, doi_f (string) points to reference article(s),
    atmos_f (string) to the AGCM, surface_f (string) to the land surface model, ocean_f (string) to the OGCM, seaice_f (string) to the sea-ice model,
    aersol_f (string) to the aerosol model, chemistry_f (string) to the atmospheric chemistry model(s) in the troposphere and stratosphere,
    obgc_f (string) to the ocean biogeochemistry model, landice_f (string) to the ice-sheet model, coupler_f (string) to the coupling software,
    complex_f is the complexity code described DOI: 10.5194/gmd-2020-418, add_info (string) adds additional info about the component models,
    cmip_f(int) is the cmip generation, rgb_f(string) is the rgb code for the model, marker_f(string) is a specific marker used for visualization,
    latres_atm_f (int) is the number of latitudinal grid-boxes in the AGCM obtained from the reference article and/or netCDF files from ESGF,
    lonres_atm_f (int) is the number of longitudinal grid-boxes in the AGCM, lev_atm_f (int) the number of vertical layers in the AGCM,
    latres_oc_f (int) is the number of latitudinal grid-boxes in the AGCM, lonres_oc_f (int) is the number of longitudinal grid-boxes in the OGCM,
    lev_oc_f (int) is the number of vertical layers in the OGCM, ecs_f (int) and tcr_f (int) are the equilibrium climate sensitivity and transient climate response
    obtained from DOI: 10.1126/sciadv.aba198; if the information for a corresponding parameter could not be found or is not yet in use, then it is set to np.nan.
    Definitions and additional information:
    complex_f integers are for 1. Atmosphere, 2. Land-surface, 3. Ocean, 4. Sea-ice, 5. Vegetation properties, 6. Terrestrial biogeochemistry (tbgc),
    7. Aerosols, 8. Atmospheric chemistry, 9. Ocean biogeochemistry (obgc), 10. Ice sheet dynamics;
    0 = absent, 1 = prescribed or non-interactive or semi-offline (in case of IPSL-CM5A or MPI-ESM1.2-HAM), 2 = interactive and interacting with at least 1 other climate system component
    If the metadata in the nc files (source_id argument) does not agree with the description in the reference article(s), preference is given to the article information.
    If the complexity code was confirmed by a model developer, this is indicated by a comment after the code
    @Author: Swen Brands, MeteoGalicia - Xunta de Galicia, swen.brands@gmail.com
    @Contributors: Jesús Fernández (UC, Spain), Jian Cao (NUIST, China), Bin Wang (IPRC, Hawaii), Laurent Li (LMD, France), Tongwen Wu (Beijing Climate Center, China),
    Evgeny Volodin (INM, Russia), Hiroaki Tatebe (JAMSTEC, Japan), Swapna Panickal (IITM, India), YoungHo Kim (Pukyong National University, Korea),
    Thorsten Mauritsen (MPI, Germany), Øyvind Seland (Norwegian Meteorological Institute), Seiji Yukimoto (MRI, Japan), Klaus Wyser and Ralf Döscher (SMHI, Sweden),
    Annalisa Cherchie and Enrico Scoccimarro (CMCC, Italy), Aurore Voldoire and Roland Séférian (CNRM, France), Olivier Boucher (IPSL,France),
    Peter Gent (NCAR, USA), Tido Semmler (AWI, Germany), Gill Martin (Met Office, UK), Ina Tegen (TROPOS, Germany) and Huan Guo (NOAA, USA)
"""
