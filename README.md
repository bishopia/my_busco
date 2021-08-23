# my_busco
instructions for installing and running busco via singularity container

head over to busco website and find their dockerfile quay url: https://busco.ezlab.org/busco_userguide.html#docker-image

## make sure the following is in .bashrc
```
export SINGULARITY_CACHEDIR=~/scratch/.singularity
export SINGULARITY_TMPDIR=~/scratch/.singularity/tmp
export SINGULARITY_BINDPATH="/gpfs/scratch/ibishop:/scratch,/users/ibishop/data/ibishop:/ccv_data":wq
```

## pull dockerfile and save it in somewhere to keep
```
singularity pull ~/data/ibishop/busco/busco_5.2.2.sif docker://ezlabgva/busco:v5.2.2_cv1
```

## check out .sif by shell command
confirm that the mounted directories look correct
```
singularity shell --no-home ~/data/ibishop/busco/busco_5.2.2.sif
```

## put .sif and fasta and sbatch script in working directory and move there
```
cd $WD
cp $GENOME .
```

#run sif via exec command via sbatch script
```
#!/bin/bash

#SBATCH --time=45:00
#SBATCH --mem=48G #default is 1 core with 2.8GB of memory
#SBATCH -n 12
#SBATCH --account=epscor-condo


singularity exec --no-home ~/data/ibishop/busco/busco_5.2.2.sif busco -i $GENOME --out run1 --mode genome -l stramenopiles_odb10 -f -c 12
```


















