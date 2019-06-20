Tuesday - 6/18/19
==================

> Used CASA's 'impbcor' (primary beam correction) command to reduce 1.4cm continuum image

''''python
cd /lustre/aoc/students/mmadden/downloads/prelim_files
casa #will not run if CASA isn't installed
impbcor(imagename='NGC1333IRAS4A_contful_p0.image.tt0', pbimage='MGC1333IRAS4A_contful_p0.pb.tt0', outfile='NGC1333IRAS4A _contful_p0.pbcor')
''''
